---
layout: default
title: Table of Contents
---

# DataFab Documentation - Table of Contents

**Version:** 6.0
**Last Updated:** February 2026

---

## Document Overview

| Document                                                      | Description                                                           | Version |
| :------------------------------------------------------------ | :-------------------------------------------------------------------- | :------ |
| [01-Introduction](./01-Introduction.md)                       | Platform overview and security summary                                | 3.2     |
| [02-Architecture](./02-Architecture.md)                       | System architecture and components                                    | 5.0     |
| [03-Knowledge-Fabric](./03-Knowledge-Fabric.md)               | Data integration and knowledge graph                                  | 4.0     |
| [04-Studio](./04-Studio.md)                                   | DDAs, widgets, datasets, utilities, Chain of Agents, MCP integrations | 6.0     |
| [05-AI-LLM](./05-AI-LLM.md)                                   | AI and LLM security architecture                                      | 3.0     |
| [06-CI-CD](./06-CI-CD.md)                                     | CI/CD pipeline security                                               | 2.0     |
| [07-Security-Operations](./07-Security-Operations.md)         | SOC, monitoring, and incident response                                | 2.0     |
| [08-Graph-Operations](./08-Graph-Operations.md)               | Graph rule engine, workflows, screening                               | 4.2     |
| [09-Schema-Management](./09-Schema-Management.md)             | Business domain discovery, schema registry                            | 2.0     |
| [10-Compliance-Capabilities](./10-Compliance-Capabilities.md) | Platform compliance features                                          | 3.0     |
| [11-API-Security](./11-API-Security.md)                       | API gateway, authentication, rate limiting                            | 5.0     |
| [12-Exchange](./12-Exchange.md)                               | Data asset marketplace, wallet & blockchain                           | 4.0     |
| [13-Graph-RAG](./13-Graph-RAG.md)                             | Graph-enhanced retrieval augmented generation                         | 3.0     |
| [14-Trust-Compliance](./14-Trust-Compliance.md)               | Trust & Compliance for managed deployments                            | 2.0     |


---

## 01 - Introduction

- Executive Summary
- Platform Capabilities
  - Knowledge Fabric
  - Studio
  - Exchange
  - Graph RAG
  - Graph Operations
  - AI & LLM Layer
- Document Structure
- Security Principles
- Operational Modes
- Regulatory Compliance
- Contact

---

## 02 - Architecture

### Platform Overview
- Platform Components

### Architecture Overview

### Knowledge Fabric
- Core Capabilities
- Knowledge Graph Model
- Entity Resolution

### Studio
- Core Capabilities
- DDA Architecture (Data-Driven Agents)
- Chain of Agents
- Graph of Agents (Planned)
- Utilities
- MCP Integrations
- AI Hybrid Planning
- Operational Modes

### Exchange
- Core Capabilities
- Asset Types
- Marketplace Model

### Schema Management
- Core Capabilities
- Schema Usage Across Platform
- Document-to-Schema Discovery

### AI & LLM Layer
- Core Capabilities
- LLM Output Consistency
- Provider Support

### Graph Operations Module
- Core Capabilities
- Pattern Detection
- Graph Workflows

### Network Architecture
- Network Segmentation
- Connectivity Patterns

### Data Flow Model

### Security Architecture
- Defense-in-Depth Model
- Cryptographic Standards

### Integration Points
- External System Integration
- MCP Protocol

### Deployment Models
- Deployment Options
- SaaS Multi-Tenant
- Dedicated Cloud Tenant
- Customer Cloud Deployment
- On-Premises Deployment
- Data Residency Configuration
- LLM Provider Configuration by Deployment
- Deployment Feature Comparison

---

## 03 - Knowledge Fabric

### Component Overview

### Architecture Overview

### Knowledge Graph
- Graph Architecture
- Entity Types
- Relationship Types
- Graph Security Controls

### Entity Resolution
- Entity Resolution Architecture
- Resolution Components
- Matching Methods
- Entity Resolution Security
- Golden Record Management

