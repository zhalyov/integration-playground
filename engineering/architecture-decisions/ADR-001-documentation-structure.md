# ADR-001: Documentation Structure

**Status:** Accepted

**Date:** 2026-07-16

# Context

The **Integration Playground** project contains two different types of documentation:

1. Documentation describing the integration solution being built.
2. Documentation describing the engineering standards and development practices followed during the project.

Initially, both types of documentation were considered part of the same documentation structure. As the project evolved, it became clear that mixing them would make navigation more difficult and blur the responsibility of each document.

To keep the documentation maintainable and easy to understand, a clear separation was required.

# Decision

The documentation is divided into two independent sections.

## Project Documentation

The `docs/` directory contains documentation describing **the solution itself**.

Examples:

- Project Charter
- Business Requirements
- System Architecture
- API Contracts
- Process Design
- Testing
- Monitoring
- Deployment

## Engineering Handbook

The `engineering/` directory contains documentation describing **how the project is developed**.

Examples:

- Engineering Principles
- Git Workflow
- Project Versioning
- Development Workflow
- Documentation Standards
- Architecture Decision Records (ADR)

# Rationale

The separation follows several engineering principles:

- Single Responsibility
- Single Source of Truth (SSOT)
- Don't Repeat Yourself (DRY)
- Separation of Concerns

Each document has one clear responsibility and should avoid duplicating information maintained elsewhere.

# Consequences

## Positive

- Clear separation between project documentation and engineering standards.
- Easier navigation.
- Better maintainability.
- Reduced duplication.
- Easier onboarding for new contributors.

## Negative

- Readers must understand the difference between project documentation and engineering documentation.
- Some documents reference each other instead of containing all related information.

# Alternatives Considered

## Alternative 1

Store all documentation under a single `docs/` directory.

**Rejected**

Reason:

Project documentation and engineering standards have different purposes and responsibilities.

## Alternative 2

Mix engineering standards inside the project documentation.

**Rejected**

Reason:

This would violate the Single Responsibility principle and increase duplication.

# Decision Drivers

The decision was guided by the following principles:

- Simplicity
- Maintainability
- Clear ownership of information
- Scalability
- Professional documentation structure

# Related Documents

- [Engineering Principles](../engineering-principles.md)
- [Project Charter](../../docs/01-project-charter.md)