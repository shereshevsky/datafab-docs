---
layout: default
title: Studio
---

# DataFab Studio

**Version:** 6.0
**Last Updated:** February 2026

---

## Component Overview

The Studio (Helix Studio) serves as the development environment for the DataFab platform, enabling users to build Data-Driven Agents (DDAs), design workflows, and orchestrate multi-agent solutions for data intelligence use cases. The platform supports five operational modes that enable organizations to balance automation with human oversight, tailored to their policies and use cases.

**Core Capabilities:**

| Capability                | Description                                                            |
| :------------------------ | :--------------------------------------------------------------------- |
| Business Domain Discovery | Extract schemas from uploaded documents                                |
| Domain Management         | Organize schemas, datasets, DDAs, and chains within business domains   |
| DDA Creation              | Build Data-Driven Agents with natural language definition and testing  |
| Widget Types              | Define visual interface components (system and output widgets)         |
| Dataset Management        | Define and manage structured data collections with file uploads        |
| Utilities                 | Build reusable components combining external APIs and DDAs             |
| Chain of Agents             | Orchestrate multiple DDAs with human-in-the-loop support               |
| Graph of Agents             | *(Planned)* Non-linear graph orchestration with branching and cycles   |
| MCP Integrations          | Connect to external tools via MCP protocol with credential management  |
| External APIs             | Configure and manage external API endpoint connections                  |
| Asset Search              | Semantic search across all Studio asset types                          |
| AI Hybrid Planning        | Create DDAs from natural language descriptions automatically           |
| AI Workflow Execution     | Execute DDA workflows with query-based invocation                      |
| Operational Modes         | Five modes from traditional platform (Mode 0) to fully automated (Mode 4) |

**Asset Types:**

| Asset Type    | API Identifier  | Description                                    |
| :------------ | :-------------- | :--------------------------------------------- |
| DDA           | `DDA`           | Data-Driven Agent with schema-bound processing |
| Chain of Agents | `CHAIN_OF_DDA`  | Multi-DDA orchestration workflow                |
| Dataset       | `DATASET`       | Structured data collection with file uploads   |
| Widget        | `WIDGET`        | Visual interface component                     |
| Utility       | `UTILITY`       | Reusable component combining APIs and DDAs     |
| Schema        | `SCHEMA`        | Business domain schema definition              |
| MCP Integration | `MCP_INTEGRATION` | External tool connection via MCP protocol   |
| Media Asset   | `MEDIA_ASSET`   | Media files with content URLs and policies     |
| Model Asset   | `MODEL_ASSET`   | Machine learning model files                   |

**Lifecycle Stages:**

| Stage     | Description                                           |
| :-------- | :---------------------------------------------------- |
| DRAFT     | Asset under development; editable, not yet published  |
| PUBLISHED | Asset published and available for use                 |

**Asset States:**

| State    | Description                   |
| :------- | :---------------------------- |
| ACTIVE   | Asset is operational          |
| INACTIVE | Asset is disabled             |

---

## Architecture Overview

```
┌─────────────────────────────────────────────────────────────────────────┐
│                           API GATEWAY LAYER                             │
│  ┌─────────────────────────────────────────────────────────────────┐    │
│  │  Authentication │ Rate Limiting │ Request Routing │ Health Check│    │
│  └─────────────────────────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────────────────────┘
            │
            ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                          STUDIO CORE SERVICES                           │
│                                                                         │
│  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐          │
│  │  DDA Service    │  │Domain & Schema  │  │  Widget Type    │          │
│  │  (Agents)       │  │  Services       │  │  Service        │          │
│  └─────────────────┘  └─────────────────┘  └─────────────────┘          │
│                                                                         │
│  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐          │
│  │  Dataset        │  │  Utility        │  │  Chain of Agents│          │
│  │  Service        │  │  Service        │  │  Service        │          │
│  └─────────────────┘  └─────────────────┘  └─────────────────┘          │
│                                                                         │
│  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐          │
│  │  MCP Integration│  │  External API   │  │  Script         │          │
│  │  Service        │  │  Service        │  │  Service        │          │
│  └─────────────────┘  └─────────────────┘  └─────────────────┘          │
│                                                                         │
│  ┌─────────────────────────────────────────────────────────────────┐    │
│  │                    EXECUTION ENGINE                             │    │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌─────────┐ │    │
│  │  │  Sandbox    │  │  Resource   │  │ Credential  │  │  State  │ │    │
│  │  │  Runtime    │  │  Manager    │  │   Vault     │  │ Manager │ │    │
│  │  └─────────────┘  └─────────────┘  └─────────────┘  └─────────┘ │    │
│  └─────────────────────────────────────────────────────────────────┘    │
│                                                                         │
│  ┌─────────────────────────────────────────────────────────────────┐    │
│  │                  ASSET MANAGEMENT LAYER                         │    │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌─────────┐ │    │
│  │  │  Unified    │  │  Asset      │  │  Media &    │  │Sources  │ │    │
│  │  │  Assets     │  │  Search     │  │  Model Mgmt │  │ Router  │ │    │
│  │  └─────────────┘  └─────────────┘  └─────────────┘  └─────────┘ │    │
│  └─────────────────────────────────────────────────────────────────┘    │
│                                                                         │
│  ┌─────────────────────────────────────────────────────────────────┐    │
│  │                  AI PLANNING & ORCHESTRATION                    │    │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌─────────┐ │    │
│  │  │  AI Hybrid  │  │  Workflow   │  │   Error     │  │Recovery │ │    │
│  │  │  Planner    │  │  Executor   │  │  Handler    │  │ Manager │ │    │
│  │  └─────────────┘  └─────────────┘  └─────────────┘  └─────────┘ │    │
│  └─────────────────────────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────────────────────┘
            │
            ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                         PLATFORM INTEGRATION                            │
│  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐          │
│  │ Knowledge Fabric│  │   AI & LLM      │  │    Audit        │          │
│  │  (Data Sources) │  │   Services      │  │   Services      │          │
│  └─────────────────┘  └─────────────────┘  └─────────────────┘          │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## Business Domains

Business Domains serve as the organizational structure for grouping related schemas, datasets, DDAs, and Chains of DDAs. Each domain represents a business area and contains the entity definitions that control data processing.

### Domain Management

| Operation | Description                                            |
| :-------- | :----------------------------------------------------- |
| Create    | Define a new business domain with name and description |
| List      | View all accessible domains with related entity counts |
| Update    | Modify domain name, description, or metadata           |
| Delete    | Remove a domain and its associations                   |

**Domain Relationships:**

| Related Entity | Description                                    |
| :------------- | :--------------------------------------------- |
| Schemas        | Entity definitions assigned to the domain      |
| Datasets       | Data collections associated with the domain    |
| DDAs           | Data-Driven Agents operating within the domain |
| Chains of DDAs | Multi-DDA workflows within the domain          |

### Domain Discovery

The Domain Discovery feature enables users to define their business domain by uploading documents, from which the system extracts relevant schemas automatically.

**Extraction Process:**

| Stage               | Description                                      |
| :------------------ | :----------------------------------------------- |
| Document Upload     | User provides business documents via file upload  |
| Content Analysis    | AI extracts text, structure, tables from documents |
| Concept Extraction  | Entities, attributes, relationships discovered   |
| Schema Generation   | Structured schemas created from extracted concepts |
| User Review         | Interactive refinement of generated schemas       |
| Domain Assignment   | Schemas assigned to target business domain        |

**Supported Document Types:**

| Document Type       | Extraction Focus                  |
| :------------------ | :-------------------------------- |
| Data Specifications | Data models, field definitions    |
| Policies            | Workflows, rules, roles           |
| Data Dictionaries   | Field definitions, types          |
| Forms & Templates   | Input fields, validations         |
| Business Documents  | Domain concepts, relationships    |

---

## Schemas

Schemas define the entity structures used by DDAs, datasets, and other Studio assets for data processing and validation.

### Schema Management

| Operation | Description                                              |
| :-------- | :------------------------------------------------------- |
| Create    | Define a new schema with name, JSON definition, domain   |
| List      | View all accessible schemas, filter by domain            |
| Update    | Modify schema definition, name, or thumbnail             |
| Delete    | Remove a schema                                          |

**Schema Structure:**

| Field      | Description                                    |
| :--------- | :--------------------------------------------- |
| Name       | Schema identifier                              |
| Definition | JSON schema defining entity structure and rules |
| Thumbnail  | Visual preview of the schema                   |
| Domain     | Associated business domain                     |

### Schema-Driven Processing

DDAs use bound schemas to control their data processing behavior.

| Binding Type      | Purpose                                        |
| :---------------- | :--------------------------------------------- |
| Input Schema      | Validates incoming data structure              |
| Output Schema     | Ensures output conforms to expected format     |
| Internal Schema   | Controls intermediate data transformations     |
| Validation Schema | Enforces business rules on processed data      |

**Schema Enforcement:**

| Control              | Implementation                                |
| :------------------- | :-------------------------------------------- |
| Type Validation      | Data types checked against schema definitions |
| Constraint Enforcement | Required fields, ranges, formats validated   |
| Reference Validation | Entity references verified against schema     |
| Schema Version Binding | DDAs pinned to specific schema versions      |

For detailed schema management capabilities, see [09-Schema-Management](09-Schema-Management.md).

---

## Data-Driven Agents (DDAs)

Data-Driven Agents (DDAs) are the fundamental execution unit in Studio. Each DDA combines a language model with a structured query plan to perform schema-bounded data processing tasks.

### DDA Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                    DDA STRUCTURE                                  │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐    │
│  │  DEFINITION                                             │    │
│  │  Name │ Description │ Instructions │ Model │ Prompt     │    │
│  └─────────────────────────────────────────────────────────┘    │
│                          │                                      │
│                          ▼                                      │
│  ┌─────────────────────────────────────────────────────────┐    │
│  │  QUERY PLAN                                             │    │
│  │  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐    │    │
│  │  │ DATASET  │ │   MCP    │ │   DDA    │ │  SCRIPT  │    │    │
│  │  │  Items   │ │  Items   │ │  Items   │ │  Items   │    │    │
│  │  └──────────┘ └──────────┘ └──────────┘ └──────────┘    │    │
│  └─────────────────────────────────────────────────────────┘    │
│                          │                                      │
│                          ▼                                      │
│  ┌─────────────────────────────────────────────────────────┐    │
│  │  PLACEHOLDERS & RUNTIME CONFIG                          │    │
│  │  Configurable component slots with per-user mappings    │    │
│  └─────────────────────────────────────────────────────────┘    │
│                          │                                      │
│                          ▼                                      │
│  ┌───────────────┐  ┌────────────┐  ┌────────────────────┐      │
│  │  Draft/Publish │  │  Execute   │  │  Execution History │      │
│  │  Lifecycle     │  │  with Files│  │  Tracking          │      │
│  └───────────────┘  └────────────┘  └────────────────────┘      │
└─────────────────────────────────────────────────────────────────┘
```

