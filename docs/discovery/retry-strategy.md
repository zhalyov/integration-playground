# Retry Strategy

## Purpose

Defines the retry strategy applied by the integration solution when recovering from temporary technical failures.

The retry strategy aims to improve reliability while preventing duplicate business transactions.

## Scope

This document describes:

- retry classification;
- retry rules;
- retry decision matrix;
- ERP timeout recovery;
- retry principles.

Failure classification and process outcomes are documented separately.

# Retry Classification

| Operation | Retry Strategy | Notes |
|-----------|----------------|------|
| CRM | Bounded Synchronous Retry | Critical business operation |
| ERP | Bounded Synchronous Retry with State Verification | Critical business operation |
| Email Service | Asynchronous Retry | Post-processing |
| Reporting Database | Asynchronous Retry | Post-processing |

# Retry Rules

| ID | Rule |
|----|------|
| RP-001 | Retry shall be performed only for transient technical failures. |
| RP-002 | Business validation errors shall never be retried. |
| RP-003 | Retry configuration shall remain environment-specific. |
| RP-004 | ERP timeout recovery requires state verification before retrying the create operation. |
| RP-005 | Post-processing operations shall use asynchronous retry whenever possible. |
| RP-006 | Maximum retry attempts shall be configurable. |

# Retry Decision Matrix

| Failure Type | Retry | Reason |
|--------------|:-----:|--------|
| Network Timeout | ✅ | Temporary communication failure |
| HTTP 500 | ✅ | Temporary server failure |
| HTTP 503 | ✅ | Service temporarily unavailable |
| HTTP 429 | ✅ | Retry according to Retry-After header when available |
| Connection Refused | ✅ | Temporary infrastructure failure |
| DNS Resolution Failure | ✅ | Temporary infrastructure failure |
| Invalid Request | ❌ | Business validation error |
| Campaign Not Found | ❌ | Business validation error |
| Duplicate Donation | ❌ | Already successfully processed |

# ERP Timeout Recovery

When an ERP timeout occurs, the integration shall not immediately retry the create operation.

Instead, it shall verify whether the Financial Record has already been created.

```text
Create Financial Record
        │
        ▼
Timeout
        │
        ▼
Lookup by externalDonationId
        │
   ┌────┴────┐
   │         │
Exists     Not Found
   │         │
Success    Retry
```

This approach prevents duplicate Financial Records.

# Retry Principles

The retry strategy follows the following principles:

- Retry only temporary technical failures.
- Never retry business validation errors.
- Verify system state before retrying non-idempotent operations.
- Never allow retry logic to create duplicate business records.
- Keep retry behavior configurable rather than hardcoded.

# Related Documents

| Document | Purpose |
|----------|---------|
| [Failure Handling Matrix](failure-handling-matrix.md) | Failure classification |
| [Architecture Decisions](architecture-decisions.md) | Architectural decisions supporting the retry strategy |
| [Business Rules](business-rules.md) | Business rules governing process execution |