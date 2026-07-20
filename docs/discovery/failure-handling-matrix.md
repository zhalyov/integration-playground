# Failure Handling Matrix

## Purpose

Defines how failures are classified during the donation processing workflow.

The Failure Handling Matrix identifies the business impact of each failure and its effect on the overall process outcome.

## Scope

This document classifies failures according to:

- failure type;
- affected system;
- business criticality;
- process outcome.

Recovery mechanisms and retry behavior are documented separately in the **Retry Strategy**.

# Failure Classification

| Failure Scenario | Failure Type | Critical | Process Outcome |
|------------------|--------------|:--------:|-----------------|
| Invalid request | Business Validation | ✅ | Failed |
| Campaign not found | Business Validation | ✅ | Failed |
| Backend API unavailable | Technical Failure | ✅ | Failed |
| CRM unavailable | Technical Failure | ✅ | Failed |
| ERP timeout | Technical Failure | ✅ | Failed* |
| ERP unavailable | Technical Failure | ✅ | Failed |
| Email Service unavailable | Technical Failure | ❌ | Completed with Warnings |
| Reporting Database unavailable | Technical Failure | ❌ | Completed with Warnings |

> **Note**
>
> > ERP timeout requires recovery before the final process outcome can be determined. See [Retry Strategy](retry-strategy.md).

# Failure Handling Principles

The solution follows these principles:

- Critical failures prevent successful completion of the donation process.
- Non-critical failures do not invalidate a successfully completed donation.
- Business validation failures are terminal.
- Temporary technical failures may require recovery.
- Recovery mechanisms are defined in the **Retry Strategy**.

# Related Documents

| Document | Purpose |
|----------|---------|
| [Process Outcomes](process-outcomes.md) | Defines the possible outcomes of the donation process |
| [Retry Strategy](retry-strategy.md) | Defines recovery mechanisms for retryable failures |
| [Business Rules](business-rules.md) | Defines the business rules governing the process |