---
layout: default
title: Graph RAG
---

# DataFab Graph RAG

**Version:** 3.0
**Last Updated:** February 2026

---

## Component Overview

Graph RAG (Retrieval-Augmented Generation) represents DataFab's advanced retrieval architecture that combines graph databases with semantic search to provide contextually rich, multi-faceted information for large language model reasoning. Unlike traditional RAG systems that rely solely on vector embeddings, Graph RAG leverages the explicit relationship structure of DataFab's knowledge graph to improve retrieval quality, context assembly, and reasoning accuracy.

**Core Capabilities:**

| Capability                | Description                                                    |
| :------------------------ | :------------------------------------------------------------- |
| Graph-Enhanced Retrieval  | Combines graph navigation with semantic search                 |
| Entity-Centric Queries    | Retrieve full context around entities and relationships        |
| Relationship Traversal    | Navigate multi-hop relationships for comprehensive context     |
| Community Detection       | Identify and retrieve hierarchical clusters of related entities |
| Hybrid Search             | Blend vector similarity with graph structure scoring           |
| Context Assembly          | Automatically structure retrieved context for LLM consumption  |
| Multi-Turn Awareness      | Build context across conversational turns using graph memory   |
| Provenance Tracking       | Maintain source lineage for all retrieved information          |
| Access-Controlled Retrieval | Enforce security constraints during graph traversal            |
| Performance Optimization  | Query planning and caching for sub-second retrieval            |

---

## Architecture Overview

