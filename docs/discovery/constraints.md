# Constraints

## Purpose

Defines the business and architectural constraints that the solution must respect.

Constraints represent fixed conditions established during the Discovery phase.

They are not implementation decisions and cannot be changed by the integration solution.

## Scope

This document captures constraints that influence the architecture and implementation of the donation processing solution.

Implementation decisions based on these constraints are documented separately in **Architecture Decisions**.

# Constraints

| ID | Constraint |
|----|------------|
| C-001 | Frends shall not be the Source of Truth for business data. |
| C-002 | Backend API remains the Source of Truth for Campaigns. |
| C-003 | Backend API remains the Source of Truth for Donations. |
| C-004 | CRM remains the Source of Truth for Donor information. |
| C-005 | ERP remains the Source of Truth for Financial Records. |
| C-006 | Critical business operations must complete before post-processing begins. |
| C-007 | Every business entity shall have a single Source of Truth. |

# Related Documents

| Document | Purpose |
|----------|---------|
| [Business Rules](business-rules.md) | Business behaviour constrained by these rules |
| [Architecture Decisions](architecture-decisions.md) | Technical decisions derived from these constraints |
| [System Context](system-context.md) | Systems participating in the solution |
| [Domain Model](domain-model.md) | Business entities governed by these constraints |