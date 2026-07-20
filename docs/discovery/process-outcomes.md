# Process Outcomes

## Purpose

Defines the possible outcomes of the donation processing workflow.

The process outcome is determined after all critical business operations have been evaluated.

## Scope

This document describes the possible completion states of the donation process.

The conditions leading to each outcome are documented in the **Failure Handling Matrix**.

# Process Outcomes

| Outcome | Description |
|----------|-------------|
| Success | All critical business operations completed successfully. |
| Completed with Warnings | All critical business operations completed successfully, but one or more non-critical operations failed. |
| Failed | One or more critical business operations failed. |

# Outcome Classification

## Success

A process is considered successful when:

- the request is valid;
- the campaign exists;
- the donor has been found or created;
- the donation has been registered;
- the financial record has been created.

## Completed with Warnings

A process is considered completed with warnings when:

- all critical business operations completed successfully;
- one or more post-processing operations failed.

Typical examples include:

- confirmation email delivery failure;
- reporting database update failure.

## Failed

A process is considered failed when at least one critical business operation cannot be completed.

Typical examples include:

- campaign validation failure;
- CRM unavailable after all recovery attempts;
- ERP unavailable after all recovery attempts;
- invalid donation request.

# Related Documents

| Document | Purpose |
|----------|---------|
| [Business Rules](business-rules.md) | Business rules governing process execution |
| [Failure Handling Matrix](failure-handling-matrix.md) | Failure classification and recovery |
| [Retry Strategy](retry-strategy.md) | Retry behaviour for each failure type |