```
┌─────────────────────────────────────────────────────────────────────────┐
│                        CLIENT LAYER                                     │
│  ┌────────────────────┐  ┌────────────────────┐  ┌────────────────────┐ │
│  │  LLM Integration   │  │  Exchange Interface│  │   Analytics UI     │ │
│  └─────────┬──────────┘  └─────────┬──────────┘  └─────────┬──────────┘ │
└────────────┼─────────────────────────┼──────────────────────┼────────────┘
             │                         │                      │
             ▼                         ▼                      ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                       GRAPH RAG API GATEWAY                             │
│  ┌─────────────────────────────────────────────────────────────────┐    │
│  │  Authentication │ Rate Limiting │ Query Validation │ Logging    │    │
│  └─────────────────────────────────────────────────────────────────┘    │
└────────────┼──────────────────────────────────────────────────────────┬─┘
             │                                                          │
             ▼                                                          │
┌─────────────────────────────────────────────────────────────────────────┐
│                    GRAPH RAG RETRIEVAL ENGINE                           │
│                                                                         │
│  ┌─────────────────────────────────────────────────────────────────┐    │
│  │            QUERY INTENT & SEMANTICS ANALYSIS                    │    │
│  │  • Intent Detection  • Entity Identification  • Relationship    │    │
│  │    • Scope Analysis   • Temporal Constraints   • Filters        │    │
│  └─────────────────────────────────────────────────────────────────┘    │
│                              │                                          │
│  ┌──────────────────────────┴──────────────────────────────────────┐    │
│  │           HYBRID RETRIEVAL STRATEGY SELECTOR                    │    │
│  │  ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌──────────────────────┐  │    │
│  │  │ Entity- │ │Relation-│ │Community│ │  Adaptive Weighting  │  │    │
│  │  │ Centric │ │  Shift  │ │ Based   │ │  (Query-dependent)   │  │    │
│  │  └─────────┘ └─────────┘ └─────────┘ └──────────────────────┘  │    │
│  └─────────────────────────┬──────────────────────────────────────┘    │
│                            │                                           │
│  ┌─────────────────────────▼──────────────────────────────────────┐    │
│  │           GRAPH TRAVERSAL & VECTOR SEARCH                      │    │
│  │  ┌─────────────────┐     ┌────────────────────────────┐        │    │
│  │  │ Graph Queries   │     │  Vector Similarity Search  │        │    │
│  │  │ • Path Finding  │     │  • Embedding Lookup        │        │    │
│  │  │ • Subgraph      │     │  • Semantic Matching       │        │    │
│  │  │ • Aggregations  │     │  • Relevance Scoring       │        │    │
│  │  └─────────────────┘     └────────────────────────────┘        │    │
│  │         │                                    │                 │    │
│  │         └────────────────┬───────────────────┘                 │    │
│  │                          ▼                                     │    │
│  │         ┌──────────────────────────────────┐                  │    │
│  │         │  RESULT FUSION & RANKING         │                  │    │
│  │         │  • Score Normalization           │                  │    │
│  │         │  • Graph-Aware Re-ranking        │                  │    │
│  │         │  • Relevance Combination         │                  │    │
│  │         │  • Diversity Optimization        │                  │    │
│  │         └──────────────────────────────────┘                  │    │
│  └─────────────────────────┬──────────────────────────────────────┘    │
│                            │                                           │
│  ┌─────────────────────────▼──────────────────────────────────────┐    │
│  │           ACCESS CONTROL & FILTERING                           │    │
│  │  • Permission Propagation  • Tenant Isolation  • Field Masking │    │
│  └─────────────────────────┬──────────────────────────────────────┘    │
│                            │                                           │
└────────────┬───────────────▼──────────────────────┬────────────────────┘
             │                                      │
             ▼                                      ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                  CONTEXT ASSEMBLY & LLM PREPARATION                     │
│  ┌─────────────────┐  ┌─────────────────┐  ┌──────────────────────┐     │
│  │ Context Builder │  │ Provenance Join │  │  Output Formatter    │     │
│  │ (Hierarchical)  │  │ (Citation Info) │  │  (Template-based)    │     │
│  └─────────────────┘  └─────────────────┘  └──────────────────────┘     │
└────────────┬────────────────────────────────────────────────────────────┘
             │
             ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                     CACHING & OPTIMIZATION LAYER                        │
│  ┌────────────────┐  ┌──────────────┐  ┌─────────────────────────┐      │
│  │  Query Cache   │  │ Result Cache │  │  Graph Index Caching    │      │
│  │  (Exact/Fuzzy) │  │  (Semantic)  │  │  (Subgraph Memoization) │      │
│  └────────────────┘  └──────────────┘  └─────────────────────────┘      │
└─────────────────────────────────────────────────────────────────────────┘
             │
             ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                    KNOWLEDGE GRAPH STORAGE LAYER                        │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  ┌────────────┐   │
│  │   Entities   │  │ Relationships│  │   Properties │  │ Vector Idx │   │
│  │   (Nodes)    │  │   (Edges)    │  │  (Metadata)  │  │ (Embeddings)   │
│  └──────────────┘  └──────────────┘  └──────────────┘  └────────────┘   │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## Graph-Enhanced Retrieval

Traditional RAG systems retrieve context based primarily on semantic similarity between the query and stored vectors. Graph RAG enhances this approach by leveraging the explicit structure of the knowledge graph to understand entity relationships, navigate semantic networks, and assemble context that reflects the actual data topology.

### Retrieval Advantages

| Advantage | Description | Example |
|:----------|:------------|:--------|
| Relationship Awareness | Understands how entities connect across the graph | Query about Person A automatically includes related Organizations, Addresses, and Identifiers |
| Multi-Hop Context | Can traverse multiple relationship degrees for comprehensive context | Query about a merger includes 5-hop relationship chains showing how entities are connected |
| Structural Bias | Weights entities based on their role in the graph structure | Central hub entities score higher than peripheral ones |
| Coherence | Retrieved context naturally aligns because it comes from connected subgraphs | All retrieved information about a topic comes from a cohesive cluster |
| Disambiguation | Graph structure helps disambiguate entities with similar names | Different "John Smith" entities are kept separate based on relationship patterns |

---

## Retrieval Patterns

Graph RAG supports multiple retrieval strategies optimized for different query types. These patterns can be combined and weighted adaptively based on the current query.

### Entity-Centric Retrieval

When users query for information about a specific entity, entity-centric retrieval returns the complete context around that entity.

**Process:**
1. Identify primary entity from query
2. Retrieve entity attributes and properties
3. Fetch all direct relationships (one-hop)
4. Retrieve connected entity contexts
5. Assemble hierarchically with primary entity at center

**Example Query:** "Tell me everything about Organization X"

| Step | Result |
|:-----|:--------|
| Entity Lookup | Organization X (EIN, legal name, jurisdiction) |
| Direct Relationships | 47 related entities: 12 Person, 15 Organization, 8 Address, 12 Document |
| Relationship Details | OWNS (5), CONTROLS (3), LOCATED_AT (2), REPRESENTS (8), EMPLOYS (29) |
| Connected Entities | Full context for each related entity |
| Assembly | Hierarchical structure with Org X at center, relationships as next level, related entities as leaves |

**Security Considerations:**
- All relationships are filtered based on user access permissions
- Related entities inherit access controls from parent
- Masked fields are propagated consistently

### Relationship-Traversal Retrieval

For queries that ask about connections between entities, relationship-traversal retrieval finds paths and patterns that connect them.

**Process:**
1. Identify source and target entities
2. Find all paths connecting them (with configurable max depth)
3. Retrieve properties of each entity on the path
4. Score paths by relevance and specificity
5. Return top paths with full context

**Example Query:** "How is Person A connected to Organization B?"

| Path Length | Description | Probability |
|:------------|:------------|:------------|
| 1 | Direct employment relationship | A EMPLOYS B |
| 2 | Through ownership | A OWNS C, C LOCATED_AT B |
| 3 | Through representation | A REPRESENTS D, D CONTROLS B |
| 4+ | Indirect connections | Multiple intermediate entities |

**Ranking Factors:**
- Path length (shorter paths often more direct)
- Relationship types (some relationships more significant)
- Temporal validity (historical vs. current)
- Data quality (confidence scores)

### Community-Based Retrieval

Communities are hierarchically organized clusters of related entities detected through graph analysis. Community-based retrieval identifies the community containing query entities and returns the complete community context.

**Community Structure:**

| Level | Description | Size |
|:------|:------------|:-----|
| Level 1 (Global) | Top-level communities (major business units, jurisdictions) | 5-10 entities each |
| Level 2 (Regional) | Sub-communities within level 1 | 10-50 entities each |
| Level 3 (Local) | Tight clusters of closely connected entities | 20-100 entities each |
| Level 4 (Micro) | Individual clusters of related records | 5-15 entities each |

**Example Query:** "What is the complete ownership structure of Organization X?"

1. Locate Organization X in graph
2. Identify its community at appropriate level
3. Retrieve all entities in that community
4. Return full relationship structure within community
5. Optionally include connections to adjacent communities

**Security Constraints:**
- Communities filtered per user permissions
- Only accessible community portions returned
- Cross-community connections restricted based on user access

### Hybrid Retrieval Pattern

Real-world queries often benefit from combining multiple retrieval patterns. The Hybrid Retrieval Pattern intelligently selects and weights multiple strategies based on query characteristics.

**Adaptive Strategy Selection:**

| Query Characteristic | Pattern Weight | Example |
|:---------------------|:--------------|:---------|
| Single entity focus | Entity-Centric: 70% | "Tell me about Organization X" |
| Connection query | Relationship-Shift: 80% | "How are X and Y related?" |
| Community scope | Community-Based: 75% | "Show the ownership chain" |
| Complex multi-faceted | Hybrid: 40/30/30 | "Analyze the corporate structure and connections" |
| Temporal aspects | Relationship-Traversal: 60% | "How has this relationship evolved?" |

**Dynamic Weight Adjustment:**
Weights are adjusted based on:
- Query complexity (number of entities mentioned)
- Result overlap (to maximize information diversity)
- User interaction patterns (learned from session history)
- Data sparsity (available information density in graph)

---

## Vector + Graph Hybrid Search

Graph RAG combines traditional vector embeddings with graph structure scoring to produce superior retrieval results.

### Dual Retrieval Process

```
┌──────────────────────────────────────────────────────────┐
│                    USER QUERY                            │
└────────────────────┬─────────────────────────────────────┘
                     │
         ┌───────────┴───────────┐
         │                       │
         ▼                       ▼
