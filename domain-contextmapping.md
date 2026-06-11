The **Domain → Context Mapping** document is where you stop pretending the system is one clean model and start acknowledging reality:

> Large systems are made of multiple domain models that overlap, conflict, and integrate in controlled ways.

This is one of the most important documents for scaling teams beyond a single bounded context.

---

# Domain – Context Mapping

## Purpose

This document defines:

* How bounded contexts relate to each other
* Where each domain model is valid
* How data and meaning translate across boundaries
* Integration patterns between systems

It ensures that **domain models do not silently leak into each other**.

---

## Key Idea

A core principle:

> A term like “Order” does NOT mean the same thing everywhere.

Each bounded context owns its own meaning.

Context Mapping makes those differences explicit.

---

# System Overview

```text id="ctx_overview"
            ┌────────────────────┐
            │   Sales Context     │
            │  (Order Model)      │
            └─────────┬──────────┘
                      │
                      │ Order Events
                      ▼
            ┌────────────────────┐
            │ Fulfillment Context│
            │ (Shipment Model)   │
            └─────────┬──────────┘
                      │
                      │ Delivery Events
                      ▼
            ┌────────────────────┐
            │ Customer Context    │
            │ (Profile Model)     │
            └────────────────────┘
```

---

# Bounded Contexts

## 1. Sales Context

### Responsibility

Handles commercial intent and order creation.

### Owns Concepts

* Customer (commercial view)
* Order
* Order Item

### Meaning of "Order"

A customer intent to purchase goods.

This is a **business contract state**, not a physical fulfillment record.

---

## 2. Fulfillment Context

### Responsibility

Handles physical execution of orders.

### Owns Concepts

* Shipment
* Tracking Event
* Delivery Status

### Meaning of "Order"

Not directly used.

Instead, it consumes a **Sales Order Snapshot Event**.

Here, the order is treated as immutable input data.

---

## 3. Customer Context

### Responsibility

Maintains identity and profile information.

### Owns Concepts

* Customer Profile
* Preferences
* Contact Information

### Meaning of "Customer"

A persistent identity record used for communication and personalization.

Not responsible for purchase behavior.

---

# Context Relationships

## 1. Sales → Fulfillment

### Type

```text id="cf1"
Customer/Supplier (Downstream Consumer)
```

### Integration Pattern

* Event-driven
* Asynchronous

### Data Flow

```text id="cf2"
Order Created → Order Confirmed → Fulfillment Request Event
```

### Translation Required

Yes.

Sales Order ≠ Fulfillment Order

Mapping required:

| Sales Context | Fulfillment Context |
| ------------- | ------------------- |
| Order         | Fulfillment Request |
| Order Item    | Shipment Line       |
| Customer ID   | Recipient Reference |

---

## 2. Fulfillment → Sales

### Type

```text id="cf3"
Upstream Feedback Provider
```

### Integration Pattern

* Event-driven

### Data Flow

* Shipment Created
* Package Shipped
* Delivery Completed

### Interpretation

Fulfillment does NOT modify Sales Order.

It only emits status updates.

---

## 3. Customer → Sales

### Type

```text id="cf4"
Customer/Supplier
```

### Integration Pattern

* Synchronous + event sync

### Data Flow

* Customer Created
* Customer Updated

### Mapping

Customer identity is shared, but semantics differ:

| Customer Context | Sales Context        |
| ---------------- | -------------------- |
| Profile          | Purchase identity    |
| Preferences      | Marketing attributes |

---

# Context Mapping Patterns

## 1. Conformist

One system accepts the model of another without translation.

Use when:

* External system cannot be changed

Example:

```text id="cm1"
Sales Context conforms to Payment Provider schema
```

---

## 2. Anti-Corruption Layer (ACL)

A translation layer protects the domain model.

Use when:

* External model is messy or unstable

Example:

```text id="cm2"
Fulfillment Context uses ACL to translate Sales Orders → Shipment Requests
```

---

## 3. Shared Kernel

Shared domain model between contexts.

Use when:

* Strong coordination exists
* Teams are tightly aligned

Example:

```text id="cm3"
Shared Customer Identity Model
```

Risk: coupling increases significantly.

---

## 4. Open Host Service

One context provides a stable API for others.

Example:

```text id="cm4"
Sales Context exposes Order API for all consumers
```

---

## 5. Published Language

Shared event vocabulary used across systems.

Example:

```text id="cm5"
OrderCreatedEvent
OrderCancelledEvent
ShipmentDeliveredEvent
```

This is the **preferred integration model in modern systems**.

---

# Context Mapping Matrix

| From \ To   | Sales         | Fulfillment    | Customer        |
| ----------- | ------------- | -------------- | --------------- |
| Sales       | —             | Event stream   | Shared identity |
| Fulfillment | Events only   | —              | None            |
| Customer    | Identity sync | Recipient data | —               |

---

# Anti-Patterns

## ❌ Shared Database Across Contexts

Problem:

* destroys boundaries
* creates hidden coupling

---

## ❌ Same Model Everywhere

Problem:

```text id="bad1"
Order means the same thing in Sales and Fulfillment
```

This almost always leads to:

* unclear ownership
* inconsistent state
* debugging chaos

---

## ❌ Direct Object Reuse

Problem:

```text id="bad2"
Passing domain objects between contexts unchanged
```

Instead, always translate.

---

## ❌ Synchronous Overuse

Problem:

Sales calling Fulfillment synchronously for every state change.

This leads to:

* tight coupling
* cascading failures

---

# Good Context Mapping Test

A healthy system ensures:

* Each bounded context has its own model
* No context directly depends on internal models of another
* All cross-context communication is explicit
* Data is translated at boundaries
* Failure in one context does not corrupt another

---

# Traceability

Context mapping connects everything:

```text id="trace_ctx"
VISION
  ↓
SCOPE
  ↓
DOMAIN MODEL
  ↓
BOUNDING CONTEXTS
  ↓
CONTEXT MAP
  ↓
INTEGRATION DESIGN
  ↓
API / EVENTS
  ↓
IMPLEMENTATION
```

Example:

```text id="trace_ex"
Sales Order Created
    ↓
Published Event
    ↓
Fulfillment ACL translates event
    ↓
Shipment created
    ↓
Tracking events emitted
```

---

# Mental Model

Think of bounded contexts like:

* Countries with different laws
* Same real-world object, different legal interpretations
* Communication happens via treaties (events / APIs)

---

# Key Insight

The most important outcome of context mapping is this:

> It makes explicit where translation must happen, and prevents hidden semantic leakage between parts of the system.

Without it, systems gradually collapse into a single confusing “mega-model.”

With it, you get:

* clear ownership
* independent evolution
* safer integrations
* scalable domain boundaries
