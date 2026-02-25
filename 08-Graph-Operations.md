---
layout: default
title: Graph Operations
---

# DataFab Graph Operations

**Version:** 4.2
**Last Updated:** January 2026

---

## Component Overview

The Graph Operations module provides comprehensive capabilities for entity analysis, pattern detection, and operational decision-making. It leverages the Knowledge Fabric's graph-based entity resolution and the Studio's workflow capabilities to deliver an integrated operational intelligence solution.

**Core Capabilities:**

| Capability | Description | Security Relevance |
|:-----------|:------------|:-------------------|
| Knowledge Graph Integration | Entity resolution and relationship mapping | Data integrity, access control |
| Rule Engine | Pattern scoring and operational decision rules | Rule versioning, audit trail |
| Graph Workflows | Multi-step operational process orchestration | Process authorization, escalation |
| External Enrichment | Data enrichment and third-party integration | Source validation, provenance |
| Graph Screening | Entity screening against external sources | Match verification, false positive handling |
| Case Management | Operational case tracking and documentation | Evidence chain, retention |

---

## Architecture Overview

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    GRAPH OPERATIONS ARCHITECTURE                        │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  ┌────────────────────────────────────────────────────────────────────┐ │
│  │                    OPERATIONS INTERFACE                            │ │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────────────────┐  │ │
│  │  │  Case Queue  │  │  Dashboards  │  │  Reporting & Analytics   │  │ │
│  │  └──────────────┘  └──────────────┘  └──────────────────────────┘  │ │
│  └────────────────────────────────────────────────────────────────────┘ │
│                              │                                          │
│  ┌────────────────────────────────────────────────────────────────────┐ │
│  │                    OPERATIONS ENGINE                               │ │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌───────────┐  │ │
│  │  │  Rule       │  │  Graph      │  │  Screening  │  │   Case    │  │ │
│  │  │  Engine     │  │  Workflows  │  │  Service    │  │  Manager  │  │ │
│  │  └─────────────┘  └─────────────┘  └─────────────┘  └───────────┘  │ │
│  └────────────────────────────────────────────────────────────────────┘ │
│                              │                                          │
│  ┌────────────────────────────────────────────────────────────────────┐ │
│  │                    KNOWLEDGE FABRIC INTEGRATION                    │ │
│  │  ┌─────────────────┐  ┌─────────────────┐  ┌────────────────────┐  │ │
│  │  │ Knowledge Graph │  │ Entity          │  │ External Source    │  │ │
│  │  │ (Entities &     │  │ Resolution      │  │ Integration        │  │ │
│  │  │  Relationships) │  │                 │  │                    │  │ │
│  │  └─────────────────┘  └─────────────────┘  └────────────────────┘  │ │
│  └────────────────────────────────────────────────────────────────────┘ │
│                              │                                          │
│  ┌────────────────────────────────────────────────────────────────────┐ │
│  │                    CUSTOMER SYSTEM CONNECTIONS                     │ │
│  │  Business Systems │ CRM │ Analytics │ Data Management              │ │
│  └────────────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## Knowledge Graph for Operations

The Knowledge Fabric's graph database provides the foundation for operational intelligence, enabling entity resolution, relationship mapping, and pattern analysis across connected data sources.

### Operational Entity Model

| Entity Type | Description | Operational Relevance |
|:------------|:------------|:----------------------|
| Entity | Core business entities (persons, organizations) | Analysis subject, pattern detection |
| Relationship | Connections between entities | Network analysis, anomaly detection |
| Case | Investigation or analysis record | Case management, audit trail |
| Assessment | Calculated analytical profile | Pattern scoring, decision support |
| Detection | Pattern or anomaly detection result | Alert management |
| Document | Evidence and supporting materials | Documentation, compliance |

### Operational Relationship Types

| Relationship | Description | Operations Use |
|:-------------|:------------|:----------------|
| OWNS | Ownership or control stake | Structure analysis |
| CONTROLS | Administrative control | Authority mapping |
| RELATED_TO | Personal/business relationship | Network analysis |
| HAS_CASE | Entity linked to operational case | Case tracking |
| HAS_DETECTION | Entity linked to detection result | Alert management |
| HAS_ASSESSMENT | Entity linked to analytical profile | Risk monitoring |

### Entity Resolution for Operations

