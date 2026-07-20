# Discovery Documentation

This directory contains the documentation produced during the **Discovery phase** of the Integration Playground project.

The Discovery phase establishes the business understanding, identifies participating systems, defines business rules, and documents the architectural decisions required before solution design and implementation begin.

## Discovery Structure

| Document | Responsibility |
|----------|----------------|
| [Discovery Overview](discovery-overview.md) | Executive overview of the Discovery phase |
| [Business Context](business-context.md) | Defines the business problem, objectives and project context |
| [Domain Model](domain-model.md) | Describes the business entities and their relationships |
| [System Context](system-context.md) | Identifies participating systems, responsibilities and communication |
| [Business Rules](business-rules.md) | Defines the confirmed business rules |
| [Constraints](constraints.md) | Documents architectural and business constraints |
| [Architecture Decisions](architecture-decisions.md) | Captures confirmed architectural decisions |
| [Process Outcomes](process-outcomes.md) | Defines the possible outcomes of the business process |
| [Failure Handling Matrix](failure-handling-matrix.md) | Defines failure classification and recovery strategy |
| [Retry Strategy](retry-strategy.md) | Documents retry policies and recovery principles |
| [Parking Lot](parking-lot.md) | Captures ideas and topics intentionally deferred |

## Discovery Lifecycle

```text
Business Context
      │
      ▼
Domain Model
      │
      ▼
System Context
      │
      ▼
Business Rules
      │
      ▼
Constraints
      │
      ▼
Architecture Decisions
      │
      ▼
Failure Handling
      │
      ▼
Retry Strategy
      │
      ▼
Discovery Complete
```

## Navigation

The documents are intended to be read in the order presented above.

Each document focuses on a single responsibility and builds upon the knowledge established by the previous documents.