### External Source Integration
- External Source Architecture
- External Source Categories
- OSINT Integration Security
- Enrichment Workflow
- External Source Monitoring

### Customer System Connections
- Connection Architecture
- Synchronization Patterns
- Customer System Types
- Connection Security Controls
- Data Synchronization Security

### Two-Way Data Flow
- Data Flow Architecture
- Read Operations (Data Access)
- Write Operations (Data Updates)
- Write-Back Workflow
- Write-Back Security Controls
- Multi-System Coordination
- What Knowledge Fabric Stores vs. What Remains in Source Systems

### Customer System Health Monitoring

### Connectivity
- Connection Types
- Database Connectivity Security
- API Connectivity Security
- MCP Connector Security (200+ connectors)
- Enterprise Data Integration
- MCP Connector Configuration
- Source System Connectivity Patterns
- MCP Integration Lifecycle Management

### Discovery Service
- Discovery Components
- Discovery Security Controls
- Discovery Scope Management
- Discovery Audit Trail

### Active Metadata
- Active Metadata Capabilities
- Automated Classification
- Lineage Tracking

### Persistent Knowledge Graph
- Knowledge Tree Structure
- Schema-Bounded Extraction
- Source Provenance Model
- Incremental Updates

### Search Sessions
- Session Architecture
- Session Graph Accumulation
- Query Turn Processing
- Search Session Security

### Data Observability
- Observability Integration
- Data Quality Metrics
- Quality Test Integration
- Observability Alerts

### Data Insights and KPIs
- Key Performance Indicators
- Platform Analytics

### Graph Database Security
- Query Security

### Monitoring
- Health Monitoring
- Performance Monitoring
- Security Monitoring
- SIEM Integration

### Authentication and Access Control
- Authentication Mechanisms
- Session Management
- Authorization Model

### Credential Management
- Source System Credentials
- Supported Credential Types

### Data Protection
- Data Classification Framework
- Data Masking

### Audit Logging
- Logged Events
- Log Security

---

## 04 - Studio

### Component Overview
- Asset Types
- Lifecycle Stages
- Asset States

### Architecture Overview

### Business Domains
- Domain Management
- Domain Discovery

### Schemas
- Schema Management
- Schema-Driven Processing

### Data-Driven Agents (DDAs)
- DDA Architecture
- DDA Definition
- Query Plan (DATASET, MCP, DDA, SCRIPT items)
- Placeholders (MCP_INTEGRATION, DATASET, DDA)
- Runtime Configuration
- DDA Lifecycle (Create, Draft, Apply Draft, Execute)
- DDA Creation Flow
- DDA Execution Security
- Execution Sandbox

### Widget Types
- Widget Type Classification (SYSTEM, OUTPUT)
- Widget View Types (dialog, canvas, both)
- Widget Type Structure
- Widget Type Management
- Widget Security Controls

### Datasets
- Dataset Architecture
- Dataset Structure (files, file_mapping, schemas, runtime config)
- Dataset Lifecycle (draft/publish)
- Dataset Security Controls
- Dataset Access Patterns

### Utilities
- Utility Structure
- Utility Placeholder Types (API, DDA)
- Utility Lifecycle
- Utility Security Controls

### Chain of Agents
- Chain Query Plan (DDA, HUMAN_IN_THE_LOOP items)
- Chain Structure
- Chain Lifecycle
- Communication Patterns
- Multi-Agent Security Controls
- Orchestration Security
- State Management Security
- Error Handling and Recovery

### Graph of Agents (Planned)
- Graph vs. Chain Comparison
- Planned Graph Structure
- Planned Node Types (DDA, HUMAN_IN_THE_LOOP, CONDITIONAL, FAN_OUT, FAN_IN, LOOP)
- Planned Security Controls

### MCP Integrations
- MCP Integration Architecture (Types, Instances, Credentials)
- MCP Integration Types
- MCP Instance Management
- MCP Credential Management
- MCP Security Controls