The Entity Resolution Engine identifies duplicate and related records across customer systems to build a unified view of each entity.

**Resolution Security Controls:**

| Control | Implementation |
|:--------|:---------------|
| Match Decision Audit | All match decisions logged with reasoning |
| Human Review Queue | Uncertain matches routed for manual review |
| Source Attribution | Every attribute linked to source system |
| Confidence Scoring | Match confidence visible for review |
| Merge History | Complete history of entity merges preserved |

### Graph Queries for Operations

| Query Type | Purpose | Security Control |
|:-----------|:--------|:-----------------|
| Relationship Traversal | Identify connected entities through relationship chains | Traversal depth limits |
| Network Analysis | Map entity relationships and patterns | Result filtering by permission |
| Pattern Matching | Detect suspicious or significant relationship patterns | Query audit logging |
| Assessment Aggregation | Calculate network-level analysis scores | Authorized users only |

---

## Rule Engine

![Rule Engine](./images/Pasted%20image%2020260128181311.png)
The Rule Engine enables administrators to define, version, and execute business rules for pattern detection, operational scoring, and decision workflows.

### Rule Engine Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                    RULE ENGINE ARCHITECTURE                         │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ┌──────────────────────────────────────────────────────────--──┐   │
│  │                    RULE DEFINITION LAYER                     │   │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐           │   │
│  │  │  Rule       │  │  Condition  │  │  Action     │           │   │
│  │  │  Builder    │  │  Editor     │  │  Designer   │           │   │
│  │  └─────────────┘  └─────────────┘  └─────────────┘           │   │
│  └───────────────────────────────────────────────────────────-──┘   │
│                              │                                      │
│  ┌────────────────────────────────────────────────────────────-─┐   │
│  │                    RULE EXECUTION ENGINE                     │   │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐           │   │
│  │  │  Evaluation │  │  Scoring    │  │  Action     │           │   │
│  │  │  Engine     │  │  Engine     │  │  Executor   │           │   │
│  │  └─────────────┘  └─────────────┘  └─────────────┘           │   │
│  └────────────────────────────────────────────────────────────-─┘   │
│                              │                                      │
│  ┌─────────────────────────────────────────────────────────────-┐   │
│  │                    GOVERNANCE LAYER                          │   │
│  │  • Version Control   • Approval Workflow   • Audit Trail     │   │
│  └────────────────────────────────────────────────────────────-─┘   │
└─────────────────────────────────────────────────────────────────────┘
```

### Rule Types

| Rule Type | Purpose | Example Use Case |
|:----------|:--------|:-----------------|
| Pattern Scoring | Calculate numeric pattern scores | Entity assessment |
| Anomaly Detection | Classify deviations from expected patterns | Unusual activity detection |
| Classification | Assign categories based on conditions | Entity categorization |
| Threshold | Trigger actions when values exceed limits | Alert generation |
| Routing | Direct workflow based on conditions | Escalation to analysts |
| Validation | Verify data meets requirements | Input data validation |

### Rule Definition Security

| Control | Implementation |
|:--------|:---------------|
| Role-Based Editing | Only authorized roles can create/modify rules |
| Version Control | All rule changes versioned with full history |
| Approval Workflow | Rule changes require approval before activation |
| Testing Required | Rules must pass test suite before deployment |
| Rollback Support | Previous versions can be restored instantly |

### Pattern Scoring Rules

Pattern scoring rules calculate numeric scores based on configurable factors and weights.

**Scoring Components:**

| Component         | Description                              | Security Control               |
| :---------------- | :--------------------------------------- | :----------------------------- |
| Factor Definition | Pattern factors with categories and weights | Admin-only modification        |
| Score Calculation | Weighted aggregation of factors          | Audit trail on calculations    |
| Threshold Mapping | Score ranges mapped to analysis levels   | Configurable per policy        |
| Override Handling | Manual score adjustments                 | Requires justification, logged |

**Pattern Factor Categories:**

| Category        | Examples                       | Typical Weight Range |
| :-------------- | :----------------------------- | :------------------- |
| Entity Type     | Organization type, sector      | 0-30 points          |
| Geography       | Country, jurisdiction          | 0-25 points          |
| Relationship    | Connection depth, multiplicity | 0-20 points          |
| Activity        | Transaction patterns, velocity | 0-20 points          |
| History         | Past alerts, issues            | 0-15 points          |
| Behavioral      | Deviation from baseline        | 0-20 points          |

**Assessment Level Mapping:**

| Assessment Level | Score Range | Review Frequency | Expected Actions |
|:-----------------|:------------|:-----------------|:-----------------|
| Low | 0-25 | 36 months | Routine monitoring |
| Medium | 26-50 | 24 months | Standard review |
| High | 51-75 | 12 months | Enhanced analysis |
| Critical | 76-100 | 6 months | Immediate review |

### Rule Versioning

| Control | Description |
|:--------|:------------|
| Immutable Versions | Published versions cannot be modified |
| Version History | Complete history of all changes preserved |
| Change Attribution | Every change linked to user and timestamp |
| Comparison View | Side-by-side comparison of versions |
| Audit Export | Version history exportable for compliance |

### Rule Execution Security

| Control | Implementation |
|:--------|:---------------|
| Execution Isolation | Rules execute in sandboxed environment |
| Input Validation | All inputs validated against schema |
| Output Verification | Results validated before action execution |
| Timeout Enforcement | Maximum execution time enforced |
| Resource Limits | Memory and CPU limits on rule execution |

### Rule Audit Trail

| Event | Logged Data | Retention |
|:------|:------------|:----------|
| Rule Created | Rule definition, creator, timestamp | 2 years |
| Rule Modified | Changes, modifier, justification | 2 years |
| Rule Activated | Version, approver, effective date | 2 years |
| Rule Executed | Input hash, score, actions triggered | 1 year |
| Rule Overridden | Override value, justification, approver | 2 years |

---

## Graph Workflows

![Graph Workflows](./images/Pasted%20image%2020260128181324.png)

The Graph Workflow system orchestrates multi-step operational processes with human tasks, automated actions, and control mechanisms.

### Graph Workflow Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                    GRAPH WORKFLOW ARCHITECTURE                      │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ┌────────────────────────────────────────────────────────-─────┐   │
│  │                    PROCESS DEFINITION                        │   │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐           │   │
│  │  │  Process    │  │  Task       │  │  Gateway    │           │   │
│  │  │  Designer   │  │  Library    │  │  Config     │           │   │
│  │  └─────────────┘  └─────────────┘  └─────────────┘           │   │
│  └────────────────────────────────────────────────────────────-─┘   │
│                              │                                      │
│  ┌───────────────────────────────────────────────────────────-──┐   │
│  │                    EXECUTION ENGINE                          │   │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐           │   │
│  │  │  Process    │  │  Task       │  │  Event      │           │   │
│  │  │  Runtime    │  │  Manager    │  │  Handler    │           │   │
│  │  └─────────────┘  └─────────────┘  └─────────────┘           │   │
│  └──────────────────────────────────────────────────────────-───┘   │
│                              │                                      │
│  ┌───────────────────────────────────────────────────────────-──┐   │
│  │                    INTEGRATION LAYER                         │   │
│  │  • Knowledge Graph   • Rule Engine   • Notification Service  │   │
│  └────────────────────────────────────────────────────────────-─┘   │
└─────────────────────────────────────────────────────────────────────┘
```

