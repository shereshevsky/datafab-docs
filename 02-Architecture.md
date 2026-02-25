---
layout: default
title: Architecture
---

# DataFab System Architecture

**Version:** 5.0
**Last Updated:** February 2026

---

## Platform Overview

DataFab is an AI-powered data intelligence platform built on a metadata-driven architecture. The platform provides unified access to distributed data assets, intelligent automation through AI agents, and comprehensive data governance capabilities.

### Platform Components

| Component             | Purpose                                 | Key Capabilities                                                                              |
| :-------------------- | :-------------------------------------- | :-------------------------------------------------------------------------------------------- |
| Knowledge Fabric      | Data integration and intelligence layer | Persistent Knowledge Graph, Entity Resolution, 200+ MCP Connectors, Search Sessions           |
| Studio                | Creation and execution environment      | DDAs (Data-Driven Agents), Widgets, Datasets, Utilities, Chain of Agents, MCP Integrations, Operational Modes (0-4) |
| Exchange              | Data asset marketplace                  | Asset Catalog, Wallet & Blockchain (DAAC), Metering & Billing, Access Control, API Gateway    |
| Schema Management     | Business domain definition and control  | Domain Discovery, Schema Registry, Schema Validation                                          |
| AI & LLM Layer        | Intelligent processing and inference    | LightLLM Gateway, Output Consistency, Model Provenance                                        |
| Graph Operations      | Data intelligence and analytics module  | Rule Engine, Query Workflows, Analytics, Case Management                                      |
| DevOps Infrastructure | Deployment and operations               | CI/CD Pipelines, Monitoring, Security Operations                                              |

---

## Architecture Overview