### External APIs
- API Configuration
- API Management
- API Security Controls

### Scripts
- Script Management
- Script Usage in Query Plans

### Asset Management
- Unified Assets
- Asset Search (semantic, step-based)
- Media Assets
- Model Assets
- Sources Router (DATASET, MCP, DDA, SCRIPT)
- Classification (Industries, Tags)

### AI Hybrid Planning
- Planning Parameters
- Planning Flow
- Security Controls

### AI Workflow Execution
- Execution Interface
- Execution Security

### Text-to-Pipeline Generation
- Generation Flow
- Pipeline DSL Structure
- DSL Validation
- Security Controls

### Tool Authorization
- Tool Categories
- Tool Permission Model

### Credential Handling
- Credential Vault
- Credential Types
- Credential Injection
- Google OAuth Integration

### Operational Modes
- Mode Overview
- Mode Definitions (Modes 0-4)
- Granular Control Options
- Mode Transition
- Mode Security Controls

### Human-in-the-Loop Controls
- Risk Classification
- Approval Controls

### Testing Framework Security
- Test Isolation
- Test Types
- Simulation Security

### Authentication
- User Context
- System API Access

### Audit Logging
- Logged Events
- Log Security

### API Reference Summary

---

## 05 - AI & LLM

### Component Overview

### LightLLM Router Architecture
- LightLLM Security Benefits

### LLM Output Consistency
- Schema-Validated Extraction
- Ontology-Based Execution
- Reasoning Chain Transparency
- Deterministic vs. Probabilistic Components

### LLM Monitoring and Observability
- Phoenix Monitoring Integration
- Quality Metrics

### Model Version Management
- Model Update Process
- A/B Testing Framework

### LLM Provenance
- Complete Invocation Logging
- Provenance Security

### Provider Security
- Provider Assessment Requirements
- Provider Isolation

### Prompt Security
- Prompt Injection Defense
- Input Sanitization
- Instruction Hierarchy

### Data Protection in AI Pipelines
- PII Handling
- Tenant Data Isolation

### Content Safety
- Input Content Filtering
- Output Content Filtering
- Hallucination Mitigation

### Vector and Embedding Security
- Embedding Security
- Retrieval Security

### Audit Logging
- AI-Specific Events
- Security Events

### Responsible AI
- Ethical Principles
- Explainability

### Quality Assurance and Feedback
- Output Tracking Mechanisms
- Quality Adjustment Mechanisms
- Continuous Improvement

### Model Lifecycle Management
- Model Selection and Configuration
- Model-Agnostic Architecture
- Model Deprecation

---

## 06 - CI/CD

### CI/CD Overview

### Source Control Security
- Repository Security
- Branching Strategy

### Security Scanning
- Secret Scanning
- Static Application Security Testing (SAST)
- Dependency Scanning
- Container Image Scanning

### Code Quality Gates

### Vulnerability Management
- Response Times
- Vulnerability Workflow

### Continuous Deployment
- Deployment Pipeline
- Deployment Security
- Blue-Green Deployment

### Secure Development Practices
- Developer Environment
- Code Review Security

### Audit and Compliance
- CI/CD Audit Trail
- Compliance Controls

---

## 07 - Security Operations

### Security Monitoring
- Security Operations Center (SOC)
- Monitoring Coverage

### Endpoint Protection
- Mobile Device Management (MDM)
- Extended Detection and Response (XDR)
- Device Control

### Monitoring Infrastructure
- Metrics Collection
- Log Management
- Alerting

### Incident Response
- Incident Classification
- Response Phases
- Communication Plan

### Business Continuity
- Recovery Objectives
- Backup Strategy
- Disaster Recovery

### Security Training
- Awareness Program
- Training Topics

---

## 08 - Graph Operations

### Component Overview

### Architecture Overview

### Knowledge Graph for Operations
- Operational Entity Model
- Operational Relationship Types
- Entity Resolution for Operations
- Graph Queries for Operations

