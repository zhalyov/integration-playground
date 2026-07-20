# Business Context

## Purpose

Defines the business problem, project objectives and business scope established during the Discovery phase.

This document provides the business context required before defining requirements and designing the integration solution.

## Scope

This document describes:

- the business problem;
- the business objectives;
- the business process overview;
- the business scope.

Detailed business rules, system responsibilities and architectural decisions are documented in their respective Discovery documents.

# Business Context

The customer operates an online charity platform that allows donors to contribute to fundraising campaigns.

When a donation is submitted, multiple business systems must be updated to complete the donation lifecycle.

These systems include donor management, financial processing, reporting and customer communication.

The objective is to automate this process using Frends as the integration platform.

# Problem Statement

The current donation process requires multiple systems to be updated independently.

Without a centralized integration layer this can result in:

- manual work;
- duplicate data entry;
- inconsistent business data;
- increased maintenance effort;
- higher operational risk.

The organization requires a centralized integration solution capable of orchestrating the complete donation workflow.

# Business Objectives

The solution shall:

- automate the donation processing workflow;
- eliminate manual data synchronization;
- maintain data consistency across participating systems;
- provide reliable processing of donation requests;
- improve operational efficiency;
- support temporary system failures through controlled recovery mechanisms.

# Business Process Overview

The donation process begins when a donor submits a donation request.

The integration is responsible for coordinating all required business operations across the participating systems.

The process consists of two logical phases:

## Critical Business Operations

- Validate donation request
- Validate campaign
- Find or create donor
- Register donation
- Create financial record

All critical operations must complete successfully for the donation to be considered successful.

## Post-Processing Operations

- Send confirmation email
- Update reporting database

Post-processing operations enhance the business process but do not determine its success.

# Business Scope

## In Scope

- Donation processing
- Campaign validation
- Donor synchronization
- Donation registration
- Financial record creation
- Confirmation email
- Reporting database update
- Failure handling
- Retry strategy
- Idempotent request processing

## Out of Scope

- Payment provider integration
- Marketing automation
- Data warehouse synchronization
- Scheduled reporting
- Long-running asynchronous recovery
- Distributed transactions

# Related Documents

| Document | Purpose |
|----------|---------|
| [Domain Model](domain-model.md) | Business entities and relationships |
| [System Context](system-context.md) | Participating systems and responsibilities |
| [Business Rules](business-rules.md) | Confirmed business rules |
| [Architecture Decisions](architecture-decisions.md) | Confirmed architectural decisions |
| [Retry Strategy](retry-strategy.md) | Retry and recovery principles |