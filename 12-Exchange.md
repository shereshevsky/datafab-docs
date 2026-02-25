---
layout: default
title: Exchange
---

# DataFab Exchange

**Version:** 4.0
**Last Updated:** February 2026

---

## Component Overview

The Exchange is the DataFab platform's data asset marketplace, enabling organizations to publish, discover, acquire, and monetize data assets across a decentralized ecosystem. Exchange supports a consumer-provider model with blockchain-backed transactions, usage-based metering, tiered access plans, and a double-entry ledger for transparent revenue sharing.

**Core Capabilities:**

| Capability | Description | Security Relevance |
|:-----------|:------------|:-------------------|
| Asset Catalog | Publish, search, and manage data assets (agents, widgets, datasets, models, utilities, media, chains, behaviour data) | Asset status governance, schema validation |
| User Profiles | Consumer, provider, and dual-role profiles with verification | Identity verification, role-based access |
| Wallet & Blockchain | DAAC token on Ethereum for purchases, deposits, withdrawals, and transfers | Cryptographic wallet security, transaction signing |
| Metering & Billing | Usage tracking with configurable metering policies and automated billing | Usage audit trail, billing integrity |
| Pricing & Subscriptions | Tiered access plans, subscription plans, fractional ownership, bulk purchases | Plan enforcement, entitlement validation |
| Access Control | Resource-level permission policies (READ, WRITE, DELETE, ADMIN) | Least privilege enforcement, permission auditing |
| Analytics | Event tracking, metric computation, dashboards, per-user analytics | Data minimization, access-scoped reporting |
| API Gateway | Managed endpoints (REST, GraphQL, Webhook, Proxy) with request logging | Endpoint security, rate limiting, request auditing |
| Ledger & Revenue Sharing | Double-entry accounting with revenue allocation, settlement, and reconciliation | Financial integrity, tamper-evident records |

---

## Architecture Overview