### Graph Rule Engine
- Rule Engine Architecture
- Rule Types
- Rule Definition Security
- Pattern Scoring Rules
- Rule Versioning
- Rule Execution Security
- Rule Audit Trail

### Graph Workflows
- Workflow Architecture
- Operational Process Types
- Risk-Based Workflow Triggering
- Workflow Task Types
- Workflow Security Controls
- Workflow Definition Security
- Task Assignment Security
- Escalation Controls
- Process Instance Security

### External Source Integration (OSINT)
- External Source Categories
- OSINT Integration Security
- Enrichment Workflow

### Graph Screening Service
- Screening Types
- Screening Security Controls

### Operations Case Management
- Case Types
- Case Security Controls

### User Roles and Permissions
- Operations-Specific Roles
- Permission Matrix

### Audit Logging
- Operations-Specific Events
- Regulatory Retention

### Reporting and Analytics
- Operations Dashboards
- Report Security

---

## 09 - Schema Management

### Component Overview

### Architecture Overview

### Business Domain Discovery
- Discovery Flow
- Supported Document Types
- Concept Extraction

### Schema Definition
- Schema Structure
- Entity Definition
- Attribute Types
- Constraint Types

### Schema Registry
- Registry Capabilities
- Version Management
- Schema Dependencies

### Schema Usage
- Studio Integration
- OSINT Extractor Integration
- MCP Connector Integration

### Schema Validation
- Validation Modes
- Validation Results
- Validation Security

### Security Controls
- Schema Access Control
- Schema Governance
- Schema Security

### Audit Logging
- Logged Events
- Audit Trail Security

---

## 10 - Compliance Capabilities

### Compliance Framework
- Applicable Regulations (GDPR, CCPA, SOC 2, HIPAA, PCI DSS)

### Data Protection
- GDPR Compliance
- CCPA/CPRA Compliance
- Data Subject Rights

### SOC 2 Alignment
- Trust Service Criteria

### AI Governance
- EU AI Act Alignment
- Responsible AI Principles

### Audit Logging
- Audit Requirements
- Log Retention

### Data Hold and Retention Management
- Retention Policy Framework
- Data Hold Capabilities
- Retention Policy Types
- Metadata-Based Policy Enforcement
- GDPR Data Subject Rights Integration
- Retention Execution
- Retention Audit Trail

### Third-Party Risk Management
- Vendor Assessment
- Contractual Requirements

### Policy Framework
- Security Policies
- Policy Management

### Data Residency

### Compliance Reporting
- Available Reports
- Audit Support

---

## 11 - API Security

### Component Overview

### Architecture Overview

### API Gateway
- Gateway Capabilities
- Gateway Security Controls

### Authentication
- Authentication Methods
- OAuth 2.0 Flows
- Token Security
- API Key Management

### Authorization
- Authorization Model
- API Scopes
- Permission Enforcement

### Rate Limiting
- Rate Limit Tiers
- Rate Limit Headers
- Rate Limit Strategies
- Rate Limit Responses

### API Versioning
- Versioning Strategy
- Version Lifecycle
- Breaking Changes Policy
- Deprecation Headers

### Request Validation
- Validation Layers
- Input Sanitization
- Security Headers

### Error Handling
- Error Response Format
- Error Categories
- Error Security

### Webhook Security
- Webhook Authentication
- Webhook Headers
- Webhook Security Controls

### Service-to-Service Communication
- Internal Authentication
- Internal Authorization

### Audit Logging
- Logged Events
- Log Security

### Security Monitoring
- Monitoring Metrics
- Threat Detection

### Client SDKs
- Available SDKs
- SDK Security Features

---

## 12 - Exchange

### Component Overview

### Architecture Overview

### User Profiles
- Profile Types (Consumer, Provider, Both)
- Profile Lifecycle
- Profile Security Controls

