# Project Charter

> Defines the project vision, objectives, scope, and success criteria.

## Related Documents

- [README](../README.md)
- [Business Requirements](02-business-requirements.md)
- [System Architecture](03-system-architecture.md)
- [API Contracts](04-api-contracts.md)

# 1. Project Purpose

Integration Playground is a hands-on portfolio and learning project created to gain practical experience with the **Frends Integration Platform (iPaaS)**.

The project combines theoretical learning with practical implementation by following the complete lifecycle of an enterprise integration project—from business analysis and architecture through implementation, testing, monitoring, deployment, and documentation.

The primary objective is to develop both **Frends platform knowledge** and **real-world integration engineering skills** while building a portfolio-quality project.

# 2. Business Problem

A charity organization receives donations through its web application.

After a donation is submitted, multiple business systems need to be updated.

Without an integration platform, this process would require either manual work or numerous custom integrations between individual systems, resulting in:

- duplicated data
- inconsistent information
- increased maintenance effort
- higher operational costs
- poor scalability

The organization requires a centralized integration platform capable of orchestrating the complete donation workflow while ensuring reliable communication between all participating systems.

# 3. Project Goal

Design and implement a complete integration solution using **Frends**.

The solution should:

- Receive donation requests.
- Validate incoming data.
- Synchronize donor information.
- Register donations.
- Notify external systems.
- Return the execution result.
- Provide monitoring and traceability.

# 4. Project Scope

The project includes:

- Frends Fundamentals
- Integration Architecture
- Process Design
- Triggers
- Tasks
- Variables
- Expressions
- Flow Control
- Data Mapping
- REST Integrations
- API Communication
- Error Handling
- Monitoring
- Deployment
- Documentation
- Testing

---

# 5. Out of Scope

The following topics are intentionally excluded from this project:

- Frontend implementation
- Backend implementation
- Authentication & Authorization implementation
- Infrastructure provisioning
- CI/CD pipelines
- Production environment configuration
- Performance optimization
- Security hardening
- Real third-party integrations

Mock services and simplified APIs will be used whenever appropriate.

# 6. Business Scenario

A donor submits a donation through the web application.

The **Backend API** receives the request and forwards it to **Frends**.

Frends validates the incoming data, orchestrates communication between participating systems, synchronizes business information, and returns the execution result back to the caller.

# 7. Project Stakeholders

| Role | Responsibility |
|------|----------------|
| Product Owner | Defines business requirements and expected business outcomes |
| Integration Engineer | Designs, implements and maintains integration processes |
| Frends Platform | Executes integration workflows |
| CRM System | Stores donor information |
| ERP System | Registers financial transactions |
| Email Service | Sends donor notifications |
| Reporting Database | Stores reporting data |

---

# 8. Participating Systems

| System | Responsibility |
|----------|----------------|
| Web Application | User interface where donations are submitted |
| Backend API | Receives requests from the frontend and forwards them to Frends |
| Frends Platform | Orchestrates the integration workflow |
| CRM | Stores donor information |
| ERP | Registers financial transactions |
| Email Service | Sends confirmation emails |
| Reporting Database | Stores reporting information |

---

# 9. High-Level Architecture

```text
                User
                  │
                  ▼
        Web Application (React)
                  │
                  ▼
            Backend API
                  │
                  ▼
        Frends Integration Platform
          ┌────────┼─────────┐
          ▼        ▼         ▼
        CRM       ERP    Email Service
                    │
                    ▼
           Reporting Database
```

---

# 10. Functional Requirements

### FR-001

The system shall receive a donation request.

### FR-002

The system shall validate all required input fields.

### FR-003

The system shall verify that the campaign exists.

### FR-004

The system shall verify whether the donor already exists.

### FR-005

If the donor does not exist, the system shall create a new donor record.

### FR-006

The system shall register the donation.

### FR-007

The system shall send a confirmation email to the donor.

### FR-008

The system shall return a response indicating whether the process completed successfully.

---

# 11. Non-Functional Requirements

- The solution should be modular.
- The solution should be maintainable.
- Process execution should be traceable through monitoring.
- Errors should be logged and handled appropriately.
- Documentation should be maintained throughout the project.
- Integration processes should be reusable whenever possible.

---

# 12. Assumptions

The project assumes that:

- The CRM system exposes REST APIs.
- The ERP system accepts JSON payloads.
- The Backend API is responsible for authentication.
- Frends is responsible only for orchestration and integration.
- Email notifications can be sent asynchronously.
- Mock services will replace unavailable external systems during development.

---

# 13. Dependencies

The implementation depends on the availability of:

- Frends Platform
- Backend API
- CRM System
- ERP System
- Email Service
- Reporting Database

---

# 14. Success Criteria

The project will be considered successful when:

- A complete integration workflow is implemented.
- All Frends Fundamentals concepts are demonstrated.
- Documentation is complete and kept up to date.
- Every lesson contains a practical implementation.
- The repository can be used as both a portfolio project and a personal learning reference.

---

# 15. Success Metrics

The project is considered complete when:

- 100% of the planned learning modules are completed.
- Every Frends Fundamentals topic has a corresponding practical implementation.
- The end-to-end donation workflow executes successfully.
- Documentation remains synchronized with implementation.
- The project can serve as a reusable learning reference.

---

# 16. Learning Objectives

By completing this project, the learner will be able to:

- Explain the purpose of an iPaaS platform.
- Design integration architectures.
- Create Frends Processes.
- Configure Triggers.
- Work with Variables and Expressions.
- Build workflows using Tasks and Flow Control.
- Integrate multiple systems.
- Monitor and troubleshoot Process executions.
- Deploy integration solutions.
- Document an integration project professionally.

---

# 17. Project Roadmap

| Sprint | Goal |
|---------|------|
| Sprint 0 | Project Foundation |
| Sprint 1 | Frends Fundamentals |
| Sprint 2 | Process Development |
| Sprint 3 | Integrations |
| Sprint 4 | Monitoring & Deployment |
| Sprint 5 | Final Project Review |

---

# 18. Deliverables

At the end of the project, the following artifacts will be available:

- Frends Fundamentals Handbook
- Integration Playground Documentation
- Learning Journal
- Architecture Diagrams
- API Contracts
- Process Documentation
- Test Scenarios
- Monitoring Guide
- Deployment Guide
- Architecture Decision Records (ADR)
- Completed Frends Integration Solution

 ---

## Next Document

➡ [Business Requirements](02-business-requirements.md)