```
┌─────────────────────────────────────────────────────────────────────────┐
│                      EXCHANGE ARCHITECTURE                              │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  ┌────────────────────────────────────────────────────────────────────┐ │
│  │                      MARKETPLACE INTERFACE                         │ │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────────────────┐  │ │
│  │  │  Asset       │  │  Provider    │  │  Consumer Dashboards     │  │ │
│  │  │  Catalog UI  │  │  Portal      │  │  & Analytics             │  │ │
│  │  └──────────────┘  └──────────────┘  └──────────────────────────┘  │ │
│  └────────────────────────────────────────────────────────────────────┘ │
│                              │                                          │
│  ┌────────────────────────────────────────────────────────────────────┐ │
│  │                      EXCHANGE SERVICES                             │ │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌───────────┐  │ │
│  │  │  Catalog    │  │  Profile    │  │  Access     │  │ Analytics │  │ │
│  │  │  Service    │  │  Service    │  │  Service    │  │ Service   │  │ │
│  │  └─────────────┘  └─────────────┘  └─────────────┘  └───────────┘  │ │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌───────────┐  │ │
│  │  │  Metering   │  │  Wallet     │  │  Gateway    │  │  Ledger   │  │ │
│  │  │  Service    │  │  Service    │  │  Service    │  │  Service  │  │ │
│  │  └─────────────┘  └─────────────┘  └─────────────┘  └───────────┘  │ │
│  └────────────────────────────────────────────────────────────────────┘ │
│                              │                                          │
│  ┌────────────────────────────────────────────────────────────────────┐ │
│  │                      BLOCKCHAIN LAYER                              │ │
│  │  ┌─────────────┐  ┌─────────────┐  ┌──────────────────────────┐    │ │
│  │  │  Ethereum   │  │  DAAC Token │  │  Transaction Processing  │    │ │
│  │  │  Network    │  │  Contract   │  │  & Gas Estimation        │    │ │
│  │  └─────────────┘  └─────────────┘  └──────────────────────────┘    │ │
│  └────────────────────────────────────────────────────────────────────┘ │
│                              │                                          │
│  ┌────────────────────────────────────────────────────────────────────┐ │
│  │                  PLATFORM INTEGRATION                              │ │
│  │  ┌─────────────┐  ┌─────────────┐  ┌──────────────────────────┐    │ │
│  │  │  Knowledge  │  │  Studio     │  │  AI & LLM Layer          │    │ │
│  │  │  Fabric     │  │  (Agents)   │  │  (LightLLM)              │    │ │
│  │  └─────────────┘  └─────────────┘  └──────────────────────────┘    │ │
│  └────────────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## User Profiles

Exchange operates on a consumer-provider marketplace model. Users register with one of three profile types and may upgrade their role as needed.

### Profile Types

| Profile Type | Description | Capabilities |
|:-------------|:------------|:-------------|
| Consumer | Data asset consumers who discover, acquire, and use assets | Browse catalog, purchase assets, manage wallet, view usage analytics |
| Provider | Data asset providers who create, publish, and monetize assets | Publish assets, define pricing plans, manage endpoints, view revenue |
| Both | Dual-role users acting as both consumer and provider | Full consumer and provider capabilities |

### Profile Lifecycle

| Stage | Description | Security Controls |
|:------|:------------|:------------------|
| Registration | Create profile with user type selection | Email verification, identity validation |
| Verification | Provider identity and capability verification | Document review, domain validation |
| Provider Upgrade | Consumer requests upgrade to provider role | Verification workflow, manual approval |
| Active | Full marketplace participation | Continuous authentication, session management |
| Deactivation | Account suspension or removal | Data retention policies, wallet freeze |

### Profile Security Controls

| Control | Implementation |
|:--------|:---------------|
| Authentication | HTTPBearer (JWT) on all API endpoints |
| Profile Isolation | Tenant-scoped profile data with cross-tenant prevention |
| Verification Status | Provider publishing gated on verification completion |
| Role Enforcement | API-level enforcement of consumer vs. provider capabilities |

---

## Asset Catalog

The Catalog is the central registry for all publishable data assets in the Exchange ecosystem.

### Asset Types

| Asset Type | Description | Example Use Cases |
|:-----------|:------------|:------------------|
| BEHAVIOUR_DATA | Behavioral analytics and pattern datasets | Customer engagement patterns, usage telemetry |
| AGENT | Executable AI agents built in Studio | Automated data enrichment, analysis workflows |
| WIDGET | Visual interface components | Dashboard components, visualization tools |
| UTILITY | Reusable processing functions and tools | Data transformation pipelines, validators |
| MEDIA | Media files and content assets | Training datasets, reference materials |
| MODEL | Machine learning models | Predictive models, classifiers, embeddings |
| DATASET | Structured data collections | Reference data, enrichment datasets |
| CHAIN | Multi-agent workflow chains | End-to-end processing pipelines |

### Asset Lifecycle

```
┌──────────┐      ┌──────────────┐      ┌──────────────┐      ┌──────────────┐
│  CREATE  │ ───→ │    DRAFT     │ ───→ │  PUBLISHED   │ ───→ │  ARCHIVED    │
│          │      │              │      │              │      │              │
│  Author  │      │  Edit, test, │      │  Discoverable│      │  Withdrawn   │
│  asset   │      │  configure   │      │  & available │      │  from market │
└──────────┘      └──────────────┘      └──────────────┘      └──────────────┘
```

| Status | Description | Visibility |
|:-------|:------------|:-----------|
| DRAFT | Under development, not yet available | Provider only |
| PUBLISHED | Active and available in marketplace | All users (subject to access controls) |
| ARCHIVED | Withdrawn from active marketplace | Provider only; existing subscribers retain access per terms |

### Catalog Operations

| Operation | Description | Authorization |
|:----------|:------------|:-------------|
| Create Asset | Register new asset with metadata, type, and description | Verified providers |
| Update Asset | Modify asset metadata, documentation, or configuration | Asset owner |
| Publish Asset | Move asset from DRAFT to PUBLISHED | Verified providers, validation checks |
| Search Catalog | Discover assets by keyword, type, category, or provider | All authenticated users |
| Get Asset Details | Retrieve full asset information and pricing | All authenticated users |
| Archive Asset | Withdraw asset from active marketplace | Asset owner |
| Delete Asset | Permanently remove asset (DRAFT only) | Asset owner |

### Catalog Security Controls

| Control | Implementation |
|:--------|:---------------|
| Provider Verification | Only verified providers may publish assets |
| Asset Validation | Schema validation on asset metadata before publication |
| Search Authorization | Results filtered by user's access entitlements |
| Version Tracking | Full version history with provenance for all asset changes |
| Content Scanning | Automated scanning for sensitive data or policy violations |

---

## Wallet & Blockchain

Exchange uses a blockchain-backed digital wallet system with the DAAC token on Ethereum for secure, transparent financial transactions.

### Currency Support

| Currency | Type | Description |
|:---------|:-----|:------------|
| ETH | Cryptocurrency | Ethereum native currency for gas fees and transfers |
| DAAC | Utility Token | Platform-native token for asset purchases, subscriptions, and payouts |

### Wallet Operations

| Operation | Description | Security Controls |
|:----------|:------------|:------------------|
| Create Wallet | Generate Ethereum wallet for user profile | Cryptographic key generation, secure key storage |
| Deposit | Fund wallet with ETH or DAAC | Transaction verification, deposit confirmation |
| Withdraw | Transfer funds from wallet to external address | Withdrawal limits, confirmation workflow, address validation |
| Transfer | Transfer between platform wallets | Sender authorization, balance verification |
| Activate / Deactivate | Enable or suspend wallet operations | Admin authorization, freeze controls |
| Balance Check | Query current wallet balance | Read-only, authenticated access |

### Blockchain Integration

| Capability | Description |
|:-----------|:------------|
| Wallet Generation | Ethereum wallet creation with secure private key management |
| DAAC Token Operations | Token balance queries, transfer execution |
| Gas Estimation | Pre-transaction gas cost estimation for user confirmation |
| Transaction Status | Real-time transaction tracking and confirmation monitoring |
| Network Verification | Ethereum network health and connectivity checks |

### Wallet Security Controls

| Control | Implementation |
|:--------|:---------------|
| Private Key Storage | Encrypted key storage with HSM-backed protection |
| Transaction Signing | All transactions cryptographically signed before broadcast |
| Withdrawal Limits | Configurable daily and per-transaction withdrawal limits |
| Address Whitelisting | Optional restriction of withdrawal to pre-approved addresses |
| Wallet Freeze | Immediate suspension capability for compromised wallets |
| Audit Trail | All wallet operations logged with full transaction history |

---

## Metering & Billing

Exchange provides configurable usage metering with automated billing for all asset consumption.

### Metering Event Types

| Event Type | Description | Measurement Unit |
|:-----------|:------------|:-----------------|
| API_CALL | API endpoint invocations | Request count |
| DATA_DOWNLOAD | Data transfer from assets | Volume (bytes) |
| ASSET_VIEW | Asset page or preview views | View count |
| COMPUTE_TIME | Processing time consumed | Duration (seconds) |
| STORAGE_USAGE | Storage capacity utilized | Volume (bytes) |

### Metering Policies

| Policy | Description | Use Case |
|:-------|:------------|:---------|
| REQUEST_COUNT | Charge per number of API calls | API-based assets |
| DATA_VOLUME | Charge per volume of data transferred | Dataset downloads |
| COMPUTE_TIME | Charge per processing time consumed | Agent and model execution |
| FLAT_RATE | Fixed periodic charge regardless of usage | Subscription access |
| TIERED_ACCESS | Variable pricing based on usage tiers | Multi-tier plans |

### Metering Pipeline

```
Usage Event → Record → Aggregate → Billing Generation → Invoice → Settlement
     │            │          │              │                │           │
 (Capture)   (Store)   (Summarize)    (Calculate)      (Deliver)  (Payout)