┌──────────────────┐     ┌──────────────────────┐
│ VECTOR SEARCH    │     │  GRAPH ANALYSIS      │
│                  │     │                      │
│ 1. Embed query   │     │ 1. Parse intent      │
│ 2. Find similar  │     │ 2. Identify entities │
│    embeddings    │     │ 3. Build subgraph    │
│ 3. Score by      │     │ 4. Calculate centrality
│    similarity    │     │ 5. Score structure   │
│                  │     │                      │
└────────┬─────────┘     └──────────┬───────────┘
         │ Similarity Scores        │ Structure Scores
         │                          │
         └───────────────┬──────────┘
                         │
                         ▼
         ┌──────────────────────────────┐
         │   SCORE NORMALIZATION        │
         │   • Min-Max scaling          │
         │   • Percentile mapping       │
         │   • Confidence calibration   │
         └────────────────┬─────────────┘
                          │
         ┌────────────────┴────────────────┐
         │                                 │
         ▼                                 ▼
   ┌──────────────────┐      ┌────────────────────┐
   │ FUSION WEIGHTING │      │  DIVERSITY CHECK   │
   │ α = 0.6 vector   │      │ Remove redundant   │
   │ β = 0.4 graph    │      │ high-overlap items │
   └────────┬─────────┘      └────────┬───────────┘
            │                         │
            └───────────────┬─────────┘
                            │
                            ▼
               ┌────────────────────────┐
               │  FINAL RANKING         │
               │  Top-K Results         │
               └────────────────────────┘