### Operational Process Types

| Process Type | Purpose | Trigger |
|:-------------|:--------|:--------|
| Entity Onboarding | Initial entity analysis workflow | Entity creation |
| Periodic Assessment | Scheduled re-analysis | Timer, score change |
| Alert Investigation | Event-driven analysis | Detection, manual referral |
| Pattern Analysis | Deep pattern investigation | High-risk detection |
| Escalation | Management review process | Risk threshold, policy |

### Pattern-Based Workflow Triggering

The Rule Engine integrates with Graph Workflows to automatically trigger appropriate workflows based on pattern detection.

**Workflow Trigger Flow:**

```
┌─────────────────────────────────────────────────────────────────────┐
│                    PATTERN-BASED WORKFLOW TRIGGERING                │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  Entity Event ──▶ [Pattern Detection] ──▶ [Rule Evaluation]         │
│       │                  │                      │                   │
│       ▼                  ▼                      ▼                   │
│  (New entity,        (Score calculated)     (Rules matched)        │
│   data change,                                  │                   │
│   alert)                                        ▼                   │
│                                     [Workflow Selection]            │
│                                           │                         │
│              ┌────────────────────────────┼────────────────┐        │
│              ▼                            ▼                ▼        │
│         [Low Risk]                  [Medium Risk]    [High Risk]    │
│              │                            │                │        │
│              ▼                            ▼                ▼        │
│       Standard Review                Extended Review   Critical    │
│        Workflow                       Workflow        Review        │
│              │                            │            Workflow    │
│              └────────────────────────────┼────────────────┘        │
│                                           ▼                         │
│                                    [Task Assignment]                │
│                                           │                         │
│                                           ▼                         │
│                                    [Process Execution]              │
│                                           │                         │
│                                           ▼                         │
│                                     [Audit Trail]                   │
└─────────────────────────────────────────────────────────────────────┘
```

