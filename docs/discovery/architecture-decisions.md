# Architecture Decisions

## Purpose

Captures the architectural decisions made during the Discovery phase.

Architecture Decisions describe how the solution will be designed to satisfy the business requirements while respecting the identified constraints.

## Scope

This document records only confirmed architectural decisions.

Business Rules, Constraints and Retry Strategy are documented separately.

# Architecture Decisions

| ID | Decision |
|----|----------|
| D-001 | Frends is used as the integration orchestration layer. |
| D-002 | The donation workflow is initiated by the Backend API through an HTTP request. |
| D-003 | Critical business operations are executed synchronously. |
| D-004 | Post-processing operations are executed after successful completion of the critical flow. |
| D-005 | Email Service is treated as a non-critical dependency. |
| D-006 | Reporting Database is treated as a non-critical dependency. |
| D-007 | Duplicate request detection is based on the request identifier (`externalDonationId`). |
| D-008 | The Backend API provides the unique request identifier required for idempotent processing.|
| D-009 | Duplicate requests return the original successful response. |
| D-010 | ERP timeout recovery requires verification of the current ERP state before retrying the create operation. |

## Related Documents

| Document | Purpose |
|----------|---------|
| [Business Rules](business-rules.md) | Business behaviour requiring these decisions |
| [Constraints](constraints.md) | Architectural limitations respected by these decisions |
| [Retry Strategy](retry-strategy.md) | Technical recovery strategy |
| [System Context](system-context.md) | Systems participating in the solution |