### DDA Definition

| Field        | Description                                            |
| :----------- | :----------------------------------------------------- |
| Name         | Agent identifier                                       |
| Description  | Purpose and capabilities                               |
| Instructions | Natural language behavioral guidelines                 |
| Model        | LLM model configuration for inference                  |
| Prompt       | System prompt template for the agent                   |
| Domain       | Associated business domain                             |
| Thumbnail    | Visual preview                                         |
| Stage        | Lifecycle stage (DRAFT or PUBLISHED)                   |
| State        | Operational state (ACTIVE or INACTIVE)                 |
| Type         | DDA type indicator (DDA or CHAIN)                      |

### Query Plan

The Query Plan defines the data sources and processing steps a DDA uses during execution. Each plan consists of ordered items that specify where data comes from and how it is processed.

**Query Plan Item Types:**

| Item Type | Description                                             |
| :-------- | :------------------------------------------------------ |
| DATASET   | Reference to a Studio dataset as a data source          |
| MCP       | Reference to an MCP integration tool                    |
| DDA       | Reference to another DDA for sub-agent execution        |
| SCRIPT    | Reference to a code script for custom processing        |

### Placeholders

Placeholders define configurable component slots within a DDA that can be mapped to specific resources at runtime.

| Placeholder Type | Description                                     |
| :--------------- | :---------------------------------------------- |
| MCP_INTEGRATION  | Slot for an MCP tool connection                 |
| DATASET          | Slot for a dataset reference                    |
| DDA              | Slot for a sub-agent reference                  |

**Placeholder Configuration:**

| Field        | Description                                    |
| :----------- | :--------------------------------------------- |
| Name         | Placeholder identifier                         |
| Type         | Component type (MCP_INTEGRATION, DATASET, DDA) |
| Description  | Purpose of the placeholder                     |
| Required     | Whether the placeholder must be mapped          |
| Default      | Default resource mapping (if any)              |

### Runtime Configuration

Runtime Config provides per-user customization of DDA behavior by mapping placeholders to specific resources.

| Field              | Description                                        |
| :----------------- | :------------------------------------------------- |
| Placeholder Mappings | Map each placeholder to a specific resource       |
| State              | Configuration state (ACTIVE or INACTIVE)           |
| User Scope         | Configuration applies per authenticated user       |

### DDA Lifecycle

| Operation    | Description                                            |
| :----------- | :----------------------------------------------------- |
| Create       | Define DDA with name, description, model, prompt       |
| Draft        | Save DDA configuration as draft for iteration          |
| Apply Draft  | Apply draft changes to the DDA definition              |
| Update       | Modify DDA properties, plan, or placeholders           |
| Publish      | Set stage from DRAFT to PUBLISHED                      |
| Execute      | Run DDA with optional file inputs                      |
| Executions   | View execution history with status tracking            |
| Delete       | Remove DDA                                             |

**Execution Status:**

| Status  | Description                     |
| :------ | :------------------------------ |
| SUCCESS | Execution completed successfully |
| ERROR   | Execution failed with error     |

### DDA Creation Flow

