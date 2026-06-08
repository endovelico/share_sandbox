A good way to operationalize your documentation model is to define:

1. **Ownership (RACI-style responsibility matrix)**
2. **Review responsibilities**
3. **Role-specific checklists before a document is considered complete**

---

# Documentation Responsibility Matrix

### Roles

| Role | Description                      |
| ---- | -------------------------------- |
| PO   | Product Owner                    |
| BA   | Business Analyst / Domain Expert |
| ARCH | Solution / Enterprise Architect  |
| DEV  | Development Team                 |
| QA   | Quality Assurance                |
| OPS  | Operations / SRE                 |
| SEC  | Security / Compliance            |
| TL   | Technical Lead                   |

### Legend

| Code | Meaning                         |
| ---- | ------------------------------- |
| A    | Accountable (owns outcome)      |
| R    | Responsible (creates/maintains) |
| C    | Consulted                       |
| I    | Informed                        |

---

## 01 Business Context

| Artifact     | PO | BA | ARCH | TL | DEV | QA | OPS |
| ------------ | -- | -- | ---- | -- | --- | -- | --- |
| Vision       | A  | R  | C    | I  | I   | I  | I   |
| Scope        | A  | R  | C    | I  | I   | I  | I   |
| Stakeholders | A  | R  | C    | I  | I   | I  | I   |

---

## 02 Domain

| Artifact       | PO | BA  | ARCH | TL | DEV | QA | OPS |
| -------------- | -- | --- | ---- | -- | --- | -- | --- |
| Glossary       | A  | R   | C    | C  | C   | C  | I   |
| Domain Model   | C  | A/R | C    | C  | C   | C  | I   |
| Business Rules | A  | R   | C    | C  | C   | C  | I   |
| Context Maps   | C  | C   | A/R  | C  | C   | I  | C   |

---

## 03 Requirements

| Artifact            | PO | BA | ARCH | TL | DEV | QA | OPS |
| ------------------- | -- | -- | ---- | -- | --- | -- | --- |
| Use Cases           | A  | R  | C    | C  | I   | C  | I   |
| User Stories        | A  | R  | I    | C  | C   | C  | I   |
| Acceptance Criteria | A  | R  | I    | C  | C   | R  | I   |
| NFRs                | A  | C  | R    | C  | C   | C  | C   |

---

## 04 Architecture

| Artifact      | PO | BA | ARCH | TL | DEV | QA | OPS |
| ------------- | -- | -- | ---- | -- | --- | -- | --- |
| C4 Context    | C  | C  | A/R  | C  | I   | I  | I   |
| C4 Containers | I  | I  | A    | R  | C   | I  | C   |
| C4 Components | I  | I  | C    | A  | R   | I  | I   |
| ADRs          | I  | I  | A    | R  | C   | I  | C   |

---

## 05 API

| Artifact           | PO | BA | ARCH | TL | DEV | QA | OPS |
| ------------------ | -- | -- | ---- | -- | --- | -- | --- |
| OpenAPI Specs      | I  | C  | C    | A  | R   | C  | I   |
| API Standards      | I  | I  | A    | R  | C   | C  | I   |
| Integration Guides | I  | C  | A    | C  | R   | C  | C   |

---

## 06 Development

| Artifact           | PO | BA | ARCH | TL | DEV | QA | OPS |
| ------------------ | -- | -- | ---- | -- | --- | -- | --- |
| Local Setup        | I  | I  | I    | A  | R   | C  | C   |
| Coding Standards   | I  | I  | C    | A  | R   | C  | I   |
| Migration Strategy | I  | I  | C    | A  | R   | C  | C   |

---

## 07 Operations

| Artifact          | PO | BA | ARCH | TL | DEV | QA | OPS |
| ----------------- | -- | -- | ---- | -- | --- | -- | --- |
| Deployment        | I  | I  | C    | C  | R   | C  | A   |
| Monitoring        | I  | I  | C    | C  | R   | C  | A   |
| Runbooks          | I  | I  | C    | C  | C   | C  | A/R |
| Incident Recovery | I  | I  | C    | C  | C   | C  | A/R |

---

## 08 User Guides

| Artifact  | PO | BA | ARCH | TL | DEV | QA | OPS |
| --------- | -- | -- | ---- | -- | --- | -- | --- |
| Tutorials | A  | R  | I    | I  | C   | C  | I   |
| FAQ       | A  | R  | I    | I  | C   | C  | C   |

---

# Documentation Workflow

```text
PO/BA
  ↓
Domain Validation
  ↓
Requirements Definition
  ↓
Architecture Design
  ↓
API Definition
  ↓
Implementation
  ↓
Testing
  ↓
Operations Readiness
  ↓
User Documentation
```

Each phase must reference the previous phase.

---

# Product Owner Checklist

## Business Context

### Vision

* [ ] Problem statement documented
* [ ] Target users identified
* [ ] Success metrics defined
* [ ] Strategic goals documented

### Scope

