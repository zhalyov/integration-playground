# Business Rules

## Purpose

Defines the confirmed business rules governing the donation processing solution.

Business Rules describe the expected business behavior independently of the technical implementation.

## Scope

This document contains only business rules confirmed during the Discovery phase.

Implementation details, retry strategies and architectural decisions are documented separately.

# Business Rules

| ID | Rule |
|----|------|
| BR-001 | A donor is uniquely identified by their email address. |
| BR-002 | If the donor does not exist, the integration shall create a new donor. |
| BR-003 | Donation amount must be greater than zero. |
| BR-004 | Every donation must belong to an existing campaign. |
| BR-005 | Campaign information is owned by the Backend API. |
| BR-006 | Donation information is owned by the Backend API. |
| BR-007 | Financial records are owned by the ERP system. |
| BR-008 | A donation is considered successful only after all critical business operations complete successfully. |
| BR-009 | Email delivery failures shall not invalidate a successful donation. |
| BR-010 | Reporting failures shall not invalidate a successful donation. |
| BR-011 | Duplicate donation requests must not create multiple donations. |
| BR-012 | Every donation request shall be initiated by the Backend API. |
| BR-013 | Donations must never be lost because of temporary CRM failures. |
| BR-014 | An ERP timeout does not necessarily mean that the financial record was not created. |
| BR-015 | If the ERP system remains unavailable after all recovery attempts, the donation process shall be marked as failed. |
| BR-016 | Every donation request shall contain a unique externalDonationId. |
| BR-017 | externalDonationId shall be used as the business identifier for idempotent request processing. |
| BR-018 | Duplicate donation requests shall return the original successful response. |
| BR-019 | Financial Records shall be uniquely identifiable by externalDonationId. |

# Business Rule Categories

## Validation Rules

- BR-001
- BR-002
- BR-003
- BR-004

## Ownership Rules

- BR-005
- BR-006
- BR-007

## Processing Rules

- BR-008
- BR-011
- BR-012

## Failure Handling Rules

- BR-009
- BR-010
- BR-013
- BR-014
- BR-015

## Idempotency Rules

- BR-016
- BR-017
- BR-018
- BR-019

# Related Documents

| Document | Purpose |
|----------|---------|
| [Business Context](business-context.md) | Business problem and objectives |
| [Domain Model](domain-model.md) | Business entities |
| [Architecture Decisions](architecture-decisions.md) | Technical decisions supporting these rules |
| [Retry Strategy](retry-strategy.md) | Technical retry implementation |