```

### Score Fusion Strategy

| Component | Weight | Calculation | Purpose |
|:----------|:-------|:------------|:--------|
| Vector Similarity | 60% | Cosine distance in embedding space | Semantic relevance to query |
| Entity Centrality | 20% | PageRank-style importance score | Entity prominence in graph |
| Relationship Score | 15% | Proximity to query entities | Connection strength |
| Temporal Freshness | 5% | Recency of last update | Data currency |

**Adaptive Weight Tuning:**
Weights automatically adjust based on:
- Query type (single entity vs. relationship queries)
- Graph sparsity (adjust entity centrality if few connections)
- Domain-specific importance (allow customer override per entity type)

### Vector Index Integration

| Component | Purpose | Update Frequency |
|:----------|:--------|:-----------------|
| Entity Embeddings | Vector representation of entity attributes | On entity update |
| Relationship Embeddings | Vector representation of connection types | On relationship schema change |
| Context Embeddings | Vector representation of surrounding context | Weekly |
| Query Embeddings | Runtime representation of incoming queries | Per query |

**Embedding Models:**
- Primary: Sentence transformers (general domain understanding)
- Domain-Specific: Fine-tuned models per customer (when available)
- Fallback: BM25 lexical matching (when embeddings unavailable)

---

## Context Assembly

Once Graph RAG has retrieved relevant entities and relationships, the Context Assembly stage structures this information for consumption by language models.

### Context Hierarchy

Retrieved context is organized hierarchically to maximize LLM token efficiency while preserving information relationships:

```
┌─────────────────────────────────────────────┐
│  LEVEL 0: PRIMARY ENTITY                    │
│  (1-3 sentences, key attributes)            │
│  • Name, ID, type                           │
│  • Most important status/classification     │
└─────────────────────────────────────────────┘
              ▼
┌─────────────────────────────────────────────┐
│  LEVEL 1: DIRECT RELATIONSHIPS              │
│  (1-2 sentences per relationship)           │
│  • Related entities and connection types    │
│  • Key attributes of related entities      │
└─────────────────────────────────────────────┘
              ▼
┌─────────────────────────────────────────────┐
│  LEVEL 2: RELATIONSHIP DETAILS              │
│  (1 sentence per significant connection)    │
│  • Temporal validity                        │
│  • Relationship properties                  │
│  • Data quality/confidence                  │
└─────────────────────────────────────────────┘
              ▼
┌─────────────────────────────────────────────┐
│  LEVEL 3: SUPPORTING CONTEXT (OPTIONAL)     │
│  (Only if space available in LLM context)   │
│  • Historical relationships                 │
│  • Statistical properties                   │
│  • External enrichment                      │
└─────────────────────────────────────────────┘
```

### Smart Context Truncation

Context is sized dynamically based on:

| Factor | Impact | Example |
|:-------|:-------|:--------|
| LLM Context Window | Absolute limit | Limit to 4K tokens for 8K context window |
| Query Complexity | Allocation | 10 entities: use ~2K tokens; 100 entities: use ~7K tokens |
| Result Quality | Adjustment | High-confidence results: fewer tokens needed; ambiguous: more context |
| Conversational State | Carryover | Multi-turn query: reserve tokens for conversation history |

### Provenance Integration

Each piece of retrieved context includes provenance information—the source system and document reference from which it originated:

**Provenance Fields:**

| Field | Content | Purpose |
|:------|:--------|:--------|
| Source System | Connector ID or source name | Identifies originating system |
| Document ID | Document, record, or asset ID | Allows user to locate source |
| Document Title | Human-readable reference | Quick identification |
| Extraction Reference | Page, paragraph, cell range, or section | Precise location within document |
| Confidence Score | 0-1 confidence of extraction | Indicates data quality |
| Last Updated | Timestamp of last sync | Shows data currency |

**Citation Generation:**
The system automatically generates citations for retrieved information, enabling users to verify facts and audit data lineage.

---

## Ranking and Relevance

Graph RAG employs multiple ranking strategies to ensure the most relevant entities and relationships surface in retrieval results.

### Ranking Algorithm Architecture

```
┌────────────────────────────────────────────┐
│         INITIAL CANDIDATES                 │
│  (From graph traversal + vector search)    │
└───────────────┬────────────────────────────┘
                │
                ▼