```

| Stage | Description | Security Controls |
|:------|:------------|:------------------|
| Event Capture | Real-time usage event recording | Event authentication, timestamp integrity |
| Usage Recording | Persistent storage of metering records | Tamper-evident storage, write-once semantics |
| Usage Summary | Aggregation by user, asset, period | Access-scoped summaries |
| Usage Check | Real-time quota and limit verification | Threshold alerts, automatic cutoff |
| Billing Generation | Automated invoice creation from usage data | Calculation verification, audit trail |

---

## Pricing & Subscriptions

Exchange supports multiple pricing models to accommodate diverse asset monetization strategies.

### Pricing Plans

| Plan Type | Description | Billing Model |
|:----------|:------------|:-------------|
| Tiered Pricing | Multiple tiers with increasing quotas and features | Per-tier fixed + overage |
| Subscription Plans | Recurring access with defined entitlements | Periodic (monthly / annual) |
| Access Tiers | Graduated access levels with varying data freshness | Per-tier pricing |
| Fractional Ownership | Revenue sharing among multiple asset stakeholders | Proportional allocation |
| Bulk Purchase | Volume-based pricing for large acquisitions | Discounted unit pricing |

### Data Freshness Levels

| Freshness Level | Latency | Typical Tier |
|:----------------|:--------|:-------------|
| REAL_TIME | Immediate | Premium |
| DELAYED_5MIN | 5-minute delay | Enterprise |
| DELAYED_15MIN | 15-minute delay | Professional |
| DELAYED_30MIN | 30-minute delay | Standard |
| END_OF_DAY | End-of-day batch | Basic |

### Subscription Lifecycle

| Stage | Description | Controls |
|:------|:------------|:---------|
| Plan Selection | Consumer selects pricing plan and tier | Plan availability validation |
| Purchase | DAAC or ETH payment processed | Balance verification, transaction confirmation |
| Activation | Access entitlements provisioned | Permission grant, metering initialization |
| Usage | Ongoing consumption within plan limits | Quota monitoring, overage alerts |
| Renewal / Expiry | Automatic renewal or access termination | Renewal notification, grace period |
| Cancellation | Consumer-initiated plan termination | Pro-rata refund calculation |

### Pricing Security Controls

| Control | Implementation |
|:--------|:---------------|
| Price Integrity | Provider-defined pricing with tamper-evident records |
| Plan Enforcement | Real-time entitlement validation on every access request |
| Overage Protection | Configurable hard and soft limits with consumer notification |
| Revenue Verification | Automated reconciliation of billing against usage records |

---

## Access Control

Exchange implements fine-grained, resource-level access control for all marketplace assets and operations.

### Permission Types

| Permission | Description | Scope |
|:-----------|:------------|:------|
| READ | View asset metadata, download data, invoke endpoints | Consumers and providers |
| WRITE | Update asset content, modify configurations | Asset owners and authorized collaborators |
| DELETE | Remove assets, revoke access records | Asset owners and administrators |
| ADMIN | Full control including access policy management | Platform administrators |

### Access Policy Model

| Component | Description |
|:----------|:------------|
| Resource Type | Asset type the policy applies to (AGENT, DATASET, MODEL, etc.) |
| Resource ID | Specific asset instance identifier |
| Permission | Granted permission level (READ, WRITE, DELETE, ADMIN) |
| User / Role | Target user or role for the policy |
| Conditions | Optional conditions (time-based, IP-based, usage-limited) |

### Access Operations

| Operation | Description | Authorization |
|:----------|:------------|:-------------|
| Create Policy | Define new access policy for a resource | Resource owner, ADMIN |
| Grant Permission | Grant specific permission to a user | Resource owner, ADMIN |
| Revoke Permission | Remove specific permission from a user | Resource owner, ADMIN |
| Check Permission | Verify if user has specific permission on a resource | All authenticated users (self-check) |
| List Policies | View access policies for a resource | Resource owner, ADMIN |

### Access Control Security

| Control | Implementation |
|:--------|:---------------|
| Policy Enforcement | Every API request validated against access policies |
| Least Privilege | Default deny; explicit grant required for all access |
| Permission Propagation | No implicit permission inheritance between asset types |
| Audit Logging | All grant, revoke, and check operations logged |
| Temporal Controls | Time-bounded permissions with automatic expiry |

---

## Analytics

Exchange provides comprehensive analytics for marketplace activity, asset performance, and user engagement.

### Analytics Capabilities

| Capability | Description | Audience |
|:-----------|:------------|:---------|
| Event Tracking | Capture and store marketplace interaction events | Platform operations |
| Metric Computation | Calculate KPIs from raw event data | Providers and platform |
| Dashboard Data | Pre-aggregated data for visual dashboards | All users |
| User Analytics | Per-user consumption and engagement metrics | Individual users, providers |

### Event Types

| Event Category | Examples | Use Case |
|:---------------|:---------|:---------|
| Discovery | Asset views, search queries, catalog browsing | Discoverability optimization |
| Consumption | Downloads, API calls, compute invocations | Usage monitoring, billing validation |
| Transaction | Purchases, subscriptions, wallet operations | Financial reporting |
| Engagement | Reviews, ratings, return visits | Marketplace health |

### Analytics Security Controls

| Control | Implementation |
|:--------|:---------------|
| Data Minimization | Analytics data aggregated and anonymized where possible |
| Access Scoping | Providers see only their own asset analytics; consumers see their own usage |
| Retention Policy | Event data retained per configurable retention periods |
| Export Controls | Analytics export requires authorized access |

---

## API Gateway

Exchange includes a managed API Gateway for exposing and consuming data assets via standardized endpoints.

### Endpoint Types

| Endpoint Type | Description | Use Case |
|:-------------|:------------|:---------|
| REST | Standard REST API endpoints | General data access, CRUD operations |
| GraphQL | GraphQL query endpoints | Flexible querying, relational data |
| Webhook | Event-driven push notifications | Real-time event delivery |
| Proxy | Transparent proxy to upstream services | Legacy system integration |

### Gateway Capabilities

| Capability | Description |
|:-----------|:------------|
| Endpoint Management | Create, update, and deactivate managed endpoints per asset |
| Request Logging | Full request/response logging with configurable retention |
| Endpoint Statistics | Latency, throughput, error rate metrics per endpoint |
| Rate Limiting | Configurable rate limits per consumer, plan, and endpoint |
| Authentication | JWT-based authentication with per-endpoint token validation |

### Gateway Operations

| Operation | Description | Authorization |
|:----------|:------------|:-------------|
| Create Endpoint | Register new API endpoint for an asset | Asset owner (verified provider) |
| Update Endpoint | Modify endpoint configuration or routing | Asset owner |
| Deactivate Endpoint | Disable endpoint without deletion | Asset owner |
| View Logs | Access request/response logs for endpoint | Asset owner |
| View Statistics | Access performance metrics for endpoint | Asset owner |

### Gateway Security Controls

| Control | Implementation |
|:--------|:---------------|
| TLS Enforcement | All gateway traffic encrypted with TLS 1.3 |
| JWT Validation | Bearer token validation on every request |
| Rate Limiting | Per-consumer and per-plan rate limits to prevent abuse |
| Request Validation | Input validation and schema checking on all requests |
| Logging Integrity | Tamper-evident request logs with retention controls |
| DDoS Protection | Traffic analysis and automatic throttling |

---

## Ledger & Revenue Sharing

Exchange implements a double-entry ledger for all financial transactions, enabling transparent revenue allocation and settlement.

### Ledger Architecture

```
Transaction → Ledger Entry → Revenue Allocation → Settlement → Payout
     │              │                │                 │           │
 (Purchase)    (Double-entry)   (Split rules)    (Reconcile)  (Transfer)