```
┌─────────────────────────────────────────────────────────────────────────┐
│                       DDA CREATION WORKFLOW                              │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  ┌─────────────────┐                                                    │
│  │  1. User        │  User initiates DDA creation                       │
│  │  Request        │  "Create new Data-Driven Agent"                    │
│  └────────┬────────┘                                                    │
│           │                                                             │
│           ▼                                                             │
│  ┌─────────────────────────────────────────────────────────────┐        │
│  │  2. Domain Selection                                        │        │
│  │  ┌─────────────────────┐   ┌─────────────────────────────┐  │        │
│  │  │  Select Existing    │   │  Create New Domain          │  │        │
│  │  │  Business Domain    │   │  via Domain Discovery       │  │        │
│  │  │  (entity schemas)   │   │  (upload documents)         │  │        │
│  │  └─────────────────────┘   └─────────────────────────────┘  │        │
│  └────────────────────────────────┬────────────────────────────┘        │
│                                   │                                     │
│                                   ▼                                     │
│  ┌─────────────────────────────────────────────────────────────┐        │
│  │  3. Schema Review & Modification                            │        │
│  │  • View generated/selected domain schemas                   │        │
│  │  • Add, modify, or remove entity definitions                │        │
│  │  • Configure attribute types and constraints                │        │
│  │  • Define relationships between entities                    │        │
│  └────────────────────────────────┬────────────────────────────┘        │
│                                   │                                     │
│                                   ▼                                     │
│  ┌─────────────────────────────────────────────────────────────┐        │
│  │  4. DDA Definition                                          │        │
│  │  • Name: Agent identifier                                   │        │
│  │  • Description: Purpose and capabilities                    │        │
│  │  • Instructions: Behavioral guidelines in plain language    │        │
│  │  • Model: LLM model selection                               │        │
│  │  • Prompt: System prompt template                           │        │
│  │  • Query Plan: Data sources (datasets, MCPs, DDAs, scripts) │        │
│  │  • Placeholders: Configurable component slots               │        │
│  └────────────────────────────────┬────────────────────────────┘        │
│                                   │                                     │
│                                   ▼                                     │
│  ┌─────────────────────────────────────────────────────────────┐        │
│  │  5. Draft & Testing                                         │        │
│  │  • Save as DRAFT stage                                      │        │
│  │  • Interactive testing interface                            │        │
│  │  • Execute with sample files                                │        │
│  │  • Output validation against schema                         │        │
│  │  • Apply draft when satisfied                               │        │
│  └────────────────────────────────┬────────────────────────────┘        │
│                                   │                                     │
│                                   ▼                                     │
│  ┌─────────────────────────────────────────────────────────────┐        │
│  │  6. Publication                                             │        │
│  │  • Set stage to PUBLISHED                                   │        │
│  │  • Configure runtime placeholders                           │        │
│  │  • Set access permissions                                   │        │
│  │  • Make available to other platform users                   │        │
│  └─────────────────────────────────────────────────────────────┘        │
└─────────────────────────────────────────────────────────────────────────┘
```

### DDA Execution Security

```
┌─────────────────────────────────────────────────────────────────┐
│                    DDA EXECUTION SECURITY                         │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  User Request ──▶ [Authentication] ──▶ [Authorization]          │
│                          │                   │                  │
│                          ▼                   ▼                  │
│                   (Identity verified)  (DDA access check)       │
│                              │                                  │
│                              ▼                                  │
│  ┌─────────────────────────────────────────────────────────┐    │
│  │              EXECUTION SANDBOX                          │    │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐      │    │
│  │  │  Process    │  │  Network    │  │  Resource   │      │    │
│  │  │  Isolation  │  │  Isolation  │  │  Limits     │      │    │
│  │  └─────────────┘  └─────────────┘  └─────────────┘      │    │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐      │    │
│  │  │  Filesystem │  │  Capability │  │  Time       │      │    │
│  │  │  Isolation  │  │  Restrict   │  │  Limits     │      │    │
│  │  └─────────────┘  └─────────────┘  └─────────────┘      │    │
│  └─────────────────────────────────────────────────────────┘    │
│                              │                                  │
│                              ▼                                  │
│  Request ──▶ [Tool Authorization] ──▶ [Parameter Validation]    │
│                          │                       │              │
│                          ▼                       ▼              │
│                         (Checks)        (Input sanitization)    │
│                              │                                  │
│                              ▼                                  │
│                       [Audit Logging]                           │
└─────────────────────────────────────────────────────────────────┘
```

### Execution Sandbox

All DDA execution occurs within isolated sandboxes.

**Sandbox Features:**

| Feature              | Implementation             | Purpose                   |
| :------------------- | :------------------------- | :------------------------ |
| Process Isolation    | Container with gVisor      | Prevent host access       |
| Filesystem Isolation | Overlay FS, read-only root | Prevent persistence       |
| Time Limits          | Process timeout            | Prevent runaway execution |

**Resource Constraints:**

| Constraint     | Limit                         | Purpose                     |
| :------------- | :---------------------------- | :-------------------------- |
| Execution Time | Configurable (default 60s)    | Prevent resource exhaustion |
| Memory         | Configurable (default 512 MB) | Prevent memory exhaustion   |
| Network        | Allowlisted endpoints only    | Prevent data exfiltration   |
| File System    | No persistent access          | Prevent local attacks       |
| Tool Calls     | Configurable per execution    | Prevent infinite loops      |
| LLM Calls      | Configurable per execution    | Cost control                |

---

## Widget Types

Widget Types define visual interface components that enable users to interact with DDA capabilities through graphical displays and interactive controls.

### Widget Type Classification

| Type   | API Value | Description                                    |
| :----- | :-------- | :--------------------------------------------- |
| System | `SYSTEM`  | Platform-provided built-in widget types         |
| Output | `OUTPUT`  | User-defined widgets for DDA output display     |

### Widget View Types

| View Type | Description                                            |
| :-------- | :----------------------------------------------------- |
| dialog    | Widget renders in a dialog/modal overlay               |
| canvas    | Widget renders on the main canvas area                 |
| both      | Widget can render in either dialog or canvas context   |

### Widget Type Structure

| Field        | Description                                    |
| :----------- | :--------------------------------------------- |
| Name         | Widget type identifier                         |
| Type         | SYSTEM or OUTPUT                               |
| View Type    | dialog, canvas, or both                        |
| Data Schemas | Schema definitions for widget data binding     |
| Thumbnail    | Visual preview of the widget type              |

### Widget Type Management

| Operation | Description                                         |
| :-------- | :-------------------------------------------------- |
| Create    | Define a new widget type with schemas and view type |
| List      | View all available widget types                     |
| Update    | Modify widget type configuration or schemas         |
| Delete    | Remove a widget type                                |

### Widget Security Controls

| Control               | Implementation                                     |
| :-------------------- | :------------------------------------------------- |
| Schema Validation     | Widget data validated against bound data schemas   |
| Access Control        | Widget access governed by DDA permissions          |
| Output Filtering      | Widget output limited to authorized data           |
| Audit Logging         | All widget interactions logged                     |

---

## Datasets

Datasets enable users to define, manage, and share structured data collections that DDAs and widgets can access for processing and analysis. Datasets support file uploads and follow a draft/publish lifecycle.

### Dataset Architecture