┌────────────────────────────────────────────┐
│      SCORE CALCULATION                     │
│  • Semantic similarity (vector)            │
│  • Graph centrality                        │
│  • Relationship strength                   │
│  • Type-specific scoring                   │
│  • Temporal factors                        │
└───────────────┬────────────────────────────┘
                │
                ▼
┌────────────────────────────────────────────┐
│    GRAPH-AWARE RE-RANKING                  │
│  • Coherence clustering (group related)    │
│  • Diversity scoring (reduce redundancy)   │
│  • Path-based importance                   │
│  • Community structure alignment           │
└───────────────┬────────────────────────────┘
                │
                ▼
┌────────────────────────────────────────────┐
│    PERSONALIZATION & CONTEXT               │
│  • User interaction history                │
│  • Session context                         │
│  • Access control filtering                │
│  • Data quality thresholds                 │
└───────────────┬────────────────────────────┘
                │
                ▼
┌────────────────────────────────────────────┐
│        FINAL RESULT SET                    │
│  (Top-K ranked entities with scores)       │
└────────────────────────────────────────────┘
```

### Ranking Factors

| Factor | Weight | Description | Tuning |
|:-------|:-------|:------------|:--------|
| Semantic Relevance | 35% | Vector similarity to query | Per-model tuning |
| Entity Importance | 25% | PageRank/centrality in graph | Per-domain calibration |
| Relationship Specificity | 20% | How directly connected to query | Auto-calculated |
| Data Freshness | 10% | Recency of last update | Configurable decay |
| Quality Score | 5% | Source confidence/accuracy | Per-source calibration |
| Access Score | 5% | User permission level | Dynamic per user |

### Type-Specific Scoring

Different entity and relationship types can have custom scoring functions:

**Entity Type Scoring:**

| Type | Priority | Special Considerations |
|:-----|:---------|:----------------------|
| Person | High | Include role/title context |
| Organization | High | Include jurisdiction/status |
| Relationship | Medium | Weight by relationship type |
| Document | Medium | Weight by document type/classification |
| Address | Low | Weight by address type (primary vs. alternate) |

**Relationship Type Scoring:**

| Relationship | Base Score | Context Impact |
|:-------------|:-----------|:--------------|
| OWNS | 0.95 | Very high relevance in ownership queries |
| CONTROLS | 0.90 | High relevance in governance queries |
| EMPLOYS | 0.85 | High relevance in organizational queries |
| LOCATED_AT | 0.70 | Medium relevance, used for disambiguation |
| RELATED_TO | 0.60 | Lower relevance, suggests weaker connection |

---

## Session-Based Retrieval

Graph RAG maintains session context across multiple query turns, allowing the system to incrementally build understanding and refer back to previously discovered information.

### Session Graph Construction

```
┌──────────────────────────────────────────────────┐
│         SESSION INITIALIZATION                   │
│         (User starts exploration)                │
└────────────────┬─────────────────────────────────┘
                 │
                 ▼
    ┌────────────────────────────┐
    │  SESSION GRAPH (Empty)     │
    │                            │
    │  Entities: {}              │
    │  Relationships: {}         │
    │  History: []               │
    └────────────────┬───────────┘
                     │
                     ▼
    ┌────────────────────────────┐
    │  USER QUERY 1              │
    │  "Find Person X"           │
    └────────────────┬───────────┘
                     │
                     ▼
    ┌────────────────────────────┐
    │  RETRIEVAL                 │
    │  • Query graph for Person X│
    │  • Add to Session Graph    │
    │  • Score and rank          │
    │  • Assemble context        │
    └────────────────┬───────────┘
                     │
                     ▼
    ┌────────────────────────────┐
    │  SESSION UPDATE            │
    │                            │
    │  Entities: {Person X, ...} │
    │  Relationships: {...}      │
    │  History: [Query 1]        │
    └────────────────┬───────────┘
                     │
                     ▼
    ┌────────────────────────────┐
    │  USER QUERY 2              │
    │  "Who does Person X work  │
    │   with?"                   │
    └────────────────┬───────────┘
                     │
                     ▼
    ┌────────────────────────────┐
    │  CONTEXT-AWARE RETRIEVAL   │
    │  • Use Person X from       │
    │    session as base         │
    │  • Find EMPLOYS rels       │
    │  • Add new entities        │
    │  • Reference existing      │
    │    session data            │
    └────────────────┬───────────┘
                     │
                     ▼
    ┌────────────────────────────┐
    │  SESSION UPDATE            │
    │                            │
    │  Entities: {+new people}   │
    │  Relationships: {+new rels}│
    │  History: [Query 1, Query2]│
    └────────────────────────────┘
