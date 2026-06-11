The **Domain → Domain Model** is where you describe the **structure and behavior of the business domain**, independent of implementation.

If the Glossary defines the vocabulary, the Domain Model defines:

> How those concepts relate to each other and how they change over time.

This is **not** a database schema, API specification, class diagram, or microservice architecture.

A Domain Model should be understandable by:

* Product
* Engineering
* QA
* Architects
* Support

without requiring knowledge of the codebase.

---

# Domain – Domain Model

## Purpose

This document describes the core business concepts managed by Project XYZ, their relationships, lifecycles, and invariants.

The domain model serves as the authoritative representation of the business domain and provides the foundation for requirements, architecture, APIs, and implementation.

---

## Scope

This model covers:

* Domain entities
* Relationships
* Lifecycles
* Ownership boundaries
* Business invariants

This model does not describe:

* Database structures
* Service boundaries
* API contracts
* Technical implementation details

---

# Domain Overview

```text
Customer
    │
    ▼
Order
 ┌──┴─────┐
 ▼        ▼
Order Item Shipment
    │
    ▼
Tracking Event
```

---

# Core Concepts

## Customer

### Description

Represents an individual or organization purchasing products or services.

### Identity

```text
CustomerId
```

### Responsibilities

* Own orders
* Receive notifications
* Maintain purchasing relationship

### Lifecycle

```text
Prospect
    ↓
Active
    ↓
Inactive
```

### Relationships

| Relationship | Type | Cardinality |
| ------------ | ---- | ----------- |
| Order        | Owns | 0..N        |

---

## Order

### Description

Represents a customer's intent to purchase one or more products.

### Identity

```text
OrderId
```

### Responsibilities

* Maintain purchase state
* Track fulfillment progress
* Record business events

### Relationships

| Relationship | Type       | Cardinality |
| ------------ | ---------- | ----------- |
| Customer     | Belongs To | 1           |
| Order Item   | Contains   | 1..N        |
| Shipment     | Produces   | 0..N        |

---

### Lifecycle

```text
Draft
  ↓
Submitted
  ↓
Confirmed
  ↓
Fulfilled

or

Cancelled
```

---

### Invariants

#### INV-001

An Order must belong to exactly one Customer.

---

#### INV-002

An Order must contain at least one Order Item.

---

#### INV-003

An Order may only have one active lifecycle state.

---

## Order Item

### Description

Represents a requested product within an Order.

### Identity

```text
OrderItemId
```

### Relationships

| Relationship | Type       | Cardinality |
| ------------ | ---------- | ----------- |
| Order        | Belongs To | 1           |
| Product      | References | 1           |

---

### Invariants

#### INV-004

Quantity must be greater than zero.

---

## Shipment

### Description

Represents fulfillment of all or part of an Order.

### Identity

```text
ShipmentId
```

### Relationships

| Relationship   | Type      | Cardinality |
| -------------- | --------- | ----------- |
| Order          | Fulfills  | 1           |
| Tracking Event | Generates | 0..N        |

---

### Lifecycle

```text
Created
    ↓
Packed
    ↓
Shipped
    ↓
Delivered
```

---

### Invariants

#### INV-005

A Shipment cannot exist without an associated Order.

---

# Aggregates

If you're using Domain-Driven Design, document aggregate boundaries explicitly.

## Order Aggregate

### Root

```text
Order
```

### Contains

```text
Order
Order Item
```

### Consistency Boundary

All Order state transitions must be validated within the aggregate.

---

### Business Rules

Referenced Rules:

```text
RULE-001
RULE-002
RULE-014
```

---

# Value Objects

These are concepts with identity based on value rather than ownership.

## Address

### Description

Physical delivery location.

### Properties

```text
Street
City
PostalCode
Country
```

### Characteristics

* Immutable
* No independent lifecycle

---

## Money

### Description

Monetary amount in a specific currency.

### Properties

```text
Amount
Currency
```

### Characteristics

* Immutable
* Currency-aware

---

# Domain Events

The model should identify important business events.

## Order Created

### Description

Occurs when an Order is successfully submitted.

### Trigger

```text
Draft → Submitted
```

### Consumers

* Fulfillment
* Notifications
* Analytics

---

## Order Cancelled

### Description

Occurs when an Order is terminated before fulfillment.

### Trigger

```text
Any Active State → Cancelled
```

---

# Bounded Contexts

For larger systems, show where concepts belong.

```text
Sales Context
 ├── Customer
 ├── Order
 └── Order Item

Fulfillment Context
 ├── Shipment
 └── Tracking Event

Billing Context
 ├── Invoice
 └── Payment
```

---

# Context Ownership

| Concept  | Owning Context |
| -------- | -------------- |
| Customer | Sales          |
| Order    | Sales          |
| Shipment | Fulfillment    |
| Invoice  | Billing        |

---

# Traceability

Every domain concept should link downstream.

Example:

```text
Order
    ↓
INV-001
INV-002
INV-003

    ↓
RULE-014

    ↓
REQ-101 Create Order
REQ-102 Cancel Order

    ↓
API-017 POST /orders
API-018 GET /orders/{id}

    ↓
ADR-009 Order State Strategy
```

---

# What a Good Domain Model Answers

A reader should be able to answer:

### What things exist?

```text
Customer
Order
Shipment
```

### How do they relate?

```text
Customer → Order → Shipment
```

### How do they evolve?

```text
Draft → Submitted → Fulfilled
```

### What must always be true?

```text
Order has exactly one active state.
```

### Who owns what?

```text
Sales owns Orders.
Fulfillment owns Shipments.
```

---

# Common Mistakes

### ❌ Database Modeling

Bad:

```text
Orders Table
OrderItems Table
Foreign Key FK_ORDER_ITEM
```

That's design, not domain.

---

### ❌ API Modeling

Bad:

```json
{
  "orderId": "...",
  "customerId": "..."
}
```

That's a contract, not a business model.

---

### ❌ Service Modeling

Bad:

```text
Order Service
Customer Service
Shipment Service
```

That's architecture.

---

### ✅ Domain Modeling

Good:

```text
Customer places Order.

Order contains Order Items.

Order may result in Shipments.

Order progresses through a lifecycle.

Certain invariants must always hold.
```

A useful rule is:

> The Domain Model should describe reality as the business sees it. Architecture, APIs, databases, and code are merely implementations of that reality.