```
┌─────────────────────────────────────────────────────────────────────────┐
│                        DATASET ARCHITECTURE                             │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  ┌─────────────────────────────────────────────────────────┐            │
│  │                    DATASET DEFINITION                   │            │
│  │  ┌───────────────┐  ┌───────────────┐  ┌──────────────┐ │            │
│  │  │  Schema       │  │  File         │  │  Runtime     │ │            │
│  │  │  Binding      │  │  Mapping      │  │  Config      │ │            │
│  │  └───────────────┘  └───────────────┘  └──────────────┘ │            │
│  └─────────────────────────────────────────────────────────┘            │
│                                │                                        │
│                                ▼                                        │
│  ┌─────────────────────────────────────────────────────────┐            │
│  │                    DATA SOURCES                         │            │
│  │  ┌─────────┐         ┌─────────┐        ┌────────────┐  │            │
│  │  │Knowledge│         │ Uploaded│        │ MCP        │  │            │
│  │  │ Fabric  │         │  Files  │        │ Sources    │  │            │
│  │  └─────────┘         └─────────┘        └────────────┘  │            │
│  └─────────────────────────────────────────────────────────┘            │
│                                │                                        │
│                                ▼                                        │
│  ┌─────────────────────────────────────────────────────────┐            │
│  │                    CONSUMERS                            │            │
│  │  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌────────────┐  │            │
│  │  │  DDAs   │  │ Widgets │  │Utilities│  │  Chains    │  │            │
│  │  └─────────┘  └─────────┘  └─────────┘  └────────────┘  │            │
│  └─────────────────────────────────────────────────────────┘            │
└─────────────────────────────────────────────────────────────────────────┘
```

### Dataset Structure

| Field          | Description                                        |
| :------------- | :------------------------------------------------- |
| Name           | Dataset identifier                                 |
| Description    | Purpose and contents description                   |
| Files          | Uploaded data files                                |
| File Mapping   | Column/field mappings from files to schema         |
| Schemas        | Bound schemas for data validation                  |
| Domain         | Associated business domain                         |
| Stage          | Lifecycle stage (DRAFT or PUBLISHED)               |
| State          | Operational state (ACTIVE or INACTIVE)             |
| Runtime Config | Per-user configuration with placeholder mappings   |

### Dataset Lifecycle

| Operation   | Description                                         |
| :---------- | :-------------------------------------------------- |
| Create      | Define dataset with name, description, domain       |
| Upload Files | Add data files to the dataset                      |
| Map Fields  | Configure file-to-schema field mappings             |
| Draft       | Save dataset configuration as draft                 |
| Apply Draft | Apply draft changes to the dataset definition       |
| Bind Schema | Associate schemas for data validation               |
| Configure   | Set runtime configuration and placeholder mappings  |
| Publish     | Set stage from DRAFT to PUBLISHED                   |
| Delete      | Remove dataset                                      |

### Dataset Security Controls

| Control               | Implementation                                |
| :-------------------- | :-------------------------------------------- |
| Schema Enforcement    | All data validated against defined schema     |
| Access Control        | Role-based and user-based dataset permissions |
| Source Authentication | Secure credentials for external data sources  |
| File Validation       | Uploaded files scanned and validated          |
| Audit Logging         | All dataset access and modifications logged   |
| Version Control       | Dataset definition changes tracked            |

### Dataset Access Patterns

| Pattern      | Description                       | Security                   |
| :----------- | :-------------------------------- | :------------------------- |
| Direct Query | DDAs query dataset directly       | Permission check per query |
| Subscription | Use real-time version of the data | Subscription authorization |
| Snapshot     | Point-in-time copy of dataset     | Immutable, audited access  |

---

## Utilities

Utilities are reusable components that combine external API endpoints and DDAs into configurable processing units. They provide a way to compose complex operations from existing building blocks.

### Utility Structure

| Field          | Description                                           |
| :------------- | :---------------------------------------------------- |
| Name           | Utility identifier                                    |
| Description    | Purpose and capabilities                              |
| API Mapping    | Reference to an external API configuration            |
| DDA References | References to DDAs used by the utility                |
| Placeholders   | Configurable component slots (API or DDA type)        |
| Runtime Config | Per-user configuration with placeholder mappings      |
| Stage          | Lifecycle stage (DRAFT or PUBLISHED)                  |
| State          | Operational state (ACTIVE or INACTIVE)                |

### Utility Placeholder Types

| Type | Description                                    |
| :--- | :--------------------------------------------- |
| API  | Slot for an external API endpoint configuration |
| DDA  | Slot for a Data-Driven Agent reference          |

### Utility Lifecycle

| Operation    | Description                                         |
| :----------- | :-------------------------------------------------- |
| Create       | Define utility with name, API mapping, DDA references |
| Draft        | Save utility configuration as draft                 |
| Apply Draft  | Apply draft changes to the utility definition       |
| Configure    | Set runtime configuration and placeholder mappings  |
| Execute      | Run the utility with provided parameters            |
| Delete       | Remove utility                                      |

### Utility Security Controls

| Control             | Implementation                                    |
| :------------------ | :------------------------------------------------ |
| API Authorization   | External API calls authorized per user permissions |
| DDA Authorization   | Referenced DDAs authorized per user permissions    |
| Input Validation    | All parameters validated against schemas           |
| Audit Logging       | All utility executions logged                      |

---

## Chain of Agents

The Chain of Agents feature enables composition of complex data workflows from multiple coordinated Data-Driven Agents with optional human-in-the-loop review steps.

### Chain Query Plan

Chains use a specialized query plan that supports DDA execution steps and human review gates.

**Chain Query Plan Item Types:**

| Item Type          | Description                                          |
| :----------------- | :--------------------------------------------------- |
| DDA                | Execute a Data-Driven Agent within the chain         |
| HUMAN_IN_THE_LOOP  | Insert a human review/approval gate in the workflow  |

### Chain Structure

| Field          | Description                                           |
| :------------- | :---------------------------------------------------- |
| Name           | Chain identifier                                      |
| Description    | Purpose and workflow description                      |
| Query Plan     | Ordered list of DDA and HUMAN_IN_THE_LOOP items       |
| Domain         | Associated business domain                            |
| Runtime Config | Per-user configuration with placeholder mappings      |
| Stage          | Lifecycle stage (DRAFT or PUBLISHED)                  |
| State          | Operational state (ACTIVE or INACTIVE)                |

### Chain Lifecycle

| Operation      | Description                                           |
| :------------- | :---------------------------------------------------- |
| Create         | Define chain with name, description, query plan       |
| Draft          | Save chain configuration as draft                     |
| Apply Draft    | Apply draft changes to the chain definition           |
| Configure      | Set runtime configuration and placeholder mappings    |
| Execute        | Run chain with optional file inputs                   |
| Executions     | View execution history with status tracking           |
| Delete         | Remove chain                                          |

### Communication Patterns

```
┌─────────────────────────────────────────────────────────────────┐
│                    CHAIN EXECUTION PATTERNS                      │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  SEQUENTIAL WITH HUMAN GATE                                      │
│  ┌─────┐ ┌─────┐ ┌──────────┐ ┌─────┐ ┌─────┐                   │
│  │DDA A│→│DDA B│→│  HUMAN   │→│DDA C│→│DDA D│                   │
│  └─────┘ └─────┘ │  REVIEW  │ └─────┘ └─────┘                   │
│                  └──────────┘                                   │
│                                                                 │
│  BRANCHING                     HIERARCHICAL                      │
│  ┌─────┐                       ┌─────┐                           │
│  │DDA A│                       │DDA A│                           │
│  └──┬──┘                       └──┬──┘                           │
│     │                        ┌────┴────┐                         │
│  ┌──┼──────┐                 ▼         ▼                         │
│  ▼  ▼      ▼              ┌─────┐  ┌─────┐                       │
│ ┌──┐┌──┐┌──────────┐      │DDA B│  │DDA C│                       │
│ │B ││C ││  HUMAN   │      └──┬──┘  └──┬──┘                       │
│ └┬─┘└┬─┘│  REVIEW  │         ▼         ▼                         │
│  │   │  └──────────┘      ┌─────┐  ┌─────┐                       │
│  └───┼──────┘             │DDA D│  │DDA E│                       │
│      ▼                    └─────┘  └─────┘                       │
│   ┌─────┐                                                        │
│   │DDA E│                                                        │
│   └─────┘                                                        │
└─────────────────────────────────────────────────────────────────┘
```

