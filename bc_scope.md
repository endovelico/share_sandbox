The **Scope** document is one of the most important—and most neglected—documents in a project.

If Vision answers:

> Why are we doing this?

then Scope answers:

> What are we responsible for, and what are we explicitly not responsible for?

A good scope document prevents requirements creep, architecture sprawl, and ownership confusion.

---

# Business Context → Scope

## Purpose

Define the boundaries of Project XYZ.

This document establishes:

* Capabilities the system owns
* Capabilities the system supports
* Capabilities delegated to other systems
* Explicit exclusions

Scope is a business and organizational boundary document, not a technical design document.

---

# Recommended Structure

```text
Scope
├── Purpose
├── In Scope
├── Out of Scope
├── System Boundaries
├── Assumptions
├── Constraints
└── Future Considerations
```

---

# Example: Order Management Platform

## Purpose

Project XYZ provides centralized order lifecycle management for customer purchases across supported sales channels.

The platform acts as the authoritative source of order state and coordinates interactions between fulfillment and customer-facing systems.

---

# In Scope

The platform is responsible for:

### Order Creation

* Accept customer orders
* Validate order requests
* Generate order identifiers

### Order Lifecycle Management

* Track order status
* Maintain order history
* Manage order state transitions

### Customer Visibility

* Provide order status information
* Expose tracking details
* Support customer inquiries

### Integrations

* Warehouse systems
* Shipping providers
* Customer support systems

### Auditability

* Record all order state changes
* Maintain historical traceability

---

# Out of Scope

The platform is not responsible for:

### Payment Processing

Payments are handled by the Payment Platform.

### Inventory Optimization

Inventory forecasting and allocation remain the responsibility of Inventory Services.

### Marketing Activities

Promotions, campaigns, and customer engagement are managed by Marketing Systems.

### Warehouse Operations

Physical picking, packing, and shipping activities remain external responsibilities.

---

# System Boundaries

## Upstream Systems

Provide data to Project XYZ.

Examples:

* E-commerce Website
* Mobile Application
* Partner Sales Channels

---

## Downstream Systems

Consume information from Project XYZ.

Examples:

* Warehouse Management System
* Shipping Providers
* Reporting Platform

---

## External Dependencies

Project XYZ depends on:

* Identity Provider
* Payment Platform
* Notification Service

These systems are outside Project XYZ ownership.

---

# Assumptions

* Customer identity is managed externally.
* Payments are authorized before order creation.
* Shipping providers expose stable integration interfaces.

If these assumptions change, requirements and architecture may need revision.

---

# Constraints

### Regulatory

* Must retain order history for seven years.

### Operational

* Must support 24/7 operation.

### Organizational

* Inventory management remains owned by Supply Chain Systems.

---

# Future Considerations

Potential future expansions:

* Returns processing
* Subscription order management
* Marketplace seller integrations

These items are not currently in scope.

---

# A Simpler Version for Smaller Projects

For smaller systems, scope can be reduced to three sections.

## Scope

### In Scope

* Customer registration
* Authentication
* Profile management

### Out of Scope

* Identity verification
* Payment processing
* Marketing communications

### Dependencies

* Identity Provider
* Email Service

That's often enough.

---

# Scope Anti-Patterns

### ❌ Listing Features

Bad:

```text
Scope:
- Add dashboard
- Add reports
- Add notifications
```

These are requirements, not scope.

Scope should describe **capabilities and responsibilities**, not backlog items.

---

### ❌ Being Vague

Bad:

```text
The system manages customer experiences.
```

Nobody knows what that means.

---

### ❌ Not Defining Exclusions

Bad:

```text
In Scope:
- Order management
```

Good:

```text
In Scope:
- Order lifecycle management

Out of Scope:
- Payments
- Inventory
- Shipping execution
```

The exclusions are often more valuable than the inclusions.

---

### ❌ Mixing Architecture Into Scope

Bad:

```text
The system uses microservices and Kafka.
```

That belongs in Architecture.

Scope should be understandable by someone who knows nothing about the implementation.

---

# In a Traceable Documentation Model

Scope should become the parent of major requirements.

Example:

```text
SCOPE-001
Manage customer orders
```

Leads to:

```text
REQ-101
Create Order

REQ-102
Cancel Order

REQ-103
Track Order Status
```

But:

```text
Payment Processing
```

is documented as:

```text
OUT-001
Payment authorization is outside project scope.
```

Which prevents someone six months later from creating:

```text
REQ-987
Build custom payment gateway
```

without first changing the approved scope.

A useful rule is:

> **Vision defines why the system exists. Scope defines where its responsibility ends.**

If Vision is the north star, Scope is the fence around the field.