```
┌─────────────────────────────────────────────────────────────────────┐
│                        PRESENTATION LAYER                           │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  ┌────────────┐   │
│  │   Web UI     │  │  API Gateway │  │   Exchange   │  │  Messaging │   │
│  │              │  │  (REST)      │  │   Interface  │  │  Mini-App  │   │
│  └──────────────┘  └──────────────┘  └──────────────┘  └────────────┘   │
│                              │                                          │
│                   [Authentication, Rate Limiting, Input Validation]     │
├─────────────────────────────────────────────────────────────────────┤
│                          APPLICATION LAYER                          │
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────────┐    │
│  │                          EXCHANGE                               │    │
│  │  ┌───────────┐  ┌───────────────┐  ┌───────────┐  ┌──────────┐  │    │
│  │  │  Catalog  │  │   Wallet &   │  │ Metering  │  │  Ledger  │  │    │
│  │  │  Service  │  │  Blockchain   │  │ & Billing │  │ Service  │  │    │
│  │  └───────────┘  └───────────────┘  └───────────┘  └──────────┘  │    │
│  └─────────────────────────────────────────────────────────────────┘    │
│                                                                         │
│  ┌─────────────────────────────────────────────────────────────────┐    │
│  │                          STUDIO                                 │    │
│  │  ┌───────────┐  ┌───────────┐  ┌───────────┐  ┌──────────────┐  │    │
│  │  │  DDA      │  │  Widgets  │  │ Datasets  │  │  Chain of    │  │    │
│  │  │  Builder  │  │ & Utilities│ │ & Media   │  │  DDAs        │  │    │
│  │  └───────────┘  └───────────┘  └───────────┘  └──────────────┘  │    │
│  └─────────────────────────────────────────────────────────────────┘    │
│                                                                         │
│  ┌─────────────────────────────────────────────────────────────────┐    │
│  │                    GRAPH OPERATIONS MODULE                      │    │
│  │  ┌───────────┐  ┌───────────────┐  ┌───────────┐  ┌──────────┐  │    │
│  │  │   Rule    │  │  Query        │  │ Analytics │  │  Case    │  │    │
│  │  │  Engine   │  │  Workflows    │  │  Service  │  │ Manager  │  │    │
│  │  └───────────┘  └───────────────┘  └───────────┘  └──────────┘  │    │
│  └─────────────────────────────────────────────────────────────────┘    │
│                                                                         │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌────────────┐ ┌────────────┐   │
│  │  Search  │ │ Lineage  │ │ Quality  │ │ Discovery  │ │ Governance │   │
│  │ Service  │ │ Service  │ │ Service  │ │  Service   │ │  Service   │   │
│  └──────────┘ └──────────┘ └──────────┘ └────────────┘ └────────────┘   │
│                              │                                          │
│                   [Service-to-Service AuthN/AuthZ, mTLS]                │
├─────────────────────────────────────────────────────────────────────┤
│                      KNOWLEDGE FABRIC LAYER                         │
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────────┐    │
│  │                    KNOWLEDGE GRAPH                              │    │
│  │  ┌──────────────┐  ┌──────────────────┐  ┌──────────────────┐   │    │
│  │  │ Entity Store │  │ Relationship     │  │  Query Engine    │   │    │
│  │  │   (Nodes)    │  │ Store (Edges)    │  │  (Traversal)     │   │    │
│  │  └──────────────┘  └──────────────────┘  └──────────────────┘   │    │
│  └─────────────────────────────────────────────────────────────────┘    │
│                                                                         │
│  ┌─────────────────────────────────────────────────────────────────┐    │
│  │                  ENTITY RESOLUTION ENGINE                       │    │
│  │  ┌───────────┐  ┌───────────┐  ┌───────────┐  ┌─────────────┐   │    │
│  │  │ Blocking  │  │ Matching  │  │ Clustering│  │ Golden      │   │    │
│  │  │ Service   │  │ Service   │  │ Service   │  │ Record Mgmt │   │    │
│  │  └───────────┘  └───────────┘  └───────────┘  └─────────────┘   │    │
│  └─────────────────────────────────────────────────────────────────┘    │
│                              │                                          │
│                   [Encryption at Rest, Access Control Lists]            │
├─────────────────────────────────────────────────────────────────────┤
│                        AI & LLM LAYER                               │
│  ┌─────────────────────────────────────────────────────────────────┐    │
│  │  ┌────────────┐  ┌──────────────┐  ┌────────────────────────┐   │    │
│  │  │  LightLLM  │  │   Provider   │  │  Prompt Management     │   │    │
│  │  │  Gateway   │  │  Abstraction │  │  & Template Engine     │   │    │
│  │  └────────────┘  └──────────────┘  └────────────────────────┘   │    │
│  └─────────────────────────────────────────────────────────────────┘    │
│                              │                                          │
│                   [Input Filtering, Output Validation, PII Detection]   │
├─────────────────────────────────────────────────────────────────────┤
│                       CONNECTIVITY LAYER                            │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  ┌────────────┐   │
│  │  Database    │  │    API       │  │     MCP      │  │   Event    │   │
│  │  Connectors  │  │  Connectors  │  │  Connectors  │  │  Streams   │   │
│  └──────────────┘  └──────────────┘  └──────────────┘  └────────────┘   │
│                              │                                          │
│               [Credential Vault, Secure Connections, Data Sampling]     │
├─────────────────────────────────────────────────────────────────────┤
│                       SOURCE SYSTEMS                                │
│  ┌──────────┐ ┌───────────┐ ┌──────────┐ ┌──────────┐ ┌──────────────┐  │
│  │Databases │ │  Document │ │  APIs    │ │  Data    │ │   External   │  │
│  │          │ │  Stores   │ │          │ │  Sources │ │   Sources    │  │
│  └──────────┘ └───────────┘ └──────────┘ └──────────┘ └──────────────┘  │
│                              │                                          │
│                [Customer-Managed, Customer Credentials]                 │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Knowledge Fabric

The Knowledge Fabric serves as the foundational data integration and intelligence layer for the DataFab platform. It implements a metadata-driven architecture that provides unified access to distributed data assets while leaving source data in place.

### Core Capabilities

| Capability                 | Description                                                                                                    |
| :------------------------- | :------------------------------------------------------------------------------------------------------------- |
| Persistent Knowledge Graph | Corporate memory with schema-bounded extraction, source provenance, and Knowledge Tree structure               |
| Entity Resolution          | Cross-source entity matching using blocking, matching, and clustering algorithms with golden record management |
| 200+ MCP Connectors        | Federated queries across databases, SaaS applications, and data systems                                        |
| Search Sessions            | Iterative exploration with session graphs and accumulated context                                              |
| Data Observability         | Quality monitoring, freshness tracking, and automated alerts                                                   |
| Discovery Service          | Automated identification and cataloging of data assets                                                         |
| Active Metadata            | Continuous metadata analysis, profiling, and enrichment                                                        |
| Data Lineage               | End-to-end tracking of data flow from source to consumption                                                    |

### Knowledge Graph Model

The Knowledge Graph stores entities as nodes and relationships as edges, enabling complex traversal queries and network analysis.

**Entity Types:**

| Entity       | Description                                         | Use Cases                          |
| :----------- | :-------------------------------------------------- | :--------------------------------- |
| Person       | Individual entities and contacts                     | Identity, risk assessment, mapping |
| Organization | Corporate entities and relationships                 | Corporate structure, analysis      |
| Asset        | Data items, resources, applications                 | Asset management, tracking         |
| Document     | Reports, data files, records                        | Document management, search        |
| Address      | Physical and registered addresses                   | Location analysis, verification    |
| Identifier   | Tax IDs, registration numbers, reference IDs        | Cross-reference, verification      |

**Relationship Types:**

| Relationship | Description |
|:-------------|:------------|
| OWNS | Ownership stake between entities |
| CONTROLS | Control relationship (voting, management) |
| RELATED_TO | Business or data relationship |
| EMPLOYS | Employment relationship |
| REFERENCES | Data or document reference |
| LOCATED_AT | Entity-address relationship |

### Entity Resolution

The Entity Resolution Engine identifies duplicate and related records across connected sources to build unified entity profiles (Golden Records).

**Resolution Pipeline:**

```
Source Records → Blocking → Candidate Pairs → Matching → Clusters → Golden Records
                    │             │              │           │
              (Key generation) (Comparison)  (Scoring)  (Merge rules)