### Multi-Agent Security Controls

| Control                  | Implementation                                    |
| :----------------------- | :------------------------------------------------ |
| Message Authentication   | All inter-DDA messages signed                     |
| Context Isolation        | Each DDA has isolated execution context            |
| Permission Propagation   | Downstream DDAs cannot exceed upstream permissions |
| Human Gate Enforcement   | HUMAN_IN_THE_LOOP items block until approved       |
| Audit Trail              | Complete chain of execution logged                 |
| Message TTL              | Messages expire to prevent replay attacks          |

### Orchestration Security

| Pattern          | Security Control                         |
| :--------------- | :--------------------------------------- |
| Sequential       | Each step authorized independently       |
| Parallel         | Concurrent executions isolated           |
| Hierarchical     | Parent DDA controls child permissions    |
| Human-in-the-Loop | Execution pauses pending human approval |

### State Management Security

| State Type       | Storage       | Security Controls                |
| :--------------- | :------------ | :------------------------------- |
| Execution State  | In-memory     | Encrypted, execution-scoped      |
| Checkpoint State | Persistent    | Encrypted, tamper-evident        |
| Workflow Context | Distributed   | Encrypted, access-controlled     |

### Error Handling and Recovery

**Error Classification:**

| Error Type  | Example                        | Strategy                    |
| :---------- | :----------------------------- | :-------------------------- |
| Transient   | Network timeout, rate limit    | Retry with backoff          |
| Permanent   | Invalid input, missing resource | Fail fast, notify          |
| Partial     | Some items failed in batch     | Continue with failures logged |
| Resource    | Memory exceeded, timeout       | Scale up or abort           |
| Dependency  | Upstream DDA failed            | Circuit breaker, fallback   |

**Recovery Controls:**

| Control         | Implementation                              |
| :-------------- | :------------------------------------------ |
| Retry Policy    | Configurable max attempts, backoff          |
| Circuit Breaker | Automatic failover on repeated failures     |
| Fallback DDAs   | Alternative execution paths                 |
| Notifications   | Configurable alerting on failures           |

---

## Graph of Agents

> **Status: Planned** — Graph of Agents is the next-generation orchestration capability, extending the linear Chain of Agents model into a full directed graph topology.

The Graph of Agents feature will enable composition of complex, non-linear workflows where multiple DDAs can be connected in arbitrary directed graph patterns — including conditional branching, parallel fan-out/fan-in, cycles with exit conditions, and dynamic routing based on intermediate results.

### Graph vs. Chain Comparison

| Capability              | Chain of Agents               | Graph of Agents                       |
| :---------------------- | :---------------------------- | :------------------------------------ |
| Topology                | Linear sequence               | Arbitrary directed graph              |
| Branching               | Limited (sequential only)     | Full conditional branching            |
| Parallelism             | Sequential with human gates   | Native parallel fan-out/fan-in        |
| Cycles                  | Not supported                 | Supported with exit conditions        |
| Dynamic Routing         | Fixed execution order         | Runtime-determined paths              |
| Human-in-the-Loop       | Gate between steps            | Gate at any node in the graph         |
| Convergence             | Single output                 | Multiple convergence points           |

### Planned Graph Structure

```
┌─────────────────────────────────────────────────────────────────┐
│                    GRAPH OF AGENTS TOPOLOGY                     │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌─────┐       ┌─────┐                                          │
│  │DDA A│──────▶│DDA B│──────────┐                               │
│  └─────┘       └──┬──┘          │                               │
│                   │             ▼                               │
│                   │          ┌──────────┐     ┌─────┐           │
│                   │          │  HUMAN   │────▶│DDA E│──┐        │
│                   │          │  REVIEW  │     └─────┘  │        │
│                   │          └──────────┘              │        │
│                   │                                    ▼        │
│                   ▼                                 ┌─────┐     │
│                ┌─────┐     ┌─────┐                  │DDA G│     │
│                │DDA C│────▶│DDA D│─────────────────▶│merge│     │
│                └─────┘     └──┬──┘                  └─────┘     │
│                               │                       ▲         │
│                               │    ┌─────┐            │         │
│                               └───▶│DDA F│────────────┘         │
│                                    └─────┘                      │
│                                    (cycle with exit condition)  │
└─────────────────────────────────────────────────────────────────┘
```

### Planned Node Types

| Node Type          | Description                                              |
| :----------------- | :------------------------------------------------------- |
| DDA                | Execute a Data-Driven Agent                              |
| HUMAN_IN_THE_LOOP  | Human review/approval gate                               |
| CONDITIONAL        | Route to different branches based on runtime evaluation  |
| FAN_OUT            | Split execution into parallel branches                   |
| FAN_IN             | Merge results from parallel branches                     |
| LOOP               | Repeated execution with configurable exit condition      |

### Planned Security Controls

| Control               | Implementation                                          |
| :-------------------- | :------------------------------------------------------ |
| Graph Validation      | Cycle detection with mandatory exit conditions           |
| Permission Propagation | Path-aware permission checking across all graph branches |
| Parallel Isolation    | Concurrent branch executions fully isolated              |
| Convergence Validation | Merged results validated against output schemas         |
| Dynamic Route Audit   | All routing decisions logged with decision rationale    |
| Resource Budgeting    | Per-graph execution resource limits                     |

---

## MCP Integrations

MCP (Model Context Protocol) Integrations provide connectivity to external tools and services. The Studio manages MCP integration types, instances, and credentials as separate entities.

### MCP Integration Architecture

| Entity      | Description                                               |
| :---------- | :-------------------------------------------------------- |
| Types       | Definitions of available MCP tools with credential schemas |
| Instances   | Configured connections to specific MCP tool deployments    |
| Credentials | Stored authentication credentials for MCP connections      |

### MCP Integration Types

| Field              | Description                                    |
| :----------------- | :--------------------------------------------- |
| Name               | Integration type name                          |
| Description        | Tool capabilities description                  |
| Command            | MCP server command to execute                  |
| Args               | Command-line arguments for the MCP server      |
| Tools              | List of available tools exposed by the server  |
| Credentials Schema | JSON schema defining required authentication fields |
| Thumbnail          | Visual preview of the integration              |

### MCP Instance Management

| Operation | Description                                              |
| :-------- | :------------------------------------------------------- |
| Create    | Configure a new MCP instance from a type definition      |
| List      | View all configured MCP instances                        |
| Update    | Modify instance configuration                            |
| Delete    | Remove an MCP instance                                   |

### MCP Credential Management

