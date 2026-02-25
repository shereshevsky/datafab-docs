---
layout: default
title: Introduction
---

# DataFab Platform - Documentation

**Version:** 3.2
**Last Updated:** February 2026

---

## Executive Summary

DataFab is an AI-powered data intelligence platform built on a metadata-driven architecture that provides unified access to distributed data assets while maintaining strict security controls. The platform enables natural language interaction across all components, supports configurable automation levels from fully manual to fully automated, integrates with 200+ data sources, and provides a data asset marketplace (Exchange) with blockchain-backed transactions.

**Platform Architecture Components:**

| Component             | Purpose                                                                             | Security Relevance                                                         |
| :-------------------- | :---------------------------------------------------------------------------------- | :------------------------------------------------------------------------- |
| Knowledge Fabric      | Active metadata, knowledge graph, entity resolution, 200+ MCP connectors            | Data access control, credential management, source provenance              |
| Studio                | DDAs (Data-Driven Agents), widgets, datasets, utilities, Chain of Agents, MCP integrations, operational modes | Execution sandboxing, schema-driven processing, human-in-the-loop controls |
| Exchange              | Data asset marketplace, catalog, wallet & blockchain (DAAC), metering, access control | Transaction security, permission enforcement, ledger integrity             |
| AI & LLM Layer        | LightLLM-based inference, provider agnostic, output consistency, model provenance   | Prompt security, schema validation, A/B testing                            |
| DevOps Infrastructure | CI/CD pipelines, deployment automation                                              | Code security, vulnerability management                                    |

**Key Security Characteristics:**

- Defense-in-depth architecture with multiple security layers
- Zero-trust access model with continuous verification
- End-to-end encryption for data in transit and at rest
- Comprehensive audit logging with tamper-evident storage
- Privacy-by-design with data minimization principles
- Compliance-ready controls for GDPR and SOC 2
- Schema-bounded extraction preventing hallucination and ensuring data quality
- Five operational modes enabling configurable human oversight

---

## Platform Capabilities

### Knowledge Fabric

The Knowledge Fabric serves as the foundational data integration and intelligence layer, implementing a metadata-driven architecture that provides unified access while leaving source data in place.

| Capability                 | Description                                                                       |
| :------------------------- | :-------------------------------------------------------------------------------- |
| Persistent Knowledge Graph | Corporate memory with schema-bounded extraction and source provenance             |
| Entity Resolution          | Cross-source entity matching with golden record management                        |
| 200+ MCP Connectors        | Federated queries across databases, SaaS, and data systems                        |
| Two-Way Data Flow          | Read from and write back to source systems                                        |
| Search Sessions            | Iterative exploration with accumulated context                                    |
| Data Observability         | Quality monitoring, freshness tracking, automated alerts                          |

### Studio

The Studio (Helix Studio) provides the development environment for building Data-Driven Agents (DDAs), widgets, datasets, utilities, and multi-agent workflows.

| Capability                | Description                                                                          |
| :------------------------ | :----------------------------------------------------------------------------------- |
| DDA Creation              | Domain-driven flow with schema selection, natural language definition, query plan, and testing |
| Widget Types              | Visual interface components (SYSTEM and OUTPUT types) with dialog/canvas views        |
| Datasets                  | Structured data collections with file uploads, schema enforcement, and draft/publish lifecycle |
| Utilities                 | Reusable components combining external APIs and DDAs with configurable placeholders   |
| Business Domain Discovery | Extract schemas from uploaded documents to define entity structures                   |
| Chain of Agents             | Multi-DDA orchestration with human-in-the-loop review gates                          |
| Graph of Agents             | *(Planned)* Non-linear graph orchestration with branching, parallelism, and cycles   |
| MCP Integrations          | Managed MCP tool connections with types, instances, and credentials                   |
| Asset Search              | Semantic search across all Studio asset types                                         |
| AI Hybrid Planning        | Automatic DDA creation from natural language descriptions                             |
| Operational Modes         | Five modes from traditional platform (Mode 0) to fully automated with audit (Mode 4) |
| Text-to-Pipeline          | Natural language workflow generation with DSL output                                  |

### Exchange

The Exchange component is the platform's data asset marketplace, enabling organizations to publish, discover, acquire, and monetize data assets with blockchain-backed transactions.