### Workflow Task Types

| Task Type | Description | Security Control |
|:----------|:------------|:-----------------|
| User Task | Human action required | Role-based assignment |
| Service Task | Automated system action | Permission validation |
| Script Task | Custom logic execution | Sandboxed execution |
| Send Task | External communication | Message logging |
| Receive Task | Wait for external event | Event validation |

### Workflow Security Controls

| Control | Implementation |
|:--------|:---------------|
| Process Authorization | Only authorized users can start processes |
| Task Assignment | Tasks assigned based on role and workload |
| Escalation Rules | Automatic escalation on SLA breach |
| Delegation Controls | Delegation requires approval, logged |
| Completion Verification | Task completion validated before proceeding |

### Workflow Definition Security

| Control | Description |
|:--------|:------------|
| Version Control | Process definitions versioned |
| Change Approval | Process changes require multi-party approval |
| Testing Required | Processes must pass simulation before deployment |
| Rollback Support | Previous versions can be restored |
| Access Restrictions | Process definition access role-based |

### Task Assignment Security

| Control | Implementation |
|:--------|:---------------|
| Role-Based Assignment | Tasks assigned to roles, not individuals |
| Workload Balancing | Even distribution across team members |
| Conflict Avoidance | Prevent assignment to conflicted parties |
| Audit Trail | All assignments and reassignments logged |
| SLA Monitoring | Task completion tracked against SLA |

### Escalation Controls

| Trigger | Action | Security Control |
|:--------|:-------|:-----------------|
| SLA Breach | Escalate to supervisor | Automatic, logged |
| Risk Threshold | Escalate to management | Rule-based, audited |
| Manual Request | Escalate per request | Requires justification |
| Timeout | Reassign or escalate | Configurable per task |

### Process Instance Security

| Control | Description |
|:--------|:------------|
| Instance Isolation | Each process instance isolated |
| Data Encryption | Process data encrypted at rest |
| Access Control | Instance access based on role and assignment |
| State Protection | State transitions validated and logged |
| Cancellation Control | Cancellation requires authorization |

---

## External Source Integration

The Graph Operations module integrates with external data sources for entity verification and enrichment.

### External Source Categories

| Category | Examples | Data Types |
|:---------|:---------|:-----------|
| Corporate Registries | Corporate filings, registration records | Incorporation, officers, filings |
| Relationship Data | Business databases, industry databases | Connections, associations |
| Public Records | News, legal records | Public information, history |
| Regulatory Data | Regulatory databases | Compliance records |
| Industry Data | Industry-specific data | Sector information |

### Source Integration Security

| Control | Implementation |
|:--------|:---------------|
| Source Validation | Only approved sources in registry |
| Credential Isolation | Per-source credential management |
| Rate Limiting | Respect source API limits |
| Data Minimization | Retrieve only required fields |
| Caching Policy | Time-limited caching per source |
| Provenance Tracking | Full lineage from source to graph |

### Enrichment Workflow

| Stage | Description | Security Control |
|:------|:------------|:-----------------|
| Request | Entity submitted for enrichment | Authorization check |
| Matching | Entity matched against external source | Matching rules applied |
| Retrieval | Data fetched from external source | Encrypted transport |
| Fusion | External data merged with existing | Conflict resolution rules |
| Validation | Enriched data validated | Schema validation |
| Storage | Enriched entity persisted | Access control inherited |
| Audit | Enrichment event logged | Full audit trail |

---

## Graph Screening Service

The Graph Screening Service performs entity screening against external sources.

### Screening Types