### Asset Catalog
- Asset Types (BEHAVIOUR_DATA, AGENT, WIDGET, UTILITY, MEDIA, MODEL, DATASET, CHAIN)
- Asset Lifecycle (DRAFT → PUBLISHED → ARCHIVED)
- Catalog Operations
- Catalog Security Controls

### Wallet & Blockchain
- Currency Support (ETH, DAAC)
- Wallet Operations
- Blockchain Integration
- Wallet Security Controls

### Metering & Billing
- Metering Event Types
- Metering Policies
- Metering Pipeline

### Pricing & Subscriptions
- Pricing Plans (Tiered, Subscription, Access Tiers, Fractional Ownership, Bulk)
- Data Freshness Levels
- Subscription Lifecycle
- Pricing Security Controls

### Access Control
- Permission Types (READ, WRITE, DELETE, ADMIN)
- Access Policy Model
- Access Operations

### Analytics
- Analytics Capabilities
- Event Types
- Analytics Security Controls

### API Gateway
- Endpoint Types (REST, GraphQL, Webhook, Proxy)
- Gateway Capabilities
- Gateway Operations
- Gateway Security Controls

### Ledger & Revenue Sharing
- Transaction Types
- Revenue Allocation
- Fractional Ownership
- Ledger Security Controls
- Administrative Operations

### Security Summary
- Authentication & Authorization
- Data Protection
- Audit & Compliance
- Platform Integration Security

### API Reference Summary
- API Domain Groups
- Authentication

---

## 13 - Graph RAG

### Component Overview

### Architecture Overview

### Graph-Enhanced Retrieval
- Retrieval Architecture
- Knowledge Graph Integration
- Vector Store Integration

### Retrieval Patterns
- Entity-Centric Retrieval
- Relationship Traversal Retrieval
- Community-Based Retrieval
- Hybrid Retrieval

### Vector and Graph Hybrid Search
- Dual-Path Query Processing
- Relevance Scoring
- Result Merging Strategies

### Context Assembly
- Context Window Management
- Source Attribution
- Context Ranking and Prioritization

### Session-Based Retrieval
- Session Graph Accumulation
- Conversational Context
- Progressive Refinement

### Security Controls
- Access Control in Retrieval
- Data Isolation
- Query Authorization

### Caching and Performance
- Semantic Cache
- Graph Cache
- Cache Security

### Monitoring and Observability
- Retrieval Quality Metrics
- Performance Monitoring
- Alert Configuration

### Audit Logging
- Retrieval Events
- Security Events
- Compliance Logging

---

## 14 - Trust & Compliance

### Overview

### Shared Responsibility Model
- Responsibility Matrix
- Joint Responsibilities

### Security Operations
- Continuous Security Management
- Patch Management SLAs
- Incident Response
- Incident Communication

### Compliance Management
- Continuous Compliance
- Compliance Activities
- Regulatory Change Management
- Audit Support

### Customer-Specific Controls
- Identity Integration
- Access Control Alignment
- Data Protection Configuration
- Integration Security

### Governance & Transparency
- Dedicated Support
- Transparency Mechanisms
- Change Management
- Periodic Reviews
- Reporting

---

## Quick Reference

### Key Platform Components

