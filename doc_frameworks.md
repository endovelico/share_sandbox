What you're remembering is probably a mix of **software documentation standards**, **architecture documentation frameworks**, and **requirements/design artifacts**. For a Spring Boot project documented in Confluence, I would avoid trying to force everything into a single template. Instead, use different document types for different questions.

A useful mental model is:

| Question                             | Document Type                       |
| ------------------------------------ | ----------------------------------- |
| Why are we building this?            | Business Requirements / Vision      |
| What problem domain are we modeling? | Domain Model                        |
| What does the system do?             | Functional Requirements / Use Cases |
| How is it designed?                  | Architecture & Design Documents     |
| How do developers work on it?        | Technical Documentation             |
| How do users operate it?             | User Guides / Runbooks              |
| How is it deployed?                  | Operations Documentation            |

---

# 1. Domain Documentation

This answers:

> What business are we in? What concepts exist? What are the rules?

### Domain Model Document

Popular in:

* Domain-Driven Design (DDD)
* Enterprise software

Contents:

* Business context
* Ubiquitous language
* Domain glossary
* Core entities
* Business rules
* Bounded contexts

Example:

```text
Customer
- Can own multiple Orders

Order
- Has OrderLines
- Has Status

Business Rule:
An Order can only be cancelled before shipment.
```

Artifacts:

* Domain glossary
* Context maps
* Entity relationship diagrams

Recommended reading:

Domain-Driven Design

---

# 2. Requirements Documentation

This answers:

> What should the system do?

### BRD (Business Requirements Document)

Contains:

* Problem statement
* Goals
* Stakeholders
* Scope
* Constraints

---

### Use Case Specification

Contains:

* Actor
* Goal
* Preconditions
* Main flow
* Alternative flows
* Postconditions

Example:

```text
Use Case: Create Order

Actor:
Sales Representative

Flow:
1. Select customer
2. Add products
3. Submit order
4. System validates stock
5. System creates order
```

---

### User Story Catalog

Agile teams often replace large BRDs with:

```text
As a customer
I want to cancel an order
So that I can correct mistakes
```

---

# 3. Modeling Documentation

This answers:

> How does the business and software structure work?

### UML Documentation

Still useful for enterprise Spring applications.

Common diagrams:

#### Class Diagram

```text
Customer
Order
Invoice
```

Maps nicely to:

```java
@Entity
public class Customer
```

---

#### Sequence Diagram

Shows:

```text
User
→ Controller
→ Service
→ Repository
→ Database
```

Excellent for Spring Boot APIs.

---

#### Activity Diagram

Shows workflow logic.

Example:

```text
Order Created
↓
Payment Received?
↓
Ship Order
```

---

#### State Diagram

Very useful for:

```text
Order
Draft
Pending
Paid
Shipped
Cancelled
```

---

# 4. Architecture Documentation

This answers:

> How is the application built?

The best modern standard is:

## C4 Model

Created by Simon Brown

For Spring Boot projects, this is arguably the best architecture framework today.

### Level 1 — Context Diagram

```text
Customer
    |
Spring Boot App
    |
Payment Gateway
```

---

### Level 2 — Container Diagram

```text
Web App
REST API
PostgreSQL
Redis
Kafka
```

---

### Level 3 — Component Diagram

```text
Order Controller
Order Service
Order Repository
```

---

### Level 4 — Code Diagram

Usually optional.

---

For Confluence I strongly recommend:

```text
Architecture/
 ├─ Context Diagram
 ├─ Container Diagram
 ├─ Component Diagram
 └─ ADRs
```

---

# 5. ADRs (Architecture Decision Records)

One of the most useful modern practices.

Each document answers:

> Why did we choose this?

Example:

```text
ADR-001
Use PostgreSQL

Context:
Need transactional consistency

Decision:
PostgreSQL

Consequences:
Strong ACID guarantees
```

Over time ADRs become invaluable.

---

# 6. API Documentation

This answers:

> How do consumers use the service?

For Spring Boot:

### OpenAPI / Swagger

Usually generated automatically.

Document:

* Endpoints
* Request payloads
* Responses
* Error codes

---

Additional API guide:

```text
Authentication
Pagination
Versioning
Rate Limits
```

---

# 7. Usage Documentation

This answers:

> How do people use the application?

### User Guide

Contains:

* Screenshots
* Workflows
* Examples

Example:

```text
Creating Orders
Cancelling Orders
Viewing Reports
```

---

### FAQ

Useful for business users.

---

# 8. Operations Documentation

This answers:

> How do we run it?

### Runbook

Contains:

* Startup procedure
* Shutdown procedure
* Monitoring
* Recovery steps

Example:

```text
Service Down

1. Check Kubernetes pods
2. Check DB connectivity
3. Restart deployment
```

---

### Incident Playbooks

Examples:

```text
Database Full
Kafka Down
Redis Failure
```

---

# Recommended Confluence Structure for Spring Boot

```text
Project XYZ

├── 01 Business Context
│   ├── Vision
│   ├── Scope
│   └── Stakeholders
│
├── 02 Domain
│   ├── Glossary
│   ├── Domain Model
│   ├── Business Rules
│   └── Context Maps
│
├── 03 Requirements
│   ├── Use Cases
│   ├── User Stories
│   └── Non-functional Requirements
│
├── 04 Architecture
│   ├── C4 Context
│   ├── C4 Containers
│   ├── C4 Components
│   └── ADRs
│
├── 05 API
│   ├── OpenAPI
│   └── Integration Guides
│
├── 06 Development
│   ├── Local Setup
│   ├── Coding Standards
│   └── Database Migrations
│
├── 07 Operations
│   ├── Deployment
│   ├── Monitoring
│   └── Runbooks
│
└── 08 User Guides
    ├── Tutorials
    └── FAQ
```

For a modern Spring Boot team, the combination of **DDD Domain Model + C4 Architecture + ADRs + OpenAPI + Runbooks** gives you excellent coverage. Those five documentation families answer most of the important questions: *what the business means, what the software does, how it's designed, why decisions were made, and how it's operated*.

