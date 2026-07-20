# Failure Handling Matrix

## Purpose

Defines how failures are classified during the donation processing workflow.

The Failure Handling Matrix determines the business impact of a failure and the resulting process outcome.

## Scope

This document classifies failures according to:

- affected system;
- business criticality;
- process outcome;
- recovery responsibility.

Detailed retry behavior is documented separately in **Retry Strategy**.

# Failure Classification

| System | Critical | Business Impact | Process Outcome |
|---------|:--------:|-----------------|-----------------|
| Backend API | ✅ | Process cannot start | Failed |
| CRM | ✅ | Donor cannot be identified | Failed |
| ERP | ✅ | Financial record cannot be created | Failed |
| Email Service | ❌ | Customer notification unavailable | Completed with Warnings |
| Reporting Database | ❌ | Reporting information unavailable | Completed with Warnings |

# Failure Categories

## Critical Failures

Critical failures prevent successful completion of the donation process.

Examples include:

- invalid request;
- campaign validation failure;
- CRM unavailable;
- ERP unavailable.

Process outcome:

**Failed**

## Non-Critical Failures

Non-critical failures occur after the successful completion of the business transaction.

Examples include:

- confirmation email failure;
- reporting database update failure.

Process outcome:

**Completed with Warnings**

# Failure Matrix

| Failure Scenario | Critical | Process Outcome | Recovery Strategy |
|------------------|:--------:|-----------------|-------------------|
| Invalid request | ✅ | Failed | Not Applicable |
| Campaign not found | ✅ | Failed | Not Applicable |
| CRM unavailable | ✅ | Failed | Retry Strategy |
| ERP timeout | ✅ | Failed* | Retry Strategy |
| ERP unavailable | ✅ | Failed | Retry Strategy |
| Email Service unavailable | ❌ | Completed with Warnings | Retry Strategy |
| Reporting Database unavailable | ❌ | Completed with Warnings | Retry Strategy |

> **Note**
>
> An ERP timeout does not immediately result in a failed process.
> The integration first verifies whether the Financial Record already exists before determining the final outcome.

# Failure Handling Principles

The solution follows the following principles:

- Critical failures prevent successful completion of the business process.
- Non-critical failures do not invalidate a successfully completed donation.
- Business validation errors are not recoverable.
- Temporary infrastructure failures may be recoverable.
- Recovery behavior is defined in the Retry Strategy.

# Related Documents

| Document | Purpose |
|----------|---------|
| [Process Outcomes](process-outcomes.md) | Defines Success, Completed with Warnings and Failed |
| [Retry Strategy](retry-strategy.md) | Defines retry behavior and recovery mechanisms |
| [Business Rules](business-rules.md) | Business rules governing failure scenarios |