| Component                  | Primary Document           | Key Features                                               |
| :------------------------- | :------------------------- | :--------------------------------------------------------- |
| Knowledge Graph            | 03-Knowledge-Fabric        | Entity storage, relationship mapping, traversal queries    |
| Entity Resolution          | 03-Knowledge-Fabric        | Blocking, matching, clustering, golden records             |
| Two-Way Data Flow          | 03-Knowledge-Fabric        | Read/write to source systems, metadata-only storage        |
| Persistent Knowledge Graph | 03-Knowledge-Fabric        | Corporate memory, schema-bounded extraction, provenance    |
| Search Sessions            | 03-Knowledge-Fabric        | Iterative exploration, session graphs, accumulated context |
| Data Observability         | 03-Knowledge-Fabric        | Quality monitoring, freshness, alerts                      |
| Text-to-Pipeline           | 04-Studio                  | Natural language workflow generation, DSL output           |
| DDAs (Data-Driven Agents)  | 04-Studio                  | Schema-bound agents with query plans and placeholders      |
| Widget Types               | 04-Studio                  | SYSTEM and OUTPUT visual interface components              |
| Datasets                   | 04-Studio                  | Structured data collections with file uploads              |
| Utilities                  | 04-Studio                  | Reusable components combining APIs and DDAs                |
| Chain of Agents              | 04-Studio                  | Multi-DDA orchestration with human-in-the-loop             |
| Graph of Agents              | 04-Studio                  | *(Planned)* Non-linear graph orchestration with branching  |
| MCP Integrations           | 04-Studio                  | Managed MCP tool connections (types, instances, credentials) |
| Asset Search               | 04-Studio                  | Semantic search across all Studio asset types              |
| AI Hybrid Planning         | 04-Studio                  | Automatic DDA creation from natural language               |
| Operational Modes          | 04-Studio                  | Five modes from manual to fully automated                  |
| LightLLM Gateway           | 05-AI-LLM                  | Provider-agnostic LLM interface                            |
| LLM Monitoring             | 05-AI-LLM                  | Output consistency, A/B testing, provenance                |
| Asset Catalog              | 12-Exchange                | Data asset marketplace with eight asset types              |
| Wallet & Blockchain        | 12-Exchange                | DAAC token on Ethereum, wallet operations                  |
| Metering & Billing         | 12-Exchange                | Usage tracking, pricing plans, subscription management     |
| Ledger & Revenue           | 12-Exchange                | Double-entry ledger, revenue allocation, settlement        |
| Graph Rule Engine          | 08-Graph-Operations        | Pattern scoring, operational rules                         |
| Graph Workflows            | 08-Graph-Operations        | Entity assessment, investigation processes                 |
| Graph Screening Service    | 08-Graph-Operations        | Watchlist, adverse media, risk screening                   |
| Graph RAG                  | 13-Graph-RAG               | Graph-enhanced retrieval, hybrid search, context assembly  |
| Schema Registry            | 09-Schema-Management       | Schema versioning, validation, binding                     |
| Domain Discovery           | 09-Schema-Management       | Document-to-schema extraction                              |
| Data Hold/Retention        | 10-Compliance-Capabilities | Metadata-based retention, data hold management             |
| API Gateway                | 11-API-Security            | Authentication, rate limiting, routing                     |
| OAuth/Token Management     | 11-API-Security            | Token lifecycle, API keys, scopes                          |
| MCP Lifecycle Management   | 03-Knowledge-Fabric        | API tracking, monitoring, remediation SLAs                 |
| Shared Responsibility      | 14-Trust-Compliance        | DataFab vs. customer responsibilities                      |
| Managed Security Ops       | 14-Trust-Compliance        | Patching SLAs, incident response, compliance               |


### Security Controls by Category

| Category | Documents |
|:---------|:----------|
| Authentication & Access | 02, 03, 04, 09, 10, 11 |
| Encryption & Data Protection | 02, 03, 05, 10, 11 |
| Audit Logging | 03, 04, 05, 08, 09, 10, 11, 13 |
| Network Security | 02, 07, 11 |
| Incident Response | 07, 14 |
| Compliance & Governance | 08, 10, 14 |
| Schema & Data Quality | 04, 09 |
| API Security | 11 |
| Service Continuity | 03, 14 |
| Graph RAG Security | 13 |

### Regulatory Coverage

| Regulation | Primary Documents |
|:-----------|:------------------|
| GDPR | 10-Compliance-Capabilities |
| CCPA/CPRA | 10-Compliance-Capabilities |
| SOC 2 Type II | 10-Compliance-Capabilities |
| HIPAA | 10-Compliance-Capabilities |
| PCI DSS | 10-Compliance-Capabilities |
| EU AI Act | 05-AI-LLM, 10-Compliance-Capabilities |

---
