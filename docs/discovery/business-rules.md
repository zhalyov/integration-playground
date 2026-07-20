# Business Rules

## Purpose

Defines the confirmed business rules governing the donation processing solution.

Business Rules describe the expected business behavior independently of the technical implementation.

## Scope

This document contains only business rules confirmed during the Discovery phase.

Implementation details, retry strategies and architectural decisions are documented separately.

Business Rules define **what** the solution must achieve, not **how** it is implemented.

# Business Rules

| ID | Rule |
|----|------|
| BR-001 | A donor is uniquely identified by their email address. |
| BR-002 | If the donor does not exist, the integration shall create a new donor. |
| BR-003 | Donation amount must be greater than zero. |
| BR-004 | Every donation must belong to an existing campaign. |
| BR-005 | A donation is considered successful only after all critical business operations complete successfully. |
| BR-006 | Email delivery failures shall not invalidate a successful donation. |
| BR-007 | Reporting failures shall not invalidate a successful donation. |
| BR-008 | Duplicate donation requests must not create multiple donations. |
| BR-009 | Every donation request shall be initiated by the Backend API. |
| BR-010 | Donations must never be lost because of temporary CRM failures. |
| BR-011 | An ERP timeout does not necessarily mean that the financial record was not created. |
| BR-012 | If the ERP system remains unavailable after all recovery attempts, the donation process shall be marked as failed. |
| BR-013 | Every donation request shall contain a unique request identifier. |

# Related Documents

| Document | Purpose |
|----------|---------|
| [Business Context](business-context.md) | Business problem and objectives |
| [Constraints](constraints.md) | Business and architectural constraints |
| [Domain Model](domain-model.md) | Business entities |
| [Architecture Decisions](architecture-decisions.md) | Technical decisions supporting these rules |
| [Retry Strategy](retry-strategy.md) | Technical retry implementation |