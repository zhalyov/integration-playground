# Discovery Notes

This document captures information gathered during the discovery phase of the project.

Its purpose is to collect, validate, and refine business knowledge before it is formalized in the **Business Requirements Specification (BRS)**.

> **Note**
>
> The information in this document is considered preliminary and may change as new business requirements are discovered.

---

# Discovery Status

**Current Sprint**

Sprint 1 — Business Discovery & Analysis

---

# Business Context

## Problem Statement

The customer operates an online charity platform.

When a donor submits a donation, multiple business systems must be updated.

The current process requires manual work and duplicate data entry.

The objective is to automate the workflow using Frends.

# Architectural Insight

The integration workflow is divided into two logical phases.

## Critical Business Operations

- Validate Request
- Validate Campaign
- Find or Create Donor
- Register Donation
- Create Financial Record

Failure in any of these operations results in a failed business process.

## Post-Processing Operations

- Send Confirmation Email
- Update Reporting Database

Failures in post-processing operations do not invalidate an already successful donation.

# Confirmed Systems

| System | Responsibility | Source of Truth |
|---------|----------------|:---------------:|
| Web Application | Donation submission | ❌ |
| Backend API | Receives requests and owns the donation domain | ✅ |
| Frends | Integration orchestration | ❌ |
| CRM | Donor management | ✅ |
| ERP | Financial records | ✅ |
| Email Service | Notifications | ❌ |
| Reporting Database | Reporting | ✅ |

# Domain Model

## Donor

Represents a person making one or more donations.

**Source of Truth:** CRM

```text
Donor
│
├── donorId
├── firstName
├── lastName
├── email
├── phone
└── address
```

## Campaign

Represents a fundraising campaign.

**Source of Truth:** Backend API

```text
Campaign
│
├── campaignId
├── title
├── description
├── status
├── startDate
└── endDate
```

## Donation

Represents the business transaction initiated by a donor.

**Source of Truth:** Backend API

```text
Donation
│
├── donationId
├── donorId
├── campaignId
├── amount
├── currency
├── donationDate
├── paymentMethod
├── externalDonationId
└── status
```

## Financial Record

Represents the accounting representation of a donation.

A Donation may create one or more Financial Records.

**Source of Truth:** ERP

```text
FinancialRecord
│
├── transactionId
├── donationId
├── accountingDate
├── amount
├── currency
├── ledgerAccount
└── status
```

## Email Notification

Represents the confirmation email sent after successful processing.

**Source of Truth:** Email Service

```text
EmailNotification
│
├── recipient
├── subject
├── template
├── sentAt
└── status
```

# Domain Relationships

```text
Donor
   │1
   │
   │*
Donation
   │
   ├──────────────► Campaign (1)
   │
   └──────────────► Financial Record (*)
```

# Confirmed Business Rules

| ID | Rule |
|----|------|
| BR-001 | A donor is uniquely identified by their email address. |
| BR-002 | If the donor does not exist, the integration shall create a new donor. |
| BR-003 | Donation amount must be greater than zero. |
| BR-004 | Every donation must belong to an existing campaign. |
| BR-005 | Campaign information is owned by the Backend API. |
| BR-006 | Donation is owned by the Backend API. |
| BR-007 | Financial records are owned by the ERP system. |
| BR-008 | A donation is considered successful only after all critical business operations complete successfully. |
| BR-009 | Email delivery failures do not invalidate a successful donation. |
| BR-010 | Reporting failures do not invalidate a successful donation. |
| BR-011 | Duplicate donation requests must not create multiple donations. |
| BR-012 | Every donation request shall be initiated by the Backend API. |
| BR-013 | Donations must never be lost because of temporary CRM failures. |
| BR-014 | Temporary CRM failures shall trigger automatic retries before the process is marked as failed. |
| BR-015 | An ERP timeout does not necessarily mean that the financial record was not created. |
| BR-016 | The integration shall verify the ERP state before retrying a timed-out operation. |
| BR-017 | If ERP remains unavailable after all retry attempts, the process shall be marked as failed. |
| BR-018 | Email delivery retries should be performed asynchronously whenever possible. |
| BR-019 | Reporting updates should be performed asynchronously whenever possible. |
| BR-021 | Every donation request shall contain a unique externalDonationId. |
| BR-022 | The integration shall use externalDonationId as the primary idempotency key. |
| BR-022 | Every donation request shall contain a unique externalDonationId. |
| BR-023 | The Backend API shall guarantee idempotency for donation requests. |
| BR-024 | Duplicate donation requests shall return the original successful response. |
| BR-025 | Retry shall be applied only to transient technical failures. |
| BR-026 | Critical systems shall use a bounded retry strategy. |
| BR-027 | Non-critical post-processing operations shall use asynchronous retry whenever possible. |
| BR-028 | ERP financial records shall be searchable by externalDonationId. |
| BR-029 | After an ERP timeout, the integration shall verify whether the financial record already exists before retrying the create operation. |