```

---

## Studio

The Studio (Helix Studio) provides the creation and execution environment for Data-Driven Agents (DDAs), widgets, datasets, utilities, and multi-agent workflows. The platform supports five operational modes enabling organizations to balance automation with human oversight.

### Core Capabilities

| Capability | Description |
|:-----------|:------------|
| DDA Creation | Domain-driven flow with schema selection, natural language definition, query plan, and testing |
| Widgets | Visual interface components (SYSTEM and OUTPUT types) with dialog/canvas views |
| Datasets | Structured data collections with file uploads, schema enforcement, and draft/publish lifecycle |
| Utilities | Reusable components combining external APIs and DDAs with configurable placeholders |
| Business Domain Discovery | Extract schemas from uploaded documents to define entity structures |
| Chain of Agents | Orchestrate multiple DDAs with human-in-the-loop review gates |
| Graph of Agents | *(Planned)* Non-linear directed graph orchestration with branching, parallelism, and cycles |
| MCP Integrations | Managed MCP tool connections with types, instances, and credentials |
| Asset Search | Semantic search across all Studio asset types |
| AI Hybrid Planning | Automatic DDA creation from natural language descriptions |
| Operational Modes | Five modes from traditional platform (Mode 0) to fully automated with audit (Mode 4) |
| Text-to-Pipeline | Natural language pipeline generation with DSL output and iterative refinement |

### DDA Architecture

Data-Driven Agents (DDAs) are the fundamental execution unit in Studio. Each DDA has:

| Component      | Description                                                    |
| :------------- | :------------------------------------------------------------- |
| Definition     | Name, description, instructions, model, prompt                 |
| Query Plan     | Ordered items referencing datasets, MCPs, DDAs, and scripts    |
| Placeholders   | Configurable component slots (MCP, dataset, DDA) for runtime mapping |
| Runtime Config | Per-user configuration with placeholder mappings               |
| Lifecycle      | Draft/publish stages with ACTIVE/INACTIVE states               |
| Execution      | Execute with file inputs; execution history with SUCCESS/ERROR status |

### Chain of Agents / Graph of Agents

Chains enable complex workflows by orchestrating multiple DDAs with optional human review. The planned Graph of Agents capability will extend this to arbitrary directed graph topologies with conditional branching, parallel fan-out/fan-in, and cycles.

| Item Type | Description | Use Case |
|:----------|:------------|:---------|
| DDA | Execute a Data-Driven Agent step | Data processing, analysis |
| HUMAN_IN_THE_LOOP | Human review/approval gate | Quality control, compliance |

### Operational Modes

The platform supports five operational modes enabling organizations to configure automation levels:

| Mode | Name | Description |
|:-----|:-----|:------------|
| 0 | Traditional Platform | No AI agents; manual investigation and analysis |
| 1 | AI-Assisted Manual | Agents in suggest-only mode; all decisions require human approval |
| 2 | Routine Automation | Agents handle routine tasks; humans focus on analysis and decisions |
| 3 | Autonomous with Escalation | Full automation with escalation on exceptions |
| 4 | Fully Automated with Audit | End-to-end automation with post-investigation human audits |

---

## Exchange

The Exchange component serves as the platform's data asset marketplace, enabling organizations to publish, discover, acquire, and monetize data assets with blockchain-backed transactions and transparent revenue sharing.

### Core Capabilities

| Capability | Description |
|:-----------|:------------|
| Asset Catalog | Publish, search, and manage data assets (agents, widgets, datasets, models, utilities, media, chains) |
| User Profiles | Consumer, provider, and dual-role profiles with verification |
| Wallet & Blockchain | DAAC token on Ethereum for purchases, deposits, withdrawals, and transfers |
| Metering & Billing | Usage tracking with configurable policies and automated billing |
| Access Control | Resource-level permission policies (READ, WRITE, DELETE, ADMIN) |
| API Gateway | Managed endpoints (REST, GraphQL, Webhook, Proxy) with request logging |
| Ledger & Revenue | Double-entry accounting with revenue allocation, settlement, and reconciliation |

### Asset Types

| Asset Type | Description |
|:-----------|:------------|
| BEHAVIOUR_DATA | Behavioral analytics and pattern datasets |
| AGENT | Executable AI agents built in Studio |
| WIDGET | Visual interface components |
| UTILITY | Reusable processing functions and tools |
| MEDIA | Media files and content assets |
| MODEL | Machine learning models |
| DATASET | Structured data collections |
| CHAIN | Multi-agent workflow chains |

### Marketplace Model

| Component | Description |
|:----------|:------------|
| Catalog Service | Asset registration, search, publish lifecycle (DRAFT → PUBLISHED → ARCHIVED) |
| Wallet Service | DAAC/ETH digital wallets with deposit, withdrawal, and transfer operations |
| Metering Service | Usage event capture, billing generation, pricing plan enforcement |
| Access Service | Per-asset permission policies with least-privilege enforcement |
| Gateway Service | Managed API endpoints with rate limiting and request logging |
| Ledger Service | Double-entry financial records with settlement and reconciliation |

---

## Schema Management

The Schema Management system provides a unified approach to defining, discovering, and managing business domain schemas across the platform.

### Core Capabilities

| Capability | Description |
|:-----------|:------------|
| Business Domain Discovery | Extract domain concepts from user documents |
| Schema Registry | Centralized storage with versioning and access control |
| Schema Validation | Ensure data conformance across all platform components |
| Schema Binding | Link schemas to agents, extractors, and MCP connectors |

### Schema Usage Across Platform

| Component | Schema Role |
|:----------|:------------|
| Studio Agents | Input/output validation, data transformation control |
| Data Extractors | Structure external data according to domain model |
| MCP Connectors | Ensure data consistency across tool integrations |
| Knowledge Graph | Entity and relationship type definitions |
| Pipelines | Data flow validation between processing steps |

### Document-to-Schema Discovery

| Stage | Description |
|:------|:------------|
| Document Analysis | Extract text, structure, and metadata from user documents |
| Concept Extraction | Identify entities, attributes, and relationships |
| Schema Generation | Create structured schema definitions |
| User Refinement | Interactive review and modification |
| Publication | Register schema in central registry |

---

## AI & LLM Layer

The AI & LLM Layer provides intelligent processing capabilities through a provider-agnostic gateway with comprehensive output consistency and quality controls.

### Core Capabilities

| Capability | Description |
|:-----------|:------------|
| LightLLM Gateway | Unified interface for multiple LLM providers |
| Output Consistency | Schema-validated extraction and ontology-based execution |
| Model Provenance | Complete tracking of model versions and configurations |
| A/B Testing | Controlled model updates with performance comparison |
| Quality Assurance | Feedback loops, accuracy monitoring, reasoning chain transparency |
| Provider Abstraction | Swap providers without code changes |
| Prompt Management | Template library with version control |

### LLM Output Consistency

| Control | Description |
|:--------|:------------|
| Schema-Validated Extraction | All outputs validated against user-defined schemas |
| Ontology-Based Execution | Responses grounded in domain ontology |
| Reasoning Chain Transparency | Full reasoning paths logged for audit |
| Deterministic Components | Separation of deterministic vs. probabilistic processing |

### Provider Support

| Provider Type | Examples | Integration |
|:--------------|:---------|:------------|
| Commercial APIs | OpenAI, Anthropic, Google | API key authentication |
| Self-Hosted | Llama, Mistral, custom models | Private endpoint |
| Enterprise | Azure OpenAI, AWS Bedrock | Cloud provider auth |

---

## Graph Operations Module

The Graph Operations module provides comprehensive capabilities for data intelligence, analytics, and case management.

### Core Capabilities

| Capability | Description |
|:-----------|:------------|
| Rule Engine | Data scoring and decision rules |
| Query Workflows | Complex query orchestration and workflows |
| Analytics Service | Analytics and reporting capabilities |
| Case Management | Data case tracking and documentation |
| Reporting | Analytics, insights, and dashboards |

### Rule Engine

The Rule Engine calculates scores based on configurable factors:

| Factor Category | Examples |
|:----------------|:---------|
| Data Quality | Completeness, uniqueness, validity metrics |
| Relationship | Entity relationships, connection strength |
| Temporal | Data freshness, change patterns |
| Behavioral | Access patterns, usage anomalies |

---

## Network Architecture

### Network Segmentation

| Zone | Purpose | Components |
|:-----|:--------|:-----------|
| Edge/DMZ | External entry point | Load balancers, WAF, API Gateway |
| Application | Service execution | Studio, Services, AI Layer |
| Data | Persistent storage | Knowledge Graph, Document Store |
| Management | Operations | Monitoring, Logging, Admin tools |

### Connectivity Patterns

| Pattern | Description | Use Case |
|:--------|:------------|:---------|
| Direct TLS | Encrypted connection over internet | Cloud-hosted sources |
| VPN Tunnel | Site-to-site encrypted tunnel | On-premises sources |
| Private Link | Cloud provider private connectivity | Same-cloud sources |
| Agent-Based | Customer-deployed agent connects outbound | Air-gapped environments |

---

## Data Flow Model

DataFab operates on a metadata-first principle. Source data remains in place while metadata flows through the platform.

| Data Type | Handling | Storage |
|:----------|:---------|:--------|
| Structural Metadata | Extracted and stored | Knowledge Graph |
| Statistical Profiles | Computed via aggregation | Knowledge Graph |
| Sample Data | Optional, user-controlled | Ephemeral cache |
| Query Results | Pass-through federation | Never persisted |
| Source Credentials | Encrypted storage | Secure Vault |

---

## Security Architecture

### Defense-in-Depth Model

```
┌─────────────────────────────────────────────────────────────────────┐
│                    PERIMETER SECURITY                               │
│    DDoS Protection │ WAF │ Rate Limiting │ Geographic Filtering     │
├─────────────────────────────────────────────────────────────────────┤
│                    NETWORK SECURITY                                 │
│    VPC Isolation │ Network Segmentation │ Private Endpoints         │
├─────────────────────────────────────────────────────────────────────┤
│                    APPLICATION SECURITY                             │
│    Input Validation │ Output Encoding │ CSRF Protection │ CSP       │
├─────────────────────────────────────────────────────────────────────┤
│                    IDENTITY & ACCESS                                │
│    OAuth 2.0/OIDC │ RBAC │ ABAC │ MFA │ Session Management          │
├─────────────────────────────────────────────────────────────────────┤
│                    DATA SECURITY                                    │
│    Encryption │ Tokenization │ Data Masking │ Classification        │
├─────────────────────────────────────────────────────────────────────┤
│                    INFRASTRUCTURE SECURITY                          │
│    Hardened Images │ Patch Management │ Container Security          │
└─────────────────────────────────────────────────────────────────────┘
```

### Cryptographic Standards

| Purpose | Algorithm | Key Length |
|:--------|:----------|:-----------|
| Data at Rest | AES-256-GCM | 256-bit |
| Data in Transit | TLS 1.3 | 256-bit |
| Key Encryption | RSA-OAEP | 2048-bit minimum |
| Digital Signatures | ECDSA | P-256 |
| Hashing | SHA-256 | N/A |

---

## Integration Points

### External System Integration

| System Type          | Integration Method       | Data Exchange                       |
| :------------------- | :----------------------- | :---------------------------------- |
| Data Systems         | API / Database connector | Data models, metadata              |
| CRM Systems          | API / Webhook            | Contacts, organizations, activities |
| Document Management  | API / File system        | Documents, metadata                 |
| Analytics Systems    | API / Database           | Reports, dashboards, metrics        |
| External Data        | API                      | Third-party data sources            |
| Monitoring Providers | API                      | System health, alerts               |

### MCP Protocol

The Model Context Protocol (MCP) provides a standardized interface for tool integration:

| Component | Purpose |
|:----------|:--------|
| Tool Registry | Catalog of available tools and capabilities |
| Schema Definition | Input/output contracts for each tool |
| Authentication | Tool-specific credential management |
| Execution | Secure tool invocation with timeout handling |

---

## Deployment Models

DataFab is available in multiple deployment configurations to meet varying security, compliance, and operational requirements.

### Deployment Options

| Model | Description | Use Case |
|:------|:------------|:---------|
| SaaS Multi-Tenant | Shared infrastructure, isolated data | Standard deployment, cost-effective |
| Dedicated Cloud Tenant | Dedicated infrastructure in DataFab cloud | Enterprise, enhanced isolation |
| Customer Cloud | Deploy in customer's cloud tenant (AWS, Azure, GCP) | Data sovereignty, infrastructure control |
| On-Premises | Fully customer-managed within data centers | Maximum control, air-gapped environments |
| Hybrid | SaaS control plane, on-premises data plane | Balance of convenience and control |

### SaaS Multi-Tenant

| Aspect | Details |
|:-------|:--------|
| Infrastructure | Shared compute, isolated data stores |
| Data Isolation | Logical tenant isolation with encryption |
| Compliance | SOC 2, GDPR compliant infrastructure |
| Updates | Automatic platform updates |
| Best For | Standard requirements, rapid deployment |

### Dedicated Cloud Tenant

| Aspect | Details |
|:-------|:--------|
| Infrastructure | Dedicated resources within DataFab cloud |
| Data Isolation | Physical separation of compute and storage |
| Compliance | Enhanced compliance posture |
| Updates | Coordinated update windows |
| Best For | Enterprise customers requiring dedicated resources |

### Customer Cloud Deployment

| Aspect | Details |
|:-------|:--------|
| Infrastructure | Customer's own cloud tenant (AWS, Azure, GCP) |
| Data Control | Customer maintains full infrastructure control |
| Region Selection | Deploy in preferred cloud region |
| Management | DataFab manages application, customer manages infrastructure |
| Best For | Data sovereignty, existing cloud investments |

### On-Premises Deployment

| Aspect | Details |
|:-------|:--------|
| Infrastructure | Customer data centers |
| Data Control | Complete data custody |
| Network | Air-gapped capability available |
| Management | Customer-managed with DataFab support |
| Best For | Strict regulatory requirements, maximum control |

### Data Residency Configuration

| Region Option | Data Location | LLM Processing |
|:--------------|:--------------|:---------------|
| UK-Only | UK data centers | UK-based providers or on-premises |
| EU-Only | EU data centers (Ireland common) | EU-based providers |
| US-Only | US data centers | US-based providers |
| Customer-Specified | Any supported region | Region-aligned providers |
| On-Premises | Customer data centers | Self-hosted models |

### LLM Provider Configuration by Deployment

| Deployment | LLM Options |
|:-----------|:------------|
| SaaS | Cloud providers (OpenAI, Anthropic, Google) |
| Dedicated Tenant | Cloud providers with dedicated keys |
| Customer Cloud | Cloud providers or self-hosted in customer cloud |
| On-Premises | Self-hosted models (Llama, Mistral) for complete data control |
| Hybrid | Cloud for non-sensitive, on-premises for sensitive |

### Deployment Feature Comparison

| Feature                            | SaaS    | Dedicated | Customer Cloud | On-Premises |
| :--------------------------------- | :------ | :-------- | :------------- | :---------- |
| Knowledge Fabric                   | ✓       | ✓         | ✓              | ✓           |
| Studio (Agents, Widgets, Datasets) | ✓       | ✓         | ✓              | ✓           |
| Exchange Interface                 | ✓       | ✓         | ✓              | ✓           |
| Multi-Tenancy                      | ✓       | ✓         | ✓              | ✓           |
| LLM Integration                    | ✓       | ✓         | ✓              | ✓           |
| Custom Region                      | Limited | ✓         | ✓              | N/A         |
| Self-Hosted LLMs                   | ✗       | ✗         | ✓              | ✓           |

---

*For detailed information see individual component documents: Knowledge Fabric, Studio, Exchange, AI-LLM, Graph Operations, and API Security.*
