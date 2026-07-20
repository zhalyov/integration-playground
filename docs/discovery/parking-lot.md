# Parking Lot

## Purpose

Captures ideas, improvements and architectural topics intentionally excluded from the current project scope.

These items are not part of the current implementation but may be considered in future project iterations.

## Scope

This document records future enhancements identified during the Discovery phase.

The items listed below are intentionally deferred and should not influence the current solution design.

# Deferred Topics

| Topic | Reason for Deferral | Potential Phase |
|-------|----------------------|-----------------|
| Payment Provider Integration | Outside the scope of the current learning project. | Future Enhancement |
| Marketing Automation | Not required for donation processing. | Future Enhancement |
| Data Warehouse Integration | Reporting Database satisfies the current reporting requirements. | Future Enhancement |
| Scheduled Reporting | Current solution focuses on real-time processing only. | Future Enhancement |
| Queue-based Recovery | Initial implementation uses synchronous processing for critical operations. | Architecture Evolution |
| Distributed Transactions | Adds unnecessary complexity for the current project scope. | Architecture Evolution |
| Dead Letter Queue (DLQ) | Requires asynchronous messaging infrastructure. | Architecture Evolution |
| Circuit Breaker Pattern | Recovery strategy currently relies on bounded retries. | Architecture Evolution |
| Message Queue Integration | Event-driven architecture is outside the scope of the initial implementation. | Architecture Evolution |
| Distributed Tracing | Monitoring requirements are intentionally simplified for the first implementation. | Operations |

# Parking Lot Principles

Topics are added to the Parking Lot when they:

- are valuable but not required for the current scope;
- would significantly increase implementation complexity;
- belong to a future architectural evolution of the solution;
- are intentionally postponed to keep the learning path incremental.

The Parking Lot is reviewed at the beginning of each new project phase to determine whether any deferred topics should be included.

# Related Documents

| Document | Purpose |
|----------|---------|
| [Business Context](business-context.md) | Defines the current project scope |
| [Architecture Decisions](architecture-decisions.md) | Documents the architectural decisions for the current solution |