```

### Session Features

| Feature | Description | Benefit |
|:--------|:------------|:--------|
| Entity Memory | Discovered entities available for future queries | No need to re-discover; queries build on each other |
| Relationship Memory | Discovered relationships cached in session | Faster traversal for related queries |
| Query History | Previous queries and results preserved | User can reference earlier findings |
| Conversation Context | LLM has access to session context | Answers remain coherent across turns |
| Implicit References | User can refer to "it" or "this" from previous query | More natural conversation flow |

### Session Timeout and Persistence

| Parameter | Value | Rationale |
|:----------|:-------|:----------|
| Active Session TTL | 24 hours | Long enough for typical investigation sessions |
| Idle Session Timeout | 30 minutes | Clear memory of idle sessions to prevent confusion |
| Session Persistence | Persistent until timeout | Users can continue sessions across applications |
| Session Archive | 90-day retention | Historical session data available for audit |

### Session Security

| Control | Implementation |
|:--------|:---------------|
| User Isolation | Sessions are user-specific and tenant-scoped |
| Permission Propagation | Session context inherits user access controls |
| Incremental Filtering | As permissions change, session graph is dynamically filtered |
| Audit Logging | All session queries and discoveries logged for compliance |

---

## Security Controls

Graph RAG enforces comprehensive security controls to ensure data is retrieved only by authorized users and that access constraints are maintained throughout the retrieval and context assembly process.

### Access-Filtered Retrieval

Every graph traversal respects user access permissions:

**Retrieval Security Model:**

1. **Query Authentication**: User identity verified via OAuth/JWT
2. **Permission Lookup**: User roles and permissions loaded from identity store
3. **Graph Filtering**: Traversal algorithm only visits permitted entities/relationships
4. **Result Filtering**: Final results include only data user is authorized to see
5. **Field Masking**: Sensitive fields masked based on field-level access controls
6. **Audit Logging**: All retrievals logged with user ID, query, and results

**Permission Enforcement:**

| Check | Timing | Action |
|:------|:--------|:--------|
| Entity Access | Graph traversal | Skip unauthorized entities |
| Relationship Access | Traversal | Skip relationships user cannot access |
| Field Access | Result assembly | Mask restricted fields |
| Bulk Operations | Query planning | Reject if > threshold of results masked |

### Tenant Isolation

In multi-tenant deployments, Graph RAG ensures complete isolation between tenants:

| Isolation Layer | Implementation |
|:--------|:---------------|
| Graph Partitioning | Separate graph partitions per tenant |
| Query Scoping | All queries automatically scoped to tenant |
| Index Isolation | Separate vector indices per tenant |
| Cache Isolation | Tenant-specific cache keys |
| Credential Vault | Per-tenant credential isolation |

### Field-Level Masking

Sensitive fields are masked based on user permissions:

**Masking Strategies:**

| Strategy | Example | Use Case |
|:---------|:--------|:---------|
| Full Masking | SSN shown as "***-**-****" | Highly sensitive fields |
| Partial Masking | Email shown as "j***@example.com" | PII fields |
| Hash Masking | Phone shown as SHA hash | For matching without disclosure |
| Redaction | Entire field omitted | When user has no access |
| Tokenization | Consistent token for same value | For analytics without disclosure |

### Injection Prevention

Graph RAG prevents multiple attack vectors:

**Attack Prevention:**

| Attack Type | Prevention | Implementation |
|:------------|:-----------|:-----------------|
| Query Injection | Parameterized graph queries | All user input treated as data, not code |
| Traversal Injection | Graph shape validation | Unauthorized relationships cannot be created |
| Prompt Injection | Context escaping | Retrieved text escaped before LLM consumption |
| Path Injection | Path analysis | Invalid paths rejected during traversal |
| Filtering Bypass | Multi-layer filtering | Checks applied at retrieval, assembly, and output |

---

## Performance and Caching

Graph RAG includes comprehensive caching and optimization strategies to deliver sub-second retrieval even for complex queries across large graphs.

### Query Execution Planning

```
┌──────────────────────────────┐
│    INCOMING QUERY            │
│  "Show complete ownership"   │
└────────────┬─────────────────┘
             │
             ▼
