# Domain Model

## Purpose

Defines the business entities participating in the donation process, their ownership, and the relationships between them.

The Domain Model establishes a common business vocabulary shared by business stakeholders, architects, and developers.

## Scope

This document describes:

- the business entities;
- the ownership of each entity;
- the entity attributes;
- the relationships between entities.

Business rules governing these entities are documented separately in **Business Rules**.

---

# Domain Overview

The donation processing solution is centered around four primary business entities:

- Donor
- Campaign
- Donation
- Financial Record

The solution also includes a supporting communication entity:

- Email Notification

Each entity has a clearly defined Source of Truth responsible for maintaining its lifecycle.

# Domain Ownership

| Entity | Source of Truth |
|---------|-----------------|
| Donor | CRM |
| Campaign | Backend API |
| Donation | Backend API |
| Financial Record | ERP |
| Email Notification | Email Service |

# Business Entities

## Donor

### Description

Represents a person making one or more donations.

### Source of Truth

CRM

### Attributes

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

### Description

Represents a fundraising campaign available for donations.

### Source of Truth

Backend API

### Attributes

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

### Description

Represents the business transaction initiated by a donor.

The Donation is the central business entity of the solution.

### Source of Truth

Backend API

### Attributes

```text
Donation
│
├── donationId
├── externalDonationId
├── donorId
├── campaignId
├── amount
├── currency
├── donationDate
├── paymentMethod
└── status
```

## Financial Record

### Description

Represents the accounting representation of a donation inside the ERP system.

A single Donation may result in one or more Financial Records.

### Source of Truth

ERP

### Attributes

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

### Description

Represents the confirmation email generated after successful donation processing.

### Source of Truth

Email Service

### Attributes

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
                  │
                  │ 1
                  │
                  │ *
              Donation
              /       \
             /         \
            ▼           ▼
     Campaign        Financial Record
        (1)                 (*)

              │
              ▼
      Email Notification
```

# Entity Relationships

| Relationship | Cardinality | Description |
|--------------|:-----------:|-------------|
| Donor → Donation | 1 : * | A donor may make multiple donations. |
| Campaign → Donation | 1 : * | A campaign may receive multiple donations. |
| Donation → Financial Record | 1 : * | A donation may create one or more financial records. |
| Donation → Email Notification | 1 : 1 | A successful donation may generate one confirmation email. |

# Entity Lifecycle

```text
Donor
        │
        ▼
Donation Request
        │
        ▼
Donation
        │
        ▼
Financial Record
        │
        ▼
Email Notification
```

# Related Documents

| Document | Purpose |
|----------|---------|
| [Business Context](business-context.md) | Business problem and objectives |
| [System Context](system-context.md) | Participating systems and responsibilities |
| [Business Rules](business-rules.md) | Business rules governing the entities |
| [Architecture Decisions](architecture-decisions.md) | Architectural decisions affecting the domain |