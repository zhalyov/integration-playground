# Failure Handling Matrix

This document defines how the integration process should respond to failures that may occur during donation processing.

The purpose of this matrix is to classify failures, determine their business impact, and define the expected system behavior.

> **Note**
>
> This document is created during the Discovery phase and may evolve as business requirements become more detailed.

# Process Outcome

The donation process can end in one of the following states.

| Outcome | Description |
|----------|-------------|
| Success | All critical business operations completed successfully. |
| Failed | One or more critical business operations failed. |
| Completed with Warnings | Critical operations succeeded, but one or more non-critical operations failed. |

# Failure Classification

| Component | Failure Scenario | Critical | Retry | Business Impact | Expected Behavior |
|-----------|------------------|:--------:|:-----:|-----------------|-------------------|
| Request Validation | Missing required fields | ✅ | ❌ | Donation cannot be processed | Stop the process and return a validation error. |
| Campaign Validation | Campaign does not exist | ✅ | ❌ | Donation cannot be assigned | Stop the process and return a business validation error. |
| CRM | Unable to find or create donor | ✅ | ✅ | Donation cannot continue | Retry according to retry policy. If unsuccessful, fail the process. |
| Backend API | Unable to register donation | ✅ | ✅ | Donation is not recorded | Retry. If still unsuccessful, fail the process. |
| ERP | Unable to create financial record | ✅ | ✅ | Financial reporting is incomplete | Retry. If unsuccessful, fail the process. |
| Email Service | Confirmation email cannot be sent | ❌ | ✅ | Donor is not notified | Mark the process as completed with warning and retry later. |
| Reporting Database | Unable to store reporting information | ❌ | ✅ | Reporting is incomplete | Retry later without affecting the business process. |

# Critical vs Non-Critical Operations

## Critical Operations

The following operations determine whether the donation has been processed successfully.

- Validate request
- Validate campaign
- Find or create donor
- Register donation
- Create financial record

Failure in any of these operations results in a failed process.

## Non-Critical Operations

The following operations do not invalidate an already completed donation.

- Send confirmation email
- Update reporting database

Failures should be logged and retried asynchronously.

---

# Retry Strategy

| Component | Retry |
|-----------|:-----:|
| CRM | Yes |
| Backend API | Yes |
| ERP | Yes |
| Email Service | Yes |
| Reporting Database | Yes |
| Validation Errors | No |

---

# Business Rules

| ID | Rule |
|----|------|
| FH-001 | Validation failures immediately terminate the process. |
| FH-002 | Donation registration failures terminate the process. |
| FH-003 | Financial record creation failures terminate the process. |
| FH-004 | Email delivery failures do not invalidate a successfully processed donation. |
| FH-005 | Reporting failures do not invalidate a successfully processed donation. |
| FH-006 | All retryable failures must be logged. |

# Recovery Strategy

Whenever possible, retryable failures should be handled automatically.

If automatic retries are exhausted, the process should be marked as failed and the appropriate support team should be notified.

# Open Questions

| ID | Question | Status |
|----|----------|--------|
| FHQ-001 | How many retry attempts should be performed for each external system? | Open |
| FHQ-002 | What is the retry interval? | Open |
| FHQ-003 | Should email retries be synchronous or asynchronous? | Open |
| FHQ-004 | How long should failed requests remain available for manual recovery? | Open |