┌──────────────────────────────┐
│  QUERY ANALYSIS              │
│  • Complexity: High          │
│  • Expected results: 50-100  │
│  • Depth: 5 hops             │
└────────────┬─────────────────┘
             │
             ▼
┌──────────────────────────────┐
│  EXECUTION PLAN GENERATION   │
│  1. Cache lookup             │
│  2. Vector search (parallel) │
│  3. Graph traversal (batch)  │
│  4. Result fusion            │
│  5. Context assembly         │
└────────────┬─────────────────┘
             │
             ▼
┌──────────────────────────────┐
│  PLAN OPTIMIZATION           │
│  • Reorder steps for speed   │
│  • Identify precalc data     │
│  • Set resource budgets      │
│  • Estimate latency          │
└────────────┬─────────────────┘
             │
             ▼
┌──────────────────────────────┐
│  EXECUTION                   │
│  (Target: < 500ms)           │
└──────────────────────────────┘
```

### Cache Architecture

| Cache Layer | Type | Purpose | TTL |
|:-----------|:-----|:--------|:-----|
| Query Result Cache | Semantic | Identical/similar queries | 24 hours |
| Entity Cache | Attribute | Entity attribute lookups | 1 hour |
| Relationship Cache | Relationship | Relationship queries | 1 hour |
| Subgraph Cache | Computation | Frequently traversed subgraphs | 12 hours |
| Vector Index Cache | Search | Vector similarity results | 6 hours |
| Embedding Cache | Computation | Query embeddings | Session |

### Cache Invalidation

| Trigger | Scope | Latency |
|:--------|:------|:--------:|
| Entity Update | Entity + neighbors | Immediate |
| Relationship Change | Both entities | Immediate |
| Access Control Change | All caches for user | 5 minutes |
| External Enrichment | Affected entities | 30 minutes |
| Batch Import | Affected subgraphs | 1 hour |
| TTL Expiration | Individual entry | Per TTL |

### Graph Index Optimization

**Index Types:**

| Index | Purpose | Lookup Time |
|:------|:--------|:-----------|
| Entity ID Index | Direct entity lookup | < 1ms |
| Entity Type Index | All entities of type | < 10ms |
| Relationship Type Index | All relationships of type | < 10ms |
| Full-Text Index | Natural language search | < 50ms |
| Vector Index | Semantic similarity | < 100ms |
| Temporal Index | Time-range queries | < 5ms |

**Query Optimization Techniques:**

1. **Early Filtering**: Apply access controls before traversal
2. **Index-First**: Use indices before graph traversal
3. **Batch Operations**: Group similar queries
4. **Approximate Answers**: Use statistical summaries when exact not needed
5. **Progressive Disclosure**: Return top results immediately, refine as time allows

---

## Monitoring

Graph RAG includes comprehensive monitoring to track retrieval quality, performance, and system health.

### Retrieval Quality Metrics

| Metric | Description | Target |
|:-------|:------------|:--------|
| Precision | Fraction of retrieved results relevant to query | > 85% |
| Recall | Fraction of relevant results actually retrieved | > 80% |
| NDCG@10 | Normalized discounted cumulative gain at rank 10 | > 0.75 |
| Mean Reciprocal Rank | Rank of first relevant result | < 3 |
| Serendipity | Fraction of results user found surprising but valuable | > 20% |

### Performance Monitoring

| Metric | Description | Alert Threshold |
|:-------|:------------|:-----------------|
| Query Latency (P95) | 95th percentile execution time | > 500ms |
| Cache Hit Rate | Fraction of queries served from cache | < 40% |
| Traversal Depth | Average graph traversal depth | > 6 hops |
| Vector Search Latency | Time to perform similarity search | > 100ms |
| Context Assembly Time | Time to build LLM context | > 200ms |

### System Health Monitoring

| Monitor | Description | Normal Range |
|:--------|:------------|:-------------|
| Index Freshness | Age of indices vs. source data | < 5 minutes |
| Cache Memory Usage | Memory consumed by caches | < 60% |
| Vector Index Size | Bytes consumed by embedding indices | Monitored |
| Query Queue Depth | Pending queries awaiting execution | < 100 |
| API Response Errors | Failed retrieval requests | < 1% |

### Logging

| Log Type | Content | Retention |
|:---------|:--------|:----------:|
| Query Logs | Query intent, results, timing, user | 1 year |
| Performance Logs | Latency, cache hits, execution plans | 90 days |
| Error Logs | Failures, timeouts, exceptions | 2 years |
| Audit Logs | User queries, entities accessed, timing | 2 years |
| Security Logs | Permission denials, anomalies | 2 years |

---

## Audit Logging

Complete audit trails are maintained for all Graph RAG operations to support compliance and security investigations.

### Logged Events

| Event | Data Logged | Retention |
|:------|:------------|:----------|
| Query Executed | User ID, query text, entities searched, results returned | 2 years |
| Entity Retrieved | Entity ID, type, fields accessed, user, timestamp | 1 year |
| Relationship Traversed | From/to entities, relationship type, user, timestamp | 1 year |
| Access Denied | User, entity, reason, timestamp | 2 years |
| Cache Hit/Miss | Query, cache type, result, timestamp | 90 days |
| Performance Event | Query latency, execution time, resource usage | 90 days |

### Audit Log Security

| Control | Implementation |
|:--------|:---------------|
| Integrity | Cryptographic hash chain prevents tampering |
| Encryption | Logs encrypted at rest with AES-256 |
| Access Control | Auditor role required; no delete capability |
| PII Handling | Sensitive fields hashed or redacted |
| Retention | Configurable per regulatory requirement |
| Export | Auditors can export logs for external analysis |

---

## Integration with Platform Components

Graph RAG is deeply integrated with other DataFab components to provide a cohesive experience.

### Knowledge Fabric Integration

| Integration | Purpose | Data Flow |
|:-----------|:---------|:----------|
| Entity Lookup | Resolve entities mentioned in queries | Query → KF → Entity ID |
| Relationship Discovery | Find connections across sources | Query → KF Graph → Relationships |
| Source Attribution | Trace context back to source systems | Context → KF Lineage → Source |
| Schema Validation | Ensure retrieved data matches schema | Results → KF Schema → Validated |

### Exchange Integration

| Integration | Purpose |
|:-----------|:---------|
| Context Provision | Supply retrieved context to conversational interface |
| Query Interpretation | Translate natural language to graph queries |
| Session Management | Maintain session graph across conversation turns |
| Result Explanation | Explain retrieval decisions to users |

### Studio Integration

| Integration | Purpose |
|:-----------|:---------|
| Agent Context | Provide agents with relevant context from graph |
| Workflow Enrichment | Enrich pipeline data with graph relationships |
| Pattern Detection | Identify patterns in retrieved context |

---

## Summary

Graph RAG represents a significant advancement over traditional vector-only RAG systems by:

- **Leveraging Explicit Structure**: Uses the knowledge graph's relationship structure to improve context quality
- **Multi-Pattern Retrieval**: Supports entity-centric, relationship-traversal, and community-based patterns
- **Hybrid Scoring**: Combines vector similarity with graph structure for superior relevance
- **Coherent Context Assembly**: Automatically organizes retrieved information hierarchically for LLM consumption
- **Session-Aware Retrieval**: Maintains context across conversational turns for cumulative understanding
- **Comprehensive Security**: Enforces access controls throughout retrieval and assembly
- **High Performance**: Achieves sub-500ms latency through intelligent caching and query optimization
- **Complete Auditability**: Maintains full audit trails for compliance and security investigations

Graph RAG enables DataFab to deliver AI-augmented intelligence that is both contextually rich and verifiable, bridging the gap between operational systems and generative AI applications.

---
