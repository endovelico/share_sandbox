The **Domain → Business Rules** document is where your system becomes *non-negotiable*.

If the Domain Model describes:

> “what exists and how it relates”

then Business Rules describe:

> “what must always be true, no matter what”

These rules are the **hard constraints of the business domain**. They are what prevent systems from drifting into inconsistent or invalid states.

---

# Domain – Business Rules

## Purpose

This document defines the authoritative set of business rules that govern the behavior of Project XYZ.

Business rules are:

* invariant constraints on the domain
* independent of technical implementation
* enforceable across all interfaces (API, UI, batch, integrations)

All systems interacting with Project XYZ MUST respect these rules.

---

## Rules vs Other Concepts

| Type           | Meaning                  | Example                             |
| -------------- | ------------------------ | ----------------------------------- |
| Vision         | Why we exist             | “Provide unified order management”  |
| Scope          | What we own              | “Order lifecycle is in scope”       |
| Domain Model   | What exists              | “Order, Customer, Shipment”         |
| Business Rules | What must always be true | “Order must have at least one item” |
| Requirements   | What we build            | “User can cancel order”             |

---

# Rule Format

All rules MUST follow this structure:

```text id="rule_format"
RULE-XXX: Short title

Statement:
Clear, testable constraint

Context:
Why this rule exists

Exceptions:
If any (default: none)

Enforcement:
Where this rule is enforced (Domain / API / DB / Event system)
```

---

# Core Business Rules

---

## RULE-001: Order Ownership

### Statement

An Order MUST belong to exactly one Customer.

### Context

Orders represent a purchase intent tied to a single customer identity.

### Exceptions

None.

### Enforcement

* API validation
* Domain layer
* Database foreign key constraint

---

## RULE-002: Order Must Contain Items

### Statement

An Order MUST contain at least one Order Item before it can be submitted.

### Context

Empty orders have no business meaning and cannot be fulfilled.

### Exceptions

Draft state may allow zero items temporarily.

### Enforcement

* Domain layer
* API validation on submission

---

## RULE-003: Immutable Order Items After Confirmation

### Statement

Once an Order reaches CONFIRMED state, its Order Items MUST NOT be modified.

### Context

Downstream systems (billing, warehouse, shipping) depend on a stable snapshot.

### Exceptions

None.

### Enforcement

* Domain logic
* API restrictions
* Event versioning

---

## RULE-004: Valid State Transitions Only

### Statement

An Order MAY only transition through defined lifecycle states.

Allowed transitions:

```text id="state_rules"
Draft → Submitted → Confirmed → Fulfilled
           ↘
         Cancelled
```

### Context

Prevents invalid or inconsistent order progression.

### Exceptions

System recovery processes may override in controlled scenarios.

### Enforcement

* Domain state machine
* API layer
* Event processing

---

## RULE-005: Single Active State

### Statement

An Order MUST have exactly one active lifecycle state at any time.

### Context

Prevents ambiguity in downstream systems.

### Exceptions

None.

### Enforcement

* Domain model
* Persistence constraints

---

## RULE-006: Shipment Requires Confirmed Order

### Statement

A Shipment MUST NOT be created unless the associated Order is in CONFIRMED or later state.

### Context

Shipping cannot occur for unvalidated orders.

### Exceptions

Manual override for emergency logistics.

### Enforcement

* Fulfillment service
* Event processing rules

---

## RULE-007: Customer Identity Consistency

### Statement

All Orders belonging to a Customer MUST reference the same CustomerId.

### Context

Ensures identity consistency across distributed systems.

### Exceptions

None.

### Enforcement

* API validation
* Integration layer

---

## RULE-008: Order Cancellation Restrictions

### Statement

An Order MAY only be cancelled if it is not in SHIPPED or DELIVERED state.

### Context

Once physical fulfillment begins, cancellation is no longer meaningful.

### Exceptions

Force cancellation via support escalation process.

### Enforcement

* Domain logic
* Support tooling

---

## RULE-009: Monetary Integrity

### Statement

All monetary values MUST:

* have a valid currency
* never be negative (except refunds handled separately)

### Context

Prevents financial inconsistencies.

### Exceptions

Refund domain rules apply separately.

### Enforcement

* Value object validation
* API validation

---

## RULE-010: Event Immutability

### Statement

Once emitted, domain events MUST NOT be modified or deleted.

### Context

Ensures auditability and reproducibility.

### Exceptions

None (compensating events must be used instead).

### Enforcement

* Event store
* Logging system

---

# Rule Categories

## 1. Structural Rules

Define how domain entities relate.

Example:

* Order must belong to Customer

---

## 2. Lifecycle Rules

Define state transitions.

Example:

* Draft → Submitted → Confirmed

---

## 3. Integrity Rules

Ensure consistency of data.

Example:

* Order must contain at least one item

---

## 4. Temporal Rules

Define time-based constraints.

Example:

* Cannot cancel after shipment

---

## 5. Financial Rules

Define monetary correctness.

Example:

* No negative totals

---

## 6. Integration Rules

Define cross-system constraints.

Example:

* Shipment only after confirmation

---

# Rule Enforcement Layers

Each rule should specify where it is enforced:

| Layer        | Responsibility                  |
| ------------ | ------------------------------- |
| Domain Model | Core invariants                 |
| API Layer    | Input validation                |
| Database     | Structural constraints          |
| Event System | Consistency across services     |
| UI           | User feedback (not enforcement) |

---

# Traceability

Business rules must connect to:

```text id="trace_map"
VISION → SCOPE → DOMAIN MODEL → RULE → REQUIREMENT → API → IMPLEMENTATION
```

Example:

```text id="trace_example"
RULE-002
Order must contain at least one item
    ↓
REQ-101 Create Order
REQ-102 Submit Order
    ↓
API-017 POST /orders
    ↓
Order Service validation logic
    ↓
ADR-009 Event sourcing decision
```

---

# Rule Anti-Patterns

### ❌ Vague Rules

Bad:

```text id="bad_rule_1"
Orders should be valid.
```

Why it fails:
Not testable, not enforceable.

---

### ❌ Implementation Details

Bad:

```text id="bad_rule_2"
The database must use a foreign key constraint.
```

Why it fails:
That is architecture, not business logic.

---

### ❌ UI Rules

Bad:

```text id="bad_rule_3"
The button should be disabled.
```

Why it fails:
UI is a rendering concern, not a business rule.

---

# Good Rule Test

A business rule is valid if:

* It can be enforced without UI
* It can be tested automatically
* It is independent of architecture
* It remains true across all integrations
* It expresses a business constraint, not a technical choice

---

# Mental Model

Think of Business Rules as:

> The constitution of the domain

* Domain Model = geography of the system
* Business Rules = laws of that geography
* Requirements = planned actions within it
* Architecture = infrastructure used to enforce it

If a rule is unclear, inconsistently enforced, or duplicated across layers, the system will eventually drift and become unreliable.