| Operation | Description                                              |
| :-------- | :------------------------------------------------------- |
| Create    | Store credentials for an MCP integration                 |
| List      | View available credential sets (metadata only)           |
| Update    | Rotate or modify stored credentials                      |
| Delete    | Remove stored credentials                                |

### MCP Security Controls

| Control              | Implementation                                    |
| :------------------- | :------------------------------------------------ |
| Schema Validation    | Tool inputs validated against MCP schema          |
| Credential Isolation | Credentials stored encrypted, never exposed in logs |
| Permission Enforcement | Tool actions authorized per user permissions     |
| Rate Limiting        | Per-tool request limits                           |
| Audit Logging        | All tool invocations logged                       |
| Version Pinning      | Explicit tool versions prevent supply chain attacks |

---

## External APIs

The Studio provides management for external API endpoint configurations that can be referenced by DDAs and Utilities.

### API Configuration

| Field        | Description                                    |
| :----------- | :--------------------------------------------- |
| Name         | API endpoint identifier                        |
| Method       | HTTP method (GET, POST, PUT, DELETE, etc.)      |
| Endpoint URL | Target API endpoint URL                        |
| Parameters   | Query and path parameter definitions           |
| Body         | Request body template                          |
| Auth Header  | Authentication header configuration            |

### API Management

| Operation | Description                                    |
| :-------- | :--------------------------------------------- |
| Create    | Define a new external API endpoint             |
| List      | View all configured API endpoints              |
| Update    | Modify API endpoint configuration              |
| Delete    | Remove an API endpoint configuration           |

### API Security Controls

| Control             | Implementation                                  |
| :------------------ | :---------------------------------------------- |
| Endpoint Validation | URLs validated and allowlisted                  |
| Auth Management     | Authentication headers managed securely         |
| Input Sanitization  | Parameters and body content sanitized           |
| Response Validation | API responses validated before processing       |
| Audit Logging       | All API calls logged with parameters and status |

---

## Scripts

Scripts are code components that can be referenced in DDA query plans for custom data processing logic.

### Script Management

| Operation | Description                                    |
| :-------- | :--------------------------------------------- |
| List      | View all available scripts                     |

### Script Usage in Query Plans

| Context      | Description                                       |
| :----------- | :------------------------------------------------ |
| DDA Plan Item | Referenced as SCRIPT type in DDA query plans     |
| Source Router | Available as SCRIPT type through the sources API |

---

## Asset Management

The Studio provides unified asset management capabilities across all asset types, including semantic search, media and model asset management, and source routing.

### Unified Assets

The Unified Assets API provides a consolidated view across all Studio asset types.

| Asset Category | Included Types                               |
| :------------- | :------------------------------------------- |
| DDAs           | Data-Driven Agents                           |
| Chains         | Chain of Agents workflows                       |
| Datasets       | Structured data collections                  |
| Widgets        | Visual interface components                  |
| Utilities      | Reusable API/DDA components                  |
| Media          | Media files and content assets               |
| Models         | Machine learning model assets                |

**Access Filters:**

| Filter     | Description                                    |
| :--------- | :--------------------------------------------- |
| owned      | Assets owned by the authenticated user         |
| accessible | Assets the user has been granted access to     |
| all        | All assets the user can view                   |

### Asset Search

The semantic search capability enables discovery across all Studio asset types using natural language queries.

| Parameter         | Description                                    |
| :---------------- | :--------------------------------------------- |
| Query             | Natural language search term                   |
| Distance Threshold | Maximum semantic distance for matching results |
| Top K             | Maximum number of results to return            |

**Search Modes:**

| Mode      | Description                                       |
| :-------- | :------------------------------------------------ |
| Standard  | Search across all asset types by semantic similarity |
| Step-Based | Search for individual workflow steps and components |

### Media Assets

| Field            | Description                                |
| :--------------- | :----------------------------------------- |
| Name             | Media asset identifier                     |
| Content URL      | URL to the media file content              |
| Policy Source URL | URL to associated usage policies          |
| Thumbnail        | Preview image                              |

### Model Assets

| Field     | Description                                    |
| :-------- | :--------------------------------------------- |
| Name      | Model asset identifier                         |
| Files     | Uploaded model files                           |
| Thumbnail | Preview image                                  |

### Sources Router

The Sources Router provides a unified view of all available data sources that can be referenced in DDA query plans.

| Source Type | Description                                    |
| :---------- | :--------------------------------------------- |
| DATASET     | Studio datasets                                |
| MCP         | MCP integration tool connections               |
| DDA         | Data-Driven Agents (for sub-agent execution)   |
| SCRIPT      | Code scripts for custom processing             |

### Classification

| Entity    | Description                                    |
| :-------- | :--------------------------------------------- |
| Industries | Industry categories for asset classification  |
| Tags       | User-defined tags for asset organization       |

---

## AI Hybrid Planning

The AI Hybrid Planning feature enables automatic creation of DDAs from natural language descriptions. Users provide a name, description, and instructions, and the system generates a structured DDA with appropriate configuration.

### Planning Parameters

| Parameter     | Description                                        |
| :------------ | :------------------------------------------------- |
| Name          | Desired DDA name                                   |
| Description   | Purpose description in natural language            |
| Instructions  | Behavioral guidelines for the DDA                  |
| Is Planned    | Whether to generate a query plan automatically     |
| Is Structured | Whether to enforce schema-structured output        |
| Has Widget    | Whether to generate an associated widget           |

### Planning Flow

| Stage              | Description                                         |
| :----------------- | :-------------------------------------------------- |
| Input Analysis     | Parse natural language description and instructions |
| Plan Generation    | Generate query plan with appropriate data sources   |
| Schema Mapping     | Map to relevant domain schemas                      |
| DDA Construction   | Create DDA definition with model and prompt          |
| Widget Generation  | Optionally generate associated widget type           |
| Draft Creation     | Save as DRAFT stage for user review                 |

### Security Controls

| Control           | Implementation                                    |
| :---------------- | :------------------------------------------------ |
| Input Validation  | Natural language inputs filtered and validated     |
| Permission Scoping | Generated DDA limited to user's authorized resources |
| Schema Binding    | Generated plans bound to existing domain schemas   |
| Draft Only        | AI-generated DDAs always start as DRAFT            |
| Audit Trail       | All planning steps logged                          |

---

## AI Workflow Execution

The AI Workflow Execution endpoint enables direct execution of published DDAs via query-based invocation.

### Execution Interface

| Parameter  | Description                                    |
| :--------- | :--------------------------------------------- |
| Agent UUID | Unique identifier of the DDA to execute        |
| Query      | Natural language query for the DDA to process  |

### Execution Security

| Control            | Implementation                                |
| :----------------- | :-------------------------------------------- |
| Authentication     | HTTPBearer (JWT) token required               |
| Authorization      | User must have execution permission on the DDA |
| Sandbox Isolation  | Execution occurs in isolated sandbox           |
| Audit Logging      | All executions logged with query and results   |

---

## Text-to-Pipeline Generation

The Text-to-Pipeline feature enables users to create workflows using natural language descriptions. The system generates a Domain Specific Language (DSL) representation that can be visualized, refined, and executed.

### Generation Flow

