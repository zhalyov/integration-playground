# System Context

This document describes the systems participating in the donation workflow and how they interact with each other.

Its purpose is to provide a high-level view of the solution context before the architecture is formalized in the System Architecture document.

> **Note**
>
> This document is part of the Discovery phase and may evolve as new information is confirmed.

---

# Business Context

The customer operates an online charity platform.

When a donor submits a donation, multiple systems must collaborate to validate the request, register the donation, create the related financial record, and send notifications.

Frends is used as the integration layer that orchestrates communication between the systems.

---

# Participating Systems

| System | Responsibility | Source of Truth | Communication with Frends |
|--------|----------------|-----------------|---------------------------|
| Web Application | User interface for submitting donations | ❌ | Indirect |
| Backend API | Receives requests from the Web Application, owns the donation domain, and validates campaigns | ✅ | Direct |
| Frends | Orchestrates the integration workflow | ❌ | N/A |
| CRM | Stores donor information | ✅ | Direct |
| ERP | Stores financial records | ✅ | Direct |
| Email Service | Sends confirmation emails | ❌ | Direct |
| Reporting Database | Stores reporting and analytics data | ✅ | Direct or asynchronous |

---

# System Responsibilities

## Web Application

The Web Application is the entry point for the donor.

It allows the user to submit a donation request, but it does not own the business logic.

---

## Backend API

The Backend API receives requests from the Web Application.

It owns the business representation of the donation and the campaign data.

It is responsible for forwarding the request to Frends for orchestration.

---

## Frends

Frends is the integration layer.

It does not own business data.

Its responsibility is to:

- validate inputs
- orchestrate the workflow
- communicate with external systems
- apply business rules
- handle errors and retries where appropriate

---

## CRM

CRM is the source of truth for donor information.

It stores donor-related data such as:

- first name
- last name
- email
- phone
- address

Frends uses CRM to find or create donor records.

---

## ERP

ERP is the source of truth for financial records.

It stores the financial and accounting representation of a donation.

Frends uses ERP to register the financial impact of the donation.

---

## Email Service

The Email Service is responsible for sending confirmation emails to the donor.

It does not store business data and does not affect the business success of the donation process.

---

## Reporting Database

The Reporting Database stores reporting and analytics data.

It is used for dashboards, reporting, and operational visibility.

Failures in this system do not invalidate a successfully processed donation.

---

# Communication Overview

```text
Donor
  ↓
Web Application
  ↓
Backend API
  ↓
Frends
  ├── CRM
  ├── ERP
  ├── Email Service
  └── Reporting Database