---
layout: default
title: Home
---

# DataFab Platform Documentation

Welcome to the DataFab platform architecture documentation.

---

## Overview

DataFab is an AI-powered data intelligence platform built on a metadata-driven architecture that provides unified access to distributed data assets while maintaining strict security controls. The platform enables natural language interaction across all components, supports configurable automation levels, and integrates with 200+ data sources through its Knowledge Fabric, Studio, Exchange, and Graph RAG modules.

---

## Documentation

| Document                                                    | Description                                                             | Version |
| :---------------------------------------------------------- | :---------------------------------------------------------------------- | :-----: |
| [Introduction](./01-Introduction.md)                        | Platform overview, capabilities, and security summary                   |   1.0   |
| [Architecture](./02-Architecture.md)                        | System architecture, deployment models, security boundaries             |   1.0   |
| [Knowledge Fabric](./03-Knowledge-Fabric.md)                | Knowledge graph, entity resolution, MCP connectors, data integration    |   1.0   |
| [Studio](./04-Studio.md)                                    | DDAs, widgets, datasets, utilities, Chain of Agents, MCP integrations     |   2.0   |
| [AI & LLM](./05-AI-LLM.md)                                  | LLM security, output consistency, model provenance                      |   1.0   |
| [CI/CD](./06-CI-CD.md)                                      | CI/CD pipeline security                                                 |   1.0   |
| [Security Operations](./07-Security-Operations.md)          | SOC, monitoring, incident response                                      |   1.0   |
| [Graph Operations](./08-Graph-Operations.md)                | Graph rule engine, pattern detection, graph workflows                   |   1.0   |
| [Schema Management](./09-Schema-Management.md)              | Business domain discovery, schema registry                              |   1.0   |
| [Compliance Capabilities](./10-Compliance-Capabilities.md)  | Platform compliance features, data hold, retention                      |   1.0   |
| [API Security](./11-API-Security.md)                        | API gateway, authentication, rate limiting                              |   1.0   |
| [Exchange](./12-Exchange.md)                                | Data asset marketplace, catalog, wallet & blockchain, metering, access |   1.0   |
| [Graph RAG](./13-Graph-RAG.md)                              | Graph-enhanced retrieval, hybrid search, context assembly               |   1.0   |
| [Trust & Compliance](./14-Trust-Compliance.md)              | Managed deployment security, compliance, and governance                 |   1.0   |


---

## Platform Components

### Knowledge Fabric
The foundational data integration layer with 200+ MCP connectors, persistent knowledge graph, entity resolution, and enterprise data integration across structured, semi-structured, and unstructured sources.

### Studio
Development environment for building Data-Driven Agents (DDAs), widgets, datasets, utilities, and multi-agent workflows (Chain of Agents, with Graph of Agents planned). Features domain-driven creation flows, MCP integrations, AI hybrid planning, semantic asset search, and five configurable operational modes.

### Exchange
Data asset marketplace enabling organizations to publish, discover, acquire, and monetize data assets. Features blockchain-backed transactions (DAAC token on Ethereum), usage-based metering, tiered access plans, and a double-entry ledger for transparent revenue sharing.

### Graph RAG
Graph-enhanced retrieval augmented generation combining vector similarity search with knowledge graph traversal for contextually rich, relationship-aware responses.

### Graph Operations
Operational intelligence module providing graph-based pattern detection, rule engines, workflow automation, entity assessment, and anomaly scoring across connected data.

### AI & LLM Layer
Provider-agnostic LLM integration via LightLLM with output consistency controls, model provenance tracking, and quality assurance.

---

## Quick Links

- [Table of Contents](./00-Table-of-Contents.md) - Complete navigation with all sections
- [Security Principles](./01-Introduction.md#security-principles) - Core security approach
- [Operational Modes](./04-Studio.md#operational-modes) - Automation levels (Mode 0-4)
- [Graph RAG Architecture](./13-Graph-RAG.md#architecture-overview) - Retrieval patterns and hybrid search

---

## Security Highlights

| Principle | Implementation |
|:----------|:---------------|
| Defense in Depth | Multiple independent security layers |
| Zero Trust | All requests authenticated regardless of source |
| Encryption Everywhere | AES-256 at rest, TLS 1.3 in transit |
| Schema-Driven Security | All extraction bounded by user-defined schemas |
| Human-in-the-Loop | Configurable automation with escalation workflows |

---

## Regulatory Compliance

The platform supports compliance with GDPR, CCPA/CPRA, HIPAA, PCI DSS, SOC 2, EU AI Act, and industry-specific standards.

---

## Contact

For security inquiries or additional documentation, please contact the DataFab security team through your account representative.

---
