# Process Outcomes

## Purpose

Defines the possible outcomes of the donation processing workflow.

## Scope

This document describes the possible end states of the donation process.

Failure classification and recovery behavior are documented separately in the **Failure Handling Matrix** and **Retry Strategy**.

# Process Outcomes

| Outcome | Description |
|----------|-------------|
| Success | All critical business operations completed successfully. |
| Failed | One or more critical business operations could not be completed successfully. |
| Completed with Warnings | All critical business operations completed successfully, but one or more non-critical operations failed. |

# Outcome Determination

The final process outcome is determined after all critical business operations have been evaluated.

| Condition | Process Outcome |
|-----------|-----------------|
| All critical operations completed successfully | **Success** |
| One or more critical operations failed | **Failed** |
| All critical operations completed successfully, but one or more non-critical operations failed | **Completed with Warnings** |

# Outcome Principles

The donation process follows these principles:

- The final outcome is determined only after all critical business operations have been evaluated.
- A failure of any critical business operation results in a **Failed** outcome.
- Failures occurring after successful completion of all critical business operations do not invalidate the donation.
- Non-critical failures result in **Completed with Warnings**.

# Related Documents

| Document | Purpose |
|----------|---------|
| [Failure Handling Matrix](failure-handling-matrix.md) | Classifies failures and their business impact |
| [Retry Strategy](retry-strategy.md) | Defines recovery mechanisms for retryable failures |
| [Business Rules](business-rules.md) | Defines the business rules governing process execution |