| Stage              | Description                                                       |
| :----------------- | :---------------------------------------------------------------- |
| User Input         | Natural language description of desired workflow                  |
| Intent Analysis    | Parse intent, identify data sources, operations, and conditions   |
| DSL Generation     | Generate structured pipeline definition                           |
| Visual Preview     | Interactive pipeline display with flow diagram and step details   |
| Refinement         | Iterate with natural language commands to modify the pipeline     |
| Execution          | Run immediately, schedule, or save as reusable template           |

### Pipeline DSL Structure

| Component         | Description                              | Purpose                    |
| :---------------- | :--------------------------------------- | :------------------------- |
| Pipeline Metadata | Name, version, description, author       | Identification, versioning |
| Inputs            | Input parameters with types, validation  | Data entry points          |
| Steps             | Ordered operations with tool mappings    | Execution sequence         |
| Connections       | Data flow between steps                  | Dependency management      |
| Outputs           | Result definitions and transformations   | Output specification       |
| Constraints       | Resource limits and execution policies   | Security and governance    |

### DSL Validation

| Check              | Description                                    | Failure Action               |
| :----------------- | :--------------------------------------------- | :--------------------------- |
| Syntax Validation  | DSL conforms to schema                         | Highlight errors, suggest fixes |
| Tool Availability  | Referenced tools exist and are accessible      | Show unavailable tools        |
| Permission Check   | User authorized for all tools and data         | Flag unauthorized steps       |
| Type Compatibility | Input/output types match across connections    | Show type mismatches          |
| Cycle Detection    | No circular dependencies                       | Identify cycle location       |
| Resource Estimation | Estimated resource usage within limits        | Warn if limits exceeded       |

### Security Controls

| Control                 | Implementation                                        |
| :---------------------- | :---------------------------------------------------- |
| Intent Validation       | Generated DSL limited to user's authorized capabilities |
| Tool Scoping            | Only tools the user has access to can be included     |
| Data Source Verification | Data sources validated against user permissions       |
| Preview Sandbox         | Pipeline preview runs in isolated environment         |
| Audit Trail             | All generation and refinement steps logged            |
| Version Control         | DSL changes tracked with full history                 |

---

## Tool Authorization

DDAs can only invoke tools explicitly authorized for the user and use case.

### Tool Categories

| Category                  | Authorization Level   | Approval Required      |
| :------------------------ | :-------------------- | :--------------------- |
| Read-Only (Search, Query) | User permission       | Automatic              |
| Data Modification         | Explicit grant        | Automatic with logging |
| External API Calls        | Per-API authorization | Risk-dependent         |
| Administrative Actions    | Privileged access     | Multi-party approval   |

### Tool Permission Model

| Permission              | Description              |
| :---------------------- | :----------------------- |
| `tools.search.read`    | Query knowledge base     |
| `tools.data.write`     | Modify user data         |
| `tools.external.call`  | Call external APIs       |
| `tools.admin.manage`   | Administrative operations |
| `tools.data.privileged` | Access privileged data  |

---

## Credential Handling

### Credential Vault

| Control  | Implementation                            |
| :------- | :---------------------------------------- |
| Encryption | AES-256-GCM with HSM-backed keys        |
| Access Control | User-scoped and DDA-scoped credentials |
| Audit    | All credential access logged              |
| Rotation | Automatic rotation support                |

### Credential Types

| Type                 | Storage                       | Access Pattern             |
| :------------------- | :---------------------------- | :------------------------- |
| API Keys             | Encrypted vault               | DDA-scoped retrieval       |
| OAuth Tokens         | Encrypted vault with refresh  | Automatic refresh          |
| Database Credentials | Encrypted vault               | Just-in-time retrieval     |
| Certificates         | Certificate store             | Managed lifecycle          |
| MCP Credentials      | Encrypted vault               | Per-integration retrieval  |

### Credential Injection

Credentials are never exposed in DDA definitions:

1. DDA references credential by name
2. At execution time, vault retrieves and decrypts credential
3. Credential injected into sandbox environment variable
4. After execution, sandbox destroyed with all credentials

### Google OAuth Integration

The platform supports Google OAuth for connecting to Google services.

| Stage    | Description                                    |
| :------- | :--------------------------------------------- |
| Auth URL | Platform generates OAuth authorization URL     |
| Callback | Platform receives OAuth callback with tokens   |
| Storage  | Tokens stored securely in credential vault     |
| Refresh  | Automatic token refresh on expiration          |

---

## Operational Modes

The platform provides five operational modes that organizations can configure based on their policies, risk tolerance, and use case requirements. Users can adjust automation levels at any time and are never locked into a single approach.

### Mode Overview

```
┌───────────────────────────────────────────────────────────────────────────┐
│                    OPERATIONAL MODE SPECTRUM                              │
├───────────────────────────────────────────────────────────────────────────┤
│                                                                           │
│  MODE 0          MODE 1          MODE 2          MODE 3          MODE 4   |
│  ────────────────────────────────────────────────────────────────────────►|
│  Traditional     AI-Assisted     Routine       Autonomous       Fully     |
│  Platform        Manual          Automation    with Escalation  Automated |
│  (No DDAs)                                                     with Audit |
│                                                                           │
│  ◄──────── Human Control ────────────── AI Automation ────────────────►   │
└───────────────────────────────────────────────────────────────────────────┘
```

### Mode Definitions

**Mode 0: Traditional Platform (No AI Agents)**

| Aspect       | Description                                                          |
| :----------- | :------------------------------------------------------------------- |
| Operation    | System operates as traditional data platform                         |
| User Role    | Users manually query data, build graphs, analyze results             |
| AI Capabilities | Limited to basic search, entity extraction, document classification |
| Decisions    | All analytical steps and conclusions are user-driven                 |
| Use Case     | Organizations requiring full manual control or regulatory constraints |

**Mode 1: Fully Manual with AI Assistance**

| Aspect       | Description                                                     |
| :----------- | :-------------------------------------------------------------- |
| Operation    | Users drive all decisions and processing steps                  |
| DDA Role     | DDAs operate in "suggest-only" mode                             |
| AI Activities | Flagging patterns, gathering supporting data, highlighting anomalies |
| Decisions    | All conclusions and next steps require user approval            |
| Use Case     | Building trust in AI capabilities, high-stakes operations       |

**Mode 2: DDAs Handle Routine Tasks**

| Aspect              | Description                                             |
| :------------------ | :------------------------------------------------------ |
| Operation           | DDAs autonomously perform routine operations            |
| Automated Tasks     | Entity resolution, document classification, data collection |
| Human Focus         | Analysis, interpretation, high-value decisions          |
| Validation Required | Significant findings require human review               |
| Use Case            | Balanced approach for standard operations               |

**Mode 3: Autonomous with Escalation**

| Aspect              | Description                                              |
| :------------------ | :------------------------------------------------------- |
| Operation           | DDAs conduct complete workflows independently            |
| Workflow            | Follow predefined workflows from start to completion     |
| Escalation Triggers | Contradictions, low-confidence findings, high-impact discoveries |
| Human Role          | Review completed work packages, validate conclusions     |
| Use Case            | High-volume processing with human oversight for exceptions |

**Mode 4: Fully Automated with Audit**