# Constraints

| ID | Constraint |
|----|------------|
| C-001 | Frends is responsible only for orchestration and does not own business data. |
| C-002 | Backend API remains the Source of Truth for Campaigns and Donations. |
| C-003 | CRM remains the Source of Truth for Donor information. |
| C-004 | ERP remains the Source of Truth for Financial Records. |
| C-005 | Critical operations must complete before post-processing begins. |

# Assumptions

| ID | Assumption | Status |
|----|------------|--------|
| A-001 | CRM is available during normal business operations. | Confirmed |
| A-002 | ERP supports unique identification of Financial Records. | Pending Validation |
| A-003 | Backend API performs authentication before invoking Frends. | Confirmed |

# Decisions Made During Discovery

| ID | Decision |
|----|----------|
| D-001 | Donor identification is based on the email address. |
| D-002 | Frends is responsible only for orchestration. |
| D-003 | The donation workflow starts with an HTTP request from the Backend API. |
| D-004 | CRM availability is required before a donation can be completed successfully. |
| D-005 | ERP timeout handling requires state verification before retry. |
| D-006 | The initial solution uses synchronous processing for critical operations. |
| D-007 | Email Service is treated as a non-critical dependency. |
| D-008 | Reporting Database is treated as a non-critical dependency. |
| D-009 | Email retries should be asynchronous. |
| D-010 | Reporting updates should be asynchronous. |
| D-011 | Duplicate detection is based on externalDonationId. |
| D-017 | The Backend API is the system of record for donation request idempotency. |
| D-018 | Duplicate requests are handled using idempotent responses. |
| D-019 | The initial solution uses a bounded synchronous retry strategy for critical systems and asynchronous retry for post-processing operations. |
| D-020 | ERP must support lookup of Financial Records by externalDonationId to safely handle timeout recovery. |

# Process Outcome

| Outcome | Description |
|----------|-------------|
| Success | All critical business operations completed successfully. |
| Completed with Warnings | Critical operations completed successfully, but one or more non-critical operations failed. |
| Failed | One or more critical business operations failed. |

# Retry Policy

The integration applies different retry strategies depending on the type of operation and failure.

## Retry Classification

| Operation | Critical | Retry Strategy | Maximum Attempts | Failure Outcome |
|-----------|:--------:|----------------|:----------------:|-----------------|
| CRM | ✅ | Synchronous Retry | Configurable | Process Failed |
| ERP | ✅ | Synchronous Retry with State Verification | Configurable | Process Failed |
| Email Service | ❌ | Asynchronous Retry | Configurable | Completed with Warnings |
| Reporting Database | ❌ | Asynchronous Retry | Configurable | Completed with Warnings |

## Retry Rules

| ID | Rule |
|----|------|
| RP-001 | Retry shall be performed only for transient technical failures. |
| RP-002 | Business validation errors shall never be retried. |
| RP-003 | Critical business operations shall use bounded synchronous retry. |
| RP-004 | ERP timeout recovery requires state verification before retrying the create operation. |
| RP-005 | Post-processing operations shall use asynchronous retry whenever possible. |
| RP-006 | After the maximum retry attempts are exhausted, the process shall be marked according to the operation type. |

## Retry Decision Matrix

| Failure Type | Retry | Reason |
|--------------|:-----:|--------|
| Network Timeout | ✅ | Temporary communication issue |
| HTTP 500 | ✅ | Temporary server failure |
| HTTP 503 | ✅ | Service temporarily unavailable |
| Connection Refused | ✅ | Infrastructure issue |
| Invalid Campaign | ❌ | Business validation error |
| Invalid Request | ❌ | Client error |
| Duplicate Donation | ❌ | Already processed |
| Validation Failure | ❌ | Business rule violation |

## ERP Timeout Recovery

```text
Create Financial Record
        │
        ▼
Timeout
        │
        ▼
Lookup Financial Record
by externalDonationId
        │
   ┌────┴────┐
   │         │
Exists     Not Found
   │         │
Success    Retry
```

The integration must verify the ERP state before retrying to prevent duplicate financial records.

## Retry Philosophy

The retry strategy follows four principles:

1. Retry only when the failure is considered temporary.
2. Never retry business validation errors.
3. Verify state before retrying non-idempotent operations.
4. Never allow retry logic to create duplicate business records.

# Parking Lot

The following topics are currently outside the scope of Sprint 1.

- Payment Provider integration
- Marketing automation
- Data Warehouse integration
- Scheduled reporting
- Queue-based recovery for prolonged ERP outages
- Distributed transactions
- Dead Letter Queue (DLQ)

# Discovery Summary

The Discovery Workshop concluded with all identified business and architectural questions resolved.

The confirmed decisions captured in this document serve as the foundation for:

- Business Requirements Specification
- System Architecture
- Process Design

# Next Steps

Complete the remaining Discovery questions.

Transform confirmed information into:

- Business Requirements Specification
- System Architecture
- Process Design