| Screening Type | Sources | Frequency |
|:---------------|:--------|:----------|
| Database Screening | Business databases, registries | Real-time, periodic batch |
| Regulatory Screening | Regulatory databases | On-demand, periodic |
| Public Records Screening | News and public records | Continuous monitoring |

### Screening Security Controls

| Control | Implementation |
|:--------|:---------------|
| Match Verification | Potential matches require human review |
| False Positive Management | Documented false positive decisions |
| Alert Escalation | True matches escalated per policy |
| Screening Audit | All screening activity logged |
| Source Update Tracking | Source list versions tracked |

---

## Case Management

Operational cases track analyses, investigations, and decision records.

### Case Types

| Case Type | Purpose | Lifecycle |
|:----------|:--------|:----------|
| Initial Analysis | Entity onboarding analysis | Open → Review → Concluded |
| Deep Investigation | Detailed pattern investigation | Triggered → Analyze → Escalate/Close |
| Pattern Review | Systematic pattern assessment | Open → Review → Documented |
| Management Review | Senior review and approval | Prepared → Review → Approved/Rejected |

### Case Security Controls

| Control | Implementation |
|:--------|:---------------|
| Access Control | Case access based on role and assignment |
| Evidence Chain | All documents and notes timestamped |
| Decision Audit | All decisions logged with justification |
| Retention Policy | Cases retained per operational requirement |
| Export Controls | Case export requires authorization |

---

## User Roles and Permissions

### Operations-Specific Roles

| Role | Description | Permissions |
|:-----|:------------|:------------|
| Analyst | Day-to-day operational analysis work | Case work, screening review, standard analysis |
| Senior Analyst | Senior operations staff | Case approval, pattern override, team management |
| Operations Manager | Operations leadership | Escalation approval, full case access |
| Data Coordinator | Intake and coordination | Create cases, basic screening, escalate |
| Auditor | Internal/external auditor | View all cases, run reports, no edit |

### Permission Matrix

| Action | Analyst | Senior | Manager | Coordinator | Auditor |
|:-------|:--------|:--------|:--------|:-----------|:--------|
| Create Case | ✓ | ✓ | ✓ | ✓ | ✗ |
| Review Case | ✓ | ✓ | ✓ | ✗ | ✓ |
| Approve Case | ✗ | ✓ | ✓ | ✗ | ✗ |
| Override Assessment | ✗ | ✓ | ✓ | ✗ | ✗ |
| Escalate Case | ✗ | ✓ | ✓ | ✗ | ✗ |
| Modify Rules | ✗ | ✓ | ✓ | ✗ | ✗ |
| View Reports | ✓ | ✓ | ✓ | ✗ | ✓ |

---

## Audit Logging

### Operations-Specific Events

| Event Category | Logged Data | Retention |
|:---------------|:------------|:----------|
| Case Created | Case ID, entity, creator, type | 3 years |
| Case Decision | Case ID, decision, approver, justification | 3 years |
| Pattern Detection | Entity, score, factors, detector | 3 years |
| Screening Performed | Entity, sources, matches, reviewer | 3 years |
| Rule Executed | Rule ID, inputs, score, actions | 1 year |
| Process Executed | Process ID, tasks, outcomes | 1 year |
| Escalation | Case ID, escalation reason, recipient | 3 years |

### Operational Retention

| Category | Retention Period | Data Types |
|:---------|:-----------------|:-----------|
| Active Case Data | Duration + 1 year | Analysis records, decisions |
| Closed Cases | 3 years minimum | Complete case files |
| Audit Records | 3 years | All system activity |
| Rule Changes | Indefinite | Rule versions and history |

---

## Reporting and Analytics

### Operations Dashboards

| Dashboard | Purpose | Access |
|:----------|:--------|:-------|
| Case Queue | Active cases and assignments | All operations roles |
| Pattern Overview | Entity pattern distribution | Manager |
| SLA Monitoring | Task completion against targets | Manager |
| Screening Alerts | Pending screening matches | Analyst, Manager |
| Operations Dashboard | Management information metrics | Manager |

### Report Security

| Control | Implementation |
|:--------|:---------------|
| Role-Based Access | Reports filtered by user permissions |
| Data Aggregation | Individual data protected in summaries |
| Export Logging | All report exports logged |
| Scheduled Reports | Automated reports require authorization |

---
