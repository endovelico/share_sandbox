The **Domain → Glossary** is arguably the most important document in the entire repository.

If the Vision is the "why" and the Domain Model is the "shape," the Glossary is the **language of the system**.

Its purpose is to ensure that when someone says:

> "Order"

everyone means exactly the same thing:

* Product
* Engineering
* QA
* Support
* Operations
* API consumers

A glossary should be treated as a **controlled vocabulary**, not a dictionary.

---

# Domain – Glossary

## Purpose

This glossary defines the canonical terminology used throughout Project XYZ.

All requirements, APIs, architecture documentation, code, user documentation, and operational procedures must use these definitions consistently.

If a term is not defined here, it is not considered part of the domain language.

---

## Rules

### Single Definition

Each domain term has exactly one canonical definition.

---

### No Uncontrolled Synonyms

Avoid:

```text
Customer
User
Account Holder
Client
```

meaning the same thing.

Instead:

```text
Customer
```

becomes the canonical term.

Other terms are mapped explicitly.

---

### Code Alignment

Glossary terms should align with naming used in:

* Domain models
* APIs
* Database schemas
* Source code

If the glossary says:

```text
Order
```

the code should not call it:

```text
PurchaseTransaction
```

unless there is a documented reason.

---

# Domain Terms

---

## Customer

### Definition

A person or organization that purchases products or services.

### Identifier

```text
TERM-001
```

### Synonyms

* Client (deprecated)

### Related Concepts

* Order
* Account

### Notes

A Customer may own multiple Orders.

---

## Account

### Definition

A registered identity associated with a Customer.

### Identifier

```text
TERM-002
```

### Related Concepts

* Customer
* Authentication

### Notes

An Account represents system access, not purchasing activity.

A Customer may exist without an Account.

---

## Order

### Definition

A request by a Customer to purchase one or more Products.

### Identifier

```text
TERM-003
```

### Related Concepts

* Customer
* Product
* Shipment

### Lifecycle

```text
Draft
Submitted
Confirmed
Fulfilled
Cancelled
```

### Notes

Order is the authoritative business object managed by Project XYZ.

---

## Product

### Definition

An item or service available for purchase.

### Identifier

```text
TERM-004
```

### Related Concepts

* Order
* Catalog

---

## Shipment

### Definition

A physical delivery associated with an Order.

### Identifier

```text
TERM-005
```

### Related Concepts

* Order
* Tracking Number

### Notes

An Order may have multiple Shipments.

---

# Domain Events

Glossary should also define important events.

---

## Order Created

### Definition

An event indicating a new Order has been successfully recorded.

### Identifier

```text
EVENT-001
```

### Trigger

Order submission completed successfully.

### Related Concepts

* Order

---

## Order Cancelled

### Definition

An event indicating an Order will no longer proceed through fulfillment.

### Identifier

```text
EVENT-002
```

### Related Concepts

* Order

---

# States

State terminology often causes confusion, so define it explicitly.

---

## Draft

### Definition

Order has been created but not submitted.

### Identifier

```text
STATE-001
```

---

## Submitted

### Definition

Order has been accepted for processing.

### Identifier

```text
STATE-002
```

---

## Fulfilled

### Definition

All required shipments have been completed.

### Identifier

```text
STATE-003
```

---

# Deprecated Terms

These terms should not be used in new documentation.

---

## Purchase Request

### Status

Deprecated

### Replace With

```text
Order
```

### Reason

Terminology standardized across business and technical teams.

---

# Term Relationships

A simple relationship section helps readers understand context.

```text
Customer
    │
    ▼
Order
    │
 ┌──┴────┐
 ▼       ▼
Product Shipment
```

---

# Traceability

Each term should connect to downstream artifacts.

Example:

```text
TERM-003 Order
    ↓
RULE-014
An Order must have exactly one active state

    ↓
REQ-101
Create Order

    ↓
API-017
POST /orders

    ↓
ADR-009
Order State Management Strategy
```

---

# Example of a Mature Glossary Entry

Instead of:

```text
Order:
A customer purchase.
```

write:

```text
Order

Definition:
A request by a Customer to purchase one or more Products.

Identifier:
TERM-003

Lifecycle:
Draft → Submitted → Confirmed → Fulfilled → Cancelled

Related Concepts:
Customer
Product
Shipment

Referenced By:
RULE-014
REQ-101
REQ-102
API-017
API-018

Owner:
Order Domain Team
```

That turns the glossary from a passive reference into the **canonical language layer** that anchors the entire documentation system.

A useful rule is:

> If two people can read a glossary entry and reasonably interpret it differently, the entry is not finished. The glossary should remove ambiguity, not merely describe terms.