* [ ] In-scope items listed
* [ ] Out-of-scope items listed
* [ ] Assumptions documented
* [ ] Constraints documented

### Requirements

* [ ] Every story links to business value
* [ ] Every story has acceptance criteria
* [ ] Every story references domain concepts
* [ ] Priorities defined
* [ ] Dependencies identified

### Traceability

* [ ] Vision → Features mapped
* [ ] Features → Stories mapped
* [ ] Stories → Releases mapped

---

# Business Analyst / Domain Expert Checklist

## Domain

### Glossary

* [ ] Terms uniquely defined
* [ ] No conflicting terminology
* [ ] Terms align with business language

### Domain Model

* [ ] Entities identified
* [ ] Relationships documented
* [ ] Lifecycle states documented

### Business Rules

* [ ] Every rule uniquely identified
* [ ] Rule source documented
* [ ] Rule owner identified
* [ ] Rule linked to requirements

### Context Maps

* [ ] Upstream systems identified
* [ ] Downstream systems identified
* [ ] Integration ownership defined

---

# Architect Checklist

## Architecture

### C4 Context

* [ ] Actors identified
* [ ] External systems identified
* [ ] Trust boundaries documented

### C4 Containers

* [ ] Deployable units identified
* [ ] Communication paths documented
* [ ] Technology choices justified

### ADRs

* [ ] Decision documented
* [ ] Alternatives evaluated
* [ ] Trade-offs captured
* [ ] Consequences documented

### Traceability

* [ ] Requirement linked to architecture
* [ ] Architecture linked to ADRs
* [ ] Architecture linked to APIs

---

# Technical Lead Checklist

## Solution Governance

* [ ] Ownership defined per component
* [ ] Coding standards approved
* [ ] Layering rules enforced
* [ ] Dependency rules documented
* [ ] Technical debt tracked

### Design Reviews

* [ ] Architecture reviewed
* [ ] API reviewed
* [ ] Security reviewed
* [ ] Operational impact reviewed

---

# Developer Checklist

## API

* [ ] Endpoint documented
* [ ] Request schemas documented
* [ ] Response schemas documented
* [ ] Error responses documented

## Development

### Local Setup

* [ ] Fresh machine installation tested
* [ ] Environment variables documented
* [ ] Bootstrap steps verified

### Code Alignment

* [ ] Code matches domain model
* [ ] Business rules implemented
* [ ] ADR constraints respected
* [ ] Naming follows glossary

### Database

* [ ] Migration documented
* [ ] Rollback strategy defined
* [ ] Backward compatibility validated

### Traceability

* [ ] Story linked to implementation
* [ ] API linked to story
* [ ] Monitoring added for feature

---

# QA Checklist

## Requirements Validation

* [ ] Acceptance criteria testable
* [ ] Test scenarios documented
* [ ] Edge cases identified

## Functional Testing

* [ ] User stories covered
* [ ] Business rules validated
* [ ] API contracts verified

## Non-Functional Testing

* [ ] Performance tested
* [ ] Security validated
* [ ] Reliability validated
* [ ] Observability verified

### Release Readiness

* [ ] Regression tests passed
* [ ] Critical defects resolved
* [ ] Documentation reviewed

---

# Operations / SRE Checklist

## Deployment

* [ ] Deployment procedure documented
* [ ] Rollback procedure tested
* [ ] Feature flags documented

## Monitoring

* [ ] Metrics defined
* [ ] Dashboards created
* [ ] Alerts configured
* [ ] Alert ownership defined

## Runbooks

* [ ] Incident procedures documented
* [ ] Recovery steps validated
* [ ] Escalation paths documented

## Production Readiness

* [ ] Capacity evaluated
* [ ] Backup strategy validated
* [ ] Recovery strategy validated

---

# Security / Compliance Checklist

## Security Review

* [ ] Authentication documented
* [ ] Authorization documented
* [ ] Sensitive data classified
* [ ] Encryption requirements documented

## Compliance

* [ ] Regulatory requirements identified
* [ ] Audit trail requirements documented
* [ ] Retention policies documented

## Operational Security

* [ ] Security monitoring defined
* [ ] Incident response process documented
* [ ] Security runbooks available

---

# Global Documentation Exit Criteria

Before any feature is considered "Done":

* [ ] Business objective exists
* [ ] Domain concepts defined
* [ ] Business rules documented
* [ ] User stories approved
* [ ] Acceptance criteria approved
* [ ] Architecture updated
* [ ] ADRs updated (if applicable)
* [ ] API documented
* [ ] Local setup still valid
* [ ] Migration documented
* [ ] Monitoring defined
* [ ] Runbooks updated
* [ ] User guide updated
* [ ] Traceability chain complete

```text
Vision
  ↓
Business Rule
  ↓
Requirement
  ↓
Architecture
  ↓
API
  ↓
Implementation
  ↓
Deployment
  ↓
Monitoring
  ↓
Runbook
```

If any link in this chain is missing, the documentation is incomplete.
