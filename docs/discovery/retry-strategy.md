# Recovery Strategy by Operation

## Purpose

Defines the recovery mechanisms applied by the integration solution when handling transient technical failures.

The retry strategy improves solution reliability while preventing duplicate business transactions.

## Scope

This document defines:

- recovery strategies for retryable operations;
- retry rules;
- ERP timeout recovery;
- retry principles.

Failure classification and process outcomes are documented separately.

# Recovery Strategies

| Operation | Recovery Strategy | Notes |
|-----------|-------------------|------|
| CRM | Bounded Synchronous Retry | Critical business operation |
| ERP | Bounded Synchronous Retry with State Verification | Critical business operation |
| Email Service | Asynchronous Retry | Post-processing operation |
| Reporting Database | Asynchronous Retry | Post-processing operation |

# Retry Rules

| ID | Rule |
|----|------|
| RP-001 | Retry shall be performed only for transient technical failures. |
| RP-002 | Business validation failures shall never be retried. |
| RP-003 | Retry configuration shall remain environment-specific. |
| RP-004 | ERP timeout recovery shall verify the current ERP state before retrying the create operation. |
| RP-005 | Post-processing operations shall use asynchronous retry whenever possible. |
| RP-006 | Maximum retry attempts shall be configurable. |

# ERP Timeout Recovery

When an ERP timeout occurs, the integration shall not immediately retry the create operation.

Instead, the integration shall verify whether the Financial Record has already been created by using the request identifier before issuing another create request.

```text
Create Financial Record
        │
        ▼
Timeout
        │
        ▼
Lookup by request identifier
        │
   ┌────┴────┐
   │         │
Exists     Not Found
   │         │
Success    Retry