| Capability                     | Description                                                                        |
| :----------------------------- | :--------------------------------------------------------------------------------- |
| Asset Catalog                  | Publish, search, and manage eight asset types (agents, widgets, datasets, models, etc.) |
| User Profiles                  | Consumer, provider, and dual-role profiles with verification workflows             |
| Wallet & Blockchain            | DAAC token on Ethereum for purchases, deposits, withdrawals, and transfers         |
| Metering & Billing             | Usage tracking with configurable policies and automated billing                    |
| Pricing & Subscriptions        | Tiered access plans, subscription plans, fractional ownership, bulk purchases      |
| Access Control                 | Resource-level permission policies (READ, WRITE, DELETE, ADMIN)                    |
| API Gateway                    | Managed endpoints (REST, GraphQL, Webhook, Proxy) with logging and rate limiting   |
| Ledger & Revenue Sharing       | Double-entry accounting with revenue allocation, settlement, and reconciliation    |

### AI & LLM Layer

The AI layer provides secure, provider-agnostic LLM integration with comprehensive monitoring and quality controls.

| Capability         | Description                                                       |
| :----------------- | :---------------------------------------------------------------- |
| LightLLM Gateway   | Provider-agnostic interface supporting multiple LLM providers     |
| Output Consistency | Schema-validated extraction and ontology-based execution          |
| Model Provenance   | Tracking of model versions and configurations                     |
| Quality Assurance  | Feedback loops, accuracy monitoring, reasoning chain transparency |

---

## Document Structure

| Document               | Content                                                                             |
| :--------------------- | :---------------------------------------------------------------------------------- |
| 01-Introduction        | Platform overview and security summary                                              |
| 02-Architecture        | System architecture, deployment models, security boundaries                         |
| 03-Knowledge-Fabric    | Knowledge graph, entity resolution, MCP connectors, data integration                |
| 04-Studio              | DDAs (Data-Driven Agents), widgets, datasets, utilities, Chain of Agents, MCP integrations, operational modes |
| 05-AI-LLM              | LLM security, output consistency, model provenance, quality assurance               |
| 06-CI-CD               | CI/CD pipeline security                                                             |
| 07-Security-Operations | SOC, monitoring, and incident response                                              |
| 08-Graph-Operations    | Graph operations, rule engine, query processing                                     |
| 09-Schema-Management   | Business domain discovery, schema registry                                          |
| 10-Compliance-Capabilities | Platform compliance features, retention management                             |
| 11-API-Security        | API gateway, authentication, rate limiting                                          |
| 12-Exchange            | Data asset marketplace, catalog, wallet & blockchain, metering, access control      |
| 13-Graph-RAG           | Graph-based retrieval augmented generation capabilities                             |

---

## Security Principles

DataFab implements the following core security principles:

| Principle              | Implementation                                                                        |
| :--------------------- | :------------------------------------------------------------------------------------ |
| Defense in Depth       | Multiple independent security layers across all components                            |
| Least Privilege        | Minimum necessary access granted, permission propagation controls                     |
| Zero Trust             | All requests are authenticated regardless of source, with continuous verification     |
| Data Minimization      | Only essential data collected; metadata-only architecture leaves source data in place |
| Encryption Everywhere  | Data encrypted at rest and in transit with AES-256 and TLS 1.3                        |
| Audit Everything       | Comprehensive logging with tamper-evident storage and full provenance                 |
| Schema-Driven Security | All data extraction and processing bounded by user-defined schemas                    |
| Human-in-the-Loop      | Configurable automation levels with escalation and approval workflows                 |

---

## Operational Modes

The platform supports five operational modes enabling organizations to balance automation with human oversight:

| Mode | Name                       | Description                                                         |
| :--- | :------------------------- | :------------------------------------------------------------------ |
| 0    | Traditional Platform       | No AI agents; manual investigation and analysis                     |
| 1    | AI-Assisted Manual         | Agents in suggest-only mode; all decisions require human approval   |
| 2    | Routine Automation         | Agents handle routine tasks; humans focus on analysis and decisions |
| 3    | Autonomous with Escalation | Full investigation automation; escalation on exceptions             |
| 4    | Fully Automated with Audit | End-to-end automation; post-investigation human audits              |

---

## Regulatory Compliance

The platform is designed to support compliance with:

| Regulation                        | Coverage                                                        |
| :-------------------------------- | :-------------------------------------------------------------- |
| GDPR                              | Data subject rights, consent management, data minimization      |
| CCPA/CPRA                         | California privacy requirements                                 |
| SOC 2                             | Security, availability, processing integrity                    |
| FCA Requirements                  | Financial services regulatory compliance                        |
| Enterprise Data Standards         | Industry best practices for data governance                      |

---

## Contact

For security inquiries or to request additional documentation, please contact the DataFab security team through your account representative.