```

### Transaction Types

| Transaction Type | Description | Ledger Impact |
|:-----------------|:------------|:-------------|
| DEPOSIT | Funds added to wallet | Credit wallet balance |
| WITHDRAWAL | Funds removed from wallet | Debit wallet balance |
| PURCHASE | Asset or plan purchase | Debit buyer, credit escrow |
| SALE | Revenue from asset sale | Credit provider, debit escrow |
| TRANSFER | Wallet-to-wallet transfer | Debit sender, credit recipient |

### Revenue Allocation

| Allocation Reason | Description | Beneficiary |
|:-------------------|:------------|:------------|
| ASSET_SALE | Direct asset purchase revenue | Asset provider |
| SUBSCRIPTION_PAYMENT | Recurring subscription revenue | Asset provider |
| PRICING_PLAN_PAYMENT | Tiered plan payment revenue | Asset provider |
| PLATFORM_FEE | Platform commission on transactions | Platform operator |
| REFERRAL_BONUS | Referral incentive payout | Referring user |

### Fractional Ownership

Exchange supports fractional ownership models where multiple stakeholders share revenue from a single asset:

| Component | Description |
|:----------|:------------|
| Ownership Shares | Percentage allocation among stakeholders |
| Revenue Split | Automatic proportional distribution of earnings |
| Pending Earnings | Accumulated earnings awaiting settlement |
| Settlement | Batch processing of pending earnings into wallet balances |

### Ledger Security Controls

| Control | Implementation |
|:--------|:---------------|
| Double-Entry Integrity | Every transaction creates balanced debit and credit entries |
| Immutable Records | Ledger entries are append-only with no modification or deletion |
| Reconciliation | Automated reconciliation checks to detect discrepancies |
| Settlement Authorization | Settlement operations require authorized approval |
| Audit Trail | Complete transaction history with timestamps and actor attribution |
| Balance Verification | Computed balances cross-checked against ledger entries |

### Administrative Operations

| Operation | Description | Authorization |
|:----------|:------------|:-------------|
| Reconciliation Check | Verify ledger balance consistency | Platform administrator |
| Settlement Execution | Process pending earnings into wallet balances | Platform administrator |
| Ledger Query | Retrieve filtered ledger entries | Authenticated users (own records), admin (all) |
| Pending Earnings | View accumulated unsettled earnings | Asset providers (own), admin (all) |

---

## Security Summary

### Authentication & Authorization

| Control | Implementation |
|:--------|:---------------|
| Authentication Method | HTTPBearer with JWT tokens on all API endpoints |
| Token Validation | Signature verification, expiry checking, issuer validation |
| Role-Based Access | Consumer, provider, and admin role enforcement |
| Resource Authorization | Per-asset permission policies with explicit grant model |
| Admin Controls | Super admin passphrase management for platform operations |

### Data Protection

| Control | Implementation |
|:--------|:---------------|
| Encryption in Transit | TLS 1.3 for all API communications |
| Encryption at Rest | AES-256 for stored data including wallet keys |
| Private Key Security | HSM-backed storage for blockchain private keys |
| Data Isolation | Tenant-scoped data access with cross-tenant prevention |
| PII Protection | Personal data encrypted and access-controlled |

### Audit & Compliance

| Control | Implementation |
|:--------|:---------------|
| Transaction Audit | All financial transactions logged with full provenance |
| Access Audit | Permission grants, revokes, and checks recorded |
| Usage Audit | Metering events captured for billing and compliance |
| API Audit | Gateway request/response logs with configurable retention |
| Ledger Audit | Immutable double-entry records with reconciliation checks |

### Platform Integration Security

| Integration | Security Mechanism |
|:------------|:-------------------|
| Knowledge Fabric | Dataset assets reference Knowledge Graph entities with access-controlled traversal |
| Studio | Agent and widget assets execute in sandboxed Studio environments |
| AI & LLM Layer | Model assets route through LightLLM with output validation |
| Blockchain | Ethereum transactions signed and verified on-chain |

---

## API Reference Summary

### API Domain Groups

| Domain | Base Path | Description |
|:-------|:----------|:------------|
| Profile | `/api/v1/profile/` | User profile management, verification, provider upgrade |
| Catalog | `/api/v1/catalog/` | Asset CRUD, search, publish |
| Wallet | `/api/v1/wallet/` | Digital wallet operations, balance, transactions |
| Blockchain | `/api/v1/blockchain/` | Ethereum network, DAAC token, gas estimation |
| Metering | `/api/v1/metering/` | Usage records, billing, pricing plans, subscriptions |
| Access | `/api/v1/access/` | Access policies, permission management |
| Analytics | `/api/v1/analytics/` | Event tracking, metrics, dashboards |
| Gateway | `/api/v1/gateway/` | API endpoint management, logs, statistics |
| Ledger | `/api/v1/ledger/` | Transaction ledger, balance, settlement |
| Admin | `/api/v1/admin/` | Administrative operations (reconciliation, settlement) |
| Passphrase | `/api/v1/passphrase/` | Admin passphrase management (super admin only) |

### Authentication

All Exchange API endpoints require HTTPBearer authentication via JWT tokens. Tokens must be included in the `Authorization` header:

```
Authorization: Bearer <jwt_token>
```

---

*For related platform documentation, see [Knowledge Fabric](./03-Knowledge-Fabric.md) for data integration, [Studio](./04-Studio.md) for agent and widget creation, [API Security](./11-API-Security.md) for gateway security patterns, and [Trust & Compliance](./14-Trust-Compliance.md) for governance controls.*