| Aspect     | Description                                              |
| :--------- | :------------------------------------------------------- |
| Operation  | DDAs run workflows end-to-end without interruption       |
| Human Role | Post-workflow audits of conclusions and evidence         |
| Provenance | System maintains complete audit trail                    |
| Review Timing | Periodic batch review or risk-triggered review        |
| Use Case   | Maximum efficiency for low-risk, high-volume operations  |

### Granular Control Options

| Control                    | Description                                             |
| :------------------------- | :------------------------------------------------------ |
| Selective DDA Activation   | Disable specific DDAs while keeping others active       |
| Confidence Thresholds      | Set thresholds requiring human review when certainty drops |
| Case Type Policies         | Apply different modes to different case types or stages |
| Override Capability        | Override DDA recommendations with user judgment          |
| Pause/Resume               | Pause and resume automated workflows as needed          |

### Mode Transition

| Transition                   | Use Case                                                  |
| :--------------------------- | :-------------------------------------------------------- |
| Higher → Lower Automation    | Workflow identifies critical issue, switch to manual      |
| Lower → Higher Automation    | Initial review complete, transition to automated processing |
| Per-Stage Configuration      | Different modes for different workflow phases             |
| Emergency Override           | Immediate switch to full manual control                  |

### Mode Security Controls

| Control           | Implementation                                    |
| :---------------- | :------------------------------------------------ |
| Mode Authorization | Only authorized users can change operational modes |
| Mode Audit        | All mode changes logged with justification        |
| Default Mode      | Organization-wide default mode setting            |
| Mode Inheritance  | Child workflows inherit parent mode unless overridden |
| Compliance Lock   | Certain modes can be locked for regulatory compliance |

---

## Human-in-the-Loop Controls

High-risk operations require human approval before execution. These controls operate in conjunction with operational modes and Chain of Agents HUMAN_IN_THE_LOOP items, providing safeguards even in higher-automation modes.

### Risk Classification

| Risk Level | Criteria                        | Approval Flow          |
| :--------- | :------------------------------ | :--------------------- |
| Low        | Read-only, no external effects  | Automatic              |
| Medium     | Data modification, limited scope | User confirmation     |
| High       | External actions, bulk operations | Explicit approval + MFA |
| Critical   | Administrative, irreversible    | Multi-party approval   |

### Approval Controls

| Stage        | Action                    | Timeout     |
| :----------- | :------------------------ | :---------- |
| Request      | DDA requests approval     | N/A         |
| Presentation | User shown action details | N/A         |
| Confirmation | User approves or rejects  | 5 minutes   |
| Execution    | Approved action executed  | N/A         |
| Audit        | Decision and outcome logged | N/A       |

---

## Testing Framework Security

### Test Isolation

| Control                | Implementation                            |
| :--------------------- | :---------------------------------------- |
| Environment Isolation  | Tests run in separate environment         |
| Data Isolation         | Test data separated from production       |
| Credential Isolation   | Test credentials separate from production |
| Result Isolation       | Test results not exposed to production    |

### Test Types

| Test Type          | Purpose                      | Security Focus        |
| :----------------- | :--------------------------- | :-------------------- |
| Unit Tests         | Individual step validation   | Input validation      |
| Integration Tests  | End-to-end flow validation   | Authorization flow    |
| Security Tests     | Vulnerability detection      | Injection, bypass     |
| Performance Tests  | Latency and throughput       | Resource exhaustion   |

### Simulation Security

| Capability              | Security Control                       |
| :---------------------- | :------------------------------------- |
| Mock Data Sources       | Generated data, no production access   |
| Mock External Services  | Simulated responses, no real calls     |
| Load Simulation         | Rate-limited, isolated environment     |
| Failure Injection       | Controlled, no production impact       |

---

## Authentication

All Studio API endpoints require HTTPBearer (JWT) authentication. The authenticated user context determines asset access, execution permissions, and runtime configurations.

### User Context

| Field | Description                                    |
| :---- | :--------------------------------------------- |
| ID    | Unique user identifier                         |
| Email | User email address                             |

### System API Access

For system-level operations such as attaching or detaching users from assets, a separate system API key authentication is required via the `X-System-API-Key` header.

| Operation    | Description                                    |
| :----------- | :--------------------------------------------- |
| Attach User  | Grant a user access to a specific asset        |
| Detach User  | Remove a user's access to a specific asset     |

---

## Audit Logging

### Logged Events

| Event Category    | Logged Data                                  | Retention |
| :---------------- | :------------------------------------------- | :-------- |
| DDA Execution     | DDA ID, user, inputs hash, duration, status  | 1 year    |
| Tool Invocation   | Tool ID, parameters, result status           | 1 year    |
| Chain Execution   | Chain ID, DDAs involved, flow path           | 1 year    |
| Approval Decisions | Request, decision, approver, timestamp      | 2 years   |
| Credential Access | Credential ID, accessor, purpose             | 2 years   |
| Security Events   | Violation type, details, action taken        | 2 years   |
| Asset Changes     | Asset ID, operation, user, before/after state | 1 year   |
| Search Queries    | Query text, results count, user              | 1 year    |

### Log Security

| Control         | Implementation                                |
| :-------------- | :-------------------------------------------- |
| Integrity       | Cryptographic hash chain prevents tampering   |
| Confidentiality | Logs encrypted at rest                        |
| Access Control  | Auditor role required; no delete capability   |
| Retention       | Configurable per regulation                   |

---

## API Reference Summary

| Endpoint Group         | Base Path                       | Operations           |
| :--------------------- | :------------------------------ | :------------------- |
| Health Check           | `/api/health-check`             | GET                  |
| Users                  | `/api/users`                    | GET (me)             |
| Domain Discovery       | `/api/domain_discover`          | POST                 |
| Domains                | `/api/domains`                  | CRUD                 |
| Schemas                | `/api/schemas`                  | CRUD                 |
| Datasets               | `/api/datasets`                 | CRUD + draft + files |
| DDAs                   | `/api/ddas`                     | CRUD + draft + execute |
| Chains of DDAs         | `/api/chain-of-ddas`            | CRUD + draft + execute |
| MCP Integration Types  | `/api/mcp-integrations-types`   | CRUD                 |
| MCP Instances          | `/api/mcp-integrations`         | CRUD                 |
| MCP Credentials        | `/api/mcp-integrations-credentials` | CRUD             |
| Widget Types           | `/api/widget-types`             | CRUD                 |
| Utilities              | `/api/utilities`                | CRUD + draft + execute |
| APIs                   | `/api/apis`                     | CRUD                 |
| Industries             | `/api/industries`               | CRUD                 |
| Tags                   | `/api/tags`                     | CRUD                 |
| Scripts                | `/api/scripts`                  | LIST                 |
| Asset Search           | `/api/asset_search`             | POST                 |
| Media Assets           | `/api/media-assets`             | CRUD                 |
| Model Assets           | `/api/model-assets`             | CRUD                 |
| Sources                | `/api/source-router`            | LIST                 |
| Unified Assets         | `/api/assets`                   | LIST                 |
| AI Workflow Execution  | `/api/ai-workflow-execution`    | POST                 |
| AI Hybrid Planning     | `/api/ai-workflow-planning`     | POST                 |
| Google OAuth           | `/api/auth/google`              | GET + callback       |
| Asset Users (System)   | `/api/asset-users`              | POST + DELETE        |

---
