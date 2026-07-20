# Constraints

## Purpose

Defines the business and architectural constraints that the solution must respect.

Constraints represent fixed conditions established during the Discovery phase. They are not implementation decisions and cannot be changed by the integration solution.

## Scope

This document captures constraints that influence the architecture and implementation of the donation processing solution.

Implementation decisions based on these constraints are documented separately in **Architecture Decisions**.

# Constraints

| ID | Constraint |
|----|------------|
| C-001 | Frends is responsible only for orchestration and does not own business data. |
| C-002 | Backend API remains the Source of Truth for Campaigns. |
| C-003 | Backend API remains the Source of Truth for Donations. |
| C-004 | CRM remains the Source of Truth for Donor information. |
| C-005 | ERP remains the Source of Truth for Financial Records. |
| C-006 | Critical business operations must complete before post-processing begins. |
| C-007 | Business data shall never be duplicated across systems of record. |
| C-008 | Every business entity shall have a single Source of Truth. |

# Constraint Categories

## Ownership Constraints

- C-001
- C-002
- C-003
- C-004
- C-005

These constraints define which system owns each business entity.

## Process Constraints

- C-006

Defines the mandatory execution order of the business process.

## Data Integrity Constraints

- C-007
- C-008

These constraints ensure consistent ownership and integrity of business data across the solution.

# Related Documents

| Document | Purpose |
|----------|---------|
| [Business Rules](business-rules.md) | Business behaviour constrained by these rules |
| [Architecture Decisions](architecture-decisions.md) | Technical decisions derived from these constraints |
| [System Context](system-context.md) | Systems participating in the solution |