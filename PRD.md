# Product Requirements Document
## E-Commerce Platform — ShopNow

**Version:** 1.0  
**Status:** Draft  
**Owner:** Product Team  
**Last Updated:** 2026-05-29

---

## Table of Contents

1. [Executive Summary](#1-executive-summary)
2. [Problem Statement](#2-problem-statement)
3. [Goals & Success Metrics](#3-goals--success-metrics)
4. [User Personas](#4-user-personas)
5. [Scope](#5-scope)
6. [Functional Requirements](#6-functional-requirements)
7. [Non-Functional Requirements](#7-non-functional-requirements)
8. [System Architecture Overview](#8-system-architecture-overview)
9. [User Flows](#9-user-flows)
10. [Feature Details](#10-feature-details)
11. [Data Models](#11-data-models)
12. [API Overview](#12-api-overview)
13. [Security & Compliance](#13-security--compliance)
14. [Release Strategy](#14-release-strategy)
15. [Risks & Mitigations](#15-risks--mitigations)
16. [Open Questions](#16-open-questions)
17. [Appendix](#17-appendix)

---

## 1. Executive Summary

**ShopNow** is a full-featured B2C/B2B e-commerce platform modelled after Amazon and Flipkart. It connects buyers and multi-vendor sellers through a unified marketplace with intelligent discovery, secure payments, real-time order tracking, and a personalized shopping experience.

The platform targets three primary markets:
- **Consumers** seeking a wide product catalogue, competitive prices, and fast delivery.
- **Sellers / SMBs** needing a low-friction channel to reach millions of buyers.
- **Enterprise / Brand owners** requiring advanced analytics, ads, and fulfilment services.

**Target launch timeline:** MVP in 6 months, full platform in 12 months.

---

## 2. Problem Statement

### Core Problems

| # | User Segment | Problem | Severity |
|---|-------------|---------|----------|
| P1 | Buyer | Fragmented shopping across many sites with inconsistent trust signals | High |
| P2 | Buyer | Poor product discovery — search results irrelevant, no personalisation | High |
| P3 | Buyer | Lack of transparency in delivery timelines and order status | High |
| P4 | Seller | Onboarding to existing marketplaces is slow (weeks, not hours) | High |
| P5 | Seller | Limited real-time analytics; difficult to optimise listings | Medium |
| P6 | Buyer | Returns and refunds are manual, opaque, and slow | Medium |
| P7 | Seller | No native advertising tools to boost product visibility | Medium |

### Why Now
Smartphone penetration and UPI/digital-payment adoption have created a massive untapped tier-2 and tier-3 city buyer base. Existing platforms have high seller fees and poor small-seller support. A modern, API-first platform with low commission rates (< 8%) can capture significant market share.

---

## 3. Goals & Success Metrics

### Business Goals

| Goal | KPI | Target (Month 12) |
|------|-----|-------------------|
| Grow buyer base | Monthly Active Users (MAU) | 500,000 |
| Grow seller base | Active Seller Accounts | 10,000 |
| Revenue | Gross Merchandise Value (GMV) | ₹100 Cr / $12M |
| Retention | 30-day buyer retention | ≥ 40% |
| Trust | Net Promoter Score (NPS) | ≥ 45 |

### Product Goals

| Goal | KPI | Target |
|------|-----|--------|
| Search quality | Click-through rate on top-3 results | ≥ 60% |
| Checkout conversion | Cart → Order completion | ≥ 72% |
| Seller satisfaction | Seller onboarding time (hours) | < 2 hrs |
| Reliability | Platform uptime | 99.9% |
| Performance | Page load time (P95) | < 2 s |

### Out-of-Scope for v1.0
- Physical fulfilment / warehousing (3PL integration only)
- Cross-border / international shipping
- Cryptocurrency payments
- Live-commerce / video shopping
- B2B bulk procurement portal (planned v2.0)

---

## 4. User Personas

### Persona 1 — Priya, The Urban Buyer
- **Age:** 28, Software Engineer, Bengaluru
- **Behaviour:** Shops 2–3× per week; price-sensitive; trusts reviews; uses EMI heavily
- **Pain Points:** Fake reviews, slow returns, inconsistent delivery estimates
- **Goals:** Find best value, quick delivery, hassle-free returns

### Persona 2 — Ramesh, The Tier-2 First-Timer
- **Age:** 42, Small Business Owner, Kanpur
- **Behaviour:** New to online shopping; needs vernacular UI, COD preferred
- **Pain Points:** Doesn't trust prepaid payments; language barrier; fear of fraud
- **Goals:** Safe, simple purchase experience in Hindi/regional language

### Persona 3 — Neha, The Power Seller (SMB)
- **Age:** 35, Textile wholesaler, Surat
- **Behaviour:** Lists 500+ SKUs; needs bulk upload, pricing tools, fast payouts
- **Pain Points:** High commission fees, slow dispute resolution, no real-time stock sync
- **Goals:** Low fees, instant payout, inventory management

### Persona 4 — Kiran, The Brand Manager (Enterprise)
- **Age:** 31, Marketing, Nike India
- **Behaviour:** Runs sponsored ads, monitors brand analytics, manages authorised resellers
- **Pain Points:** Limited ad targeting, no brand store customisation, poor ROI visibility
- **Goals:** Brand store, ad campaigns, competitor insights

---

## 5. Scope

### MVP — Phase 1 (Month 1–6)

| Module | Features Included |
|--------|------------------|
| Buyer App | Registration/Login, Product Browse & Search, PDP, Cart, Checkout, Order Tracking, Basic Reviews |
| Seller Portal | Registration, Product Listing (single + bulk CSV), Inventory Management, Order Management, Basic Analytics |
| Payments | UPI, Credit/Debit Card, Net Banking, COD |
| Admin Panel | User Management, Category Management, Commission Config, KYC Approvals |
| Infrastructure | Monolith-to-microservice-ready architecture, CDN, Basic CI/CD |

### Full Platform — Phase 2 (Month 7–12)

| Module | Features Added |
|--------|---------------|
| Personalisation | ML-powered recommendations, personalised homepage, smart search |
| Returns & Refunds | Automated return flow, refund SLA engine |
| Seller Analytics | Revenue dashboard, conversion funnel, inventory forecasting |
| Ads Platform | Sponsored Products, Sponsored Brands, CPC bidding |
| Loyalty Program | ShopNow Coins, tier-based cashback |
| Vernacular Support | Hindi, Tamil, Telugu, Kannada, Bengali |
| Mobile Apps | iOS & Android (React Native) |

---

## 6. Functional Requirements

### 6.1 User Authentication & Identity

| ID | Requirement | Priority |
|----|------------|---------|
| AUTH-01 | Email + password registration with OTP verification | Must Have |
| AUTH-02 | Mobile number login via OTP (no password needed) | Must Have |
| AUTH-03 | OAuth2 via Google and Apple | Must Have |
| AUTH-04 | Multi-factor authentication for seller/admin accounts | Must Have |
| AUTH-05 | Session management with JWT (15-min access, 7-day refresh) | Must Have |
| AUTH-06 | Biometric login on mobile (FaceID / Fingerprint) | Should Have |
| AUTH-07 | Guest checkout (converts to account post-purchase) | Should Have |

### 6.2 Product Catalogue

| ID | Requirement | Priority |
|----|------------|---------|
| CAT-01 | Hierarchical category tree (Category → Sub-category → Leaf) | Must Have |
| CAT-02 | Product listing page with filters (price, brand, rating, delivery, etc.) | Must Have |
| CAT-03 | Product detail page: images (zoom), specs, variants (size/colour), stock status | Must Have |
| CAT-04 | Seller bulk upload via CSV / Excel with validation errors report | Must Have |
| CAT-05 | Product variations (e.g., different sizes link to parent SKU) | Must Have |
| CAT-06 | Dynamic pricing: flash sales, festive discounts, quantity-based pricing | Should Have |
| CAT-07 | AI-powered product title/description generation for sellers | Nice to Have |
| CAT-08 | Seller can import from Shopify / WooCommerce store | Nice to Have |

### 6.3 Search & Discovery

| ID | Requirement | Priority |
|----|------------|---------|
| SRCH-01 | Full-text search with typo tolerance and synonyms | Must Have |
| SRCH-02 | Faceted filters applied without page reload | Must Have |
| SRCH-03 | Auto-complete / type-ahead suggestions | Must Have |
| SRCH-04 | Voice search (microphone input) | Should Have |
| SRCH-05 | Visual search (upload image to find similar products) | Nice to Have |
| SRCH-06 | Personalised search ranking based on user history | Phase 2 |
| SRCH-07 | "Frequently bought together" and "Customers also viewed" widgets | Phase 2 |

### 6.4 Cart & Wishlist

| ID | Requirement | Priority |
|----|------------|---------|
| CART-01 | Persistent cart (survives logout, syncs across devices) | Must Have |
| CART-02 | Guest cart merged on login | Must Have |
| CART-03 | Quantity update, item removal, save-for-later | Must Have |
| CART-04 | Coupon/promo code application with real-time validation | Must Have |
| CART-05 | Wishlist with share-link feature | Should Have |
| CART-06 | In-cart upsell recommendations | Nice to Have |

### 6.5 Checkout & Payments

| ID | Requirement | Priority |
|----|------------|---------|
| PAY-01 | Single-page checkout: address → payment → review → confirm | Must Have |
| PAY-02 | Address book (save multiple addresses, default selection) | Must Have |
| PAY-03 | UPI (VPA + QR), Debit/Credit Card (Visa/MC/RuPay), Net Banking | Must Have |
| PAY-04 | Cash on Delivery (COD) with configurable eligibility rules | Must Have |
| PAY-05 | EMI on credit cards (3/6/9/12 months, bank-specific rates) | Must Have |
| PAY-06 | ShopNow Wallet (top-up, balance, auto-debit) | Should Have |
| PAY-07 | BNPL (Buy Now Pay Later) via Simpl / LazyPay | Should Have |
| PAY-08 | PCI-DSS compliant card tokenisation (no raw PAN storage) | Must Have |
| PAY-09 | Payment retry on failure with intelligent routing | Must Have |

### 6.6 Order Management

| ID | Requirement | Priority |
|----|------------|---------|
| ORD-01 | Order confirmation with itemised invoice (PDF download) | Must Have |
| ORD-02 | Real-time order status: Placed → Confirmed → Shipped → Out for Delivery → Delivered | Must Have |
| ORD-03 | Push + SMS + email notifications at each status change | Must Have |
| ORD-04 | Live shipment tracking via 3PL API (Shiprocket, Delhivery) | Must Have |
| ORD-05 | Order cancellation (before shipment) with instant refund | Must Have |
| ORD-06 | Multi-seller cart → split shipments with consolidated tracking page | Must Have |
| ORD-07 | Partial fulfilment handling (backordered items) | Should Have |

### 6.7 Returns, Refunds & Disputes

| ID | Requirement | Priority |
|----|------------|---------|
| RET-01 | Self-service return initiation within configurable return window | Must Have |
| RET-02 | Return reasons taxonomy with optional photo upload | Must Have |
| RET-03 | Automated refund (original payment method) within 5-7 business days | Must Have |
| RET-04 | Reverse logistics coordination with 3PL pickup scheduling | Must Have |
| RET-05 | Buyer–seller dispute escalation to admin arbitration | Should Have |
| RET-06 | Instant refund to ShopNow Wallet option | Nice to Have |

### 6.8 Ratings & Reviews

| ID | Requirement | Priority |
|----|------------|---------|
| REV-01 | Star rating (1–5) + written review after confirmed delivery | Must Have |
| REV-02 | Verified Purchase badge | Must Have |
| REV-03 | Review moderation queue with NLP spam/abuse detection | Must Have |
| REV-04 | Seller response to reviews | Should Have |
| REV-05 | Helpful votes on reviews ("Was this helpful?") | Should Have |
| REV-06 | Review-based Q&A section (community answers) | Nice to Have |

### 6.9 Seller Portal

| ID | Requirement | Priority |
|----|------------|---------|
| SEL-01 | Self-serve onboarding: GST + PAN + bank account KYC | Must Have |
| SEL-02 | Product listing with rich text editor, image upload (5 images + 1 video) | Must Have |
| SEL-03 | Inventory management: stock levels, low-stock alerts, SKU management | Must Have |
| SEL-04 | Order fulfilment dashboard: accept, pack, dispatch, mark shipped | Must Have |
| SEL-05 | Payout dashboard: settled, pending, commission breakdown | Must Have |
| SEL-06 | Performance analytics: GMV, conversion, returns rate, customer ratings | Should Have |
| SEL-07 | Promotional tools: coupons, flash deals, bundle offers | Should Have |
| SEL-08 | Sponsored Ads campaign manager (CPC bidding) | Phase 2 |

### 6.10 Admin Panel

| ID | Requirement | Priority |
|----|------------|---------|
| ADM-01 | User and seller account management (view, suspend, ban) | Must Have |
| ADM-02 | Category and attribute management | Must Have |
| ADM-03 | Commission rate configuration by category | Must Have |
| ADM-04 | KYC review and approval workflow | Must Have |
| ADM-05 | Platform-wide promotional banner management | Must Have |
| ADM-06 | Fraud monitoring dashboard with rule-based alerts | Should Have |
| ADM-07 | Content moderation queue (products, reviews) | Should Have |
| ADM-08 | Financial reconciliation and payout controls | Must Have |

---

## 7. Non-Functional Requirements

### Performance

| Metric | Target |
|--------|--------|
| Homepage load time (P95) | < 1.5 s |
| Search result latency (P95) | < 300 ms |
| Checkout page load (P95) | < 2 s |
| API response time (P99) | < 500 ms |
| Concurrent users (Day 1) | 10,000 |
| Concurrent users (Month 12) | 500,000 |

### Scalability

- Horizontal auto-scaling for all stateless services
- Database read replicas for catalogue and order reads
- Elasticsearch / OpenSearch for product search (sharded)
- Redis for session, cart, and catalogue caching
- CDN for static assets and product images (< 50 ms globally)

### Availability & Reliability

| Service | SLA |
|---------|-----|
| Buyer-facing storefront | 99.9% (< 8.7 hrs downtime/yr) |
| Payment processing | 99.95% |
| Seller portal | 99.5% |
| Admin panel | 99.0% |

### Security

- TLS 1.3 everywhere (HSTS enforced)
- OWASP Top-10 mitigations at application layer
- WAF + DDoS protection (Cloudflare or AWS Shield)
- PCI-DSS SAQ-D compliance for payment flows
- GDPR / India DPDP Act compliance for personal data
- Role-based access control (RBAC) in admin and seller portal
- All PII encrypted at rest (AES-256) and in transit

### Observability

- Structured logging (JSON) shipped to centralised log management
- Distributed tracing (OpenTelemetry) across microservices
- Business metrics dashboards (Grafana / DataDog)
- Error tracking and alerting (Sentry / PagerDuty)
- SLO/SLA monitoring with automated incident creation

---

## 8. System Architecture Overview

```
┌──────────────────────────────────────────────────────────┐
│                      CDN / WAF / DDoS                     │
└────────────────────────┬─────────────────────────────────┘
                         │
           ┌─────────────▼──────────────┐
           │       API Gateway           │
           │  (Auth, Rate-Limit, Route)  │
           └──┬───────┬────────┬────────┘
              │       │        │
   ┌──────────▼─┐ ┌───▼───┐ ┌─▼──────────┐
   │  Buyer BFF │ │Seller │ │ Admin BFF  │
   │  (Next.js) │ │  BFF  │ │            │
   └──────┬─────┘ └───┬───┘ └─────┬──────┘
          │           │           │
   ┌──────▼───────────▼───────────▼──────────┐
   │             Internal Service Mesh        │
   │  ┌────────┐ ┌────────┐ ┌─────────────┐  │
   │  │Catalogue│ │ Order  │ │  Payment    │  │
   │  │Service │ │Service │ │  Service    │  │
   │  └────────┘ └────────┘ └─────────────┘  │
   │  ┌────────┐ ┌────────┐ ┌─────────────┐  │
   │  │  User  │ │Search  │ │Notification │  │
   │  │Service │ │Service │ │  Service    │  │
   │  └────────┘ └────────┘ └─────────────┘  │
   │  ┌────────┐ ┌────────┐ ┌─────────────┐  │
   │  │ Cart   │ │Review  │ │  Seller     │  │
   │  │Service │ │Service │ │  Service    │  │
   │  └────────┘ └────────┘ └─────────────┘  │
   └──────────────────┬──────────────────────┘
                      │
   ┌──────────────────▼──────────────────────┐
   │              Data Layer                  │
   │  PostgreSQL │ Redis │ Elasticsearch      │
   │  S3 / GCS   │ Kafka │ ClickHouse (OLAP)  │
   └─────────────────────────────────────────┘
```

### Tech Stack Recommendation

| Layer | Technology |
|-------|-----------|
| Web Frontend | Next.js 14 (App Router) + TypeScript + Tailwind CSS |
| Mobile | React Native (Expo) |
| Backend Services | Node.js (Fastify) + Python (FastAPI for ML services) |
| API Gateway | Kong / AWS API Gateway |
| Auth | Keycloak or Auth0 (OAuth2 / OIDC) |
| Database (Transactional) | PostgreSQL 16 (RDS) |
| Cache | Redis 7 (ElastiCache) |
| Search | OpenSearch / Elasticsearch 8 |
| Message Queue | Apache Kafka |
| Object Storage | AWS S3 + CloudFront CDN |
| OLAP / Analytics | ClickHouse |
| Infrastructure | AWS / GCP (Kubernetes + Helm) |
| CI/CD | GitHub Actions + ArgoCD |
| Monitoring | Grafana + Prometheus + OpenTelemetry |

---

## 9. User Flows

### 9.1 Buyer Purchase Flow

```
[Home] → [Search/Browse] → [PLP] → [PDP]
  → [Add to Cart] → [Cart Review]
  → [Checkout: Address] → [Checkout: Payment]
  → [Order Confirmation] → [Email/SMS Notification]
  → [Track Order] → [Delivery] → [Review Prompt]
```

### 9.2 New Seller Onboarding Flow

```
[Landing Page] → [Register: Email + Mobile OTP]
  → [KYC: Upload GST + PAN + Bank Details]
  → [Admin KYC Review (async, < 2 hrs)]
  → [Seller Dashboard Access]
  → [Add First Product] → [Go Live]
```

### 9.3 Return Flow

```
[My Orders] → [Select Order] → [Request Return]
  → [Select Items + Reason + Photo Upload]
  → [Schedule Pickup (3PL)] → [Item Picked Up]
  → [Quality Check at Warehouse]
  → [Refund Initiated] → [Refund Credited]
```

### 9.4 Seller Order Fulfilment Flow

```
[New Order Alert (push/email)] → [Seller Dashboard]
  → [Accept Order] → [Pack Item]
  → [Generate Shipping Label] → [Hand to 3PL]
  → [Mark Dispatched + AWB Entry]
  → [Buyer Notified Automatically]
```

---

## 10. Feature Details

### 10.1 Search Engine Design

**Technology:** OpenSearch with custom ranking

**Ranking Signals (in order of weight):**
1. Text relevance (BM25 score)
2. Seller rating (weighted average)
3. Sales velocity (last 30 days)
4. Sponsored placement (CPC — Phase 2)
5. Price competitiveness within category
6. Inventory availability
7. Personalisation boost (user history — Phase 2)

**Index Structure:**
- `products` index: id, title, description, brand, category path, attributes, price, stock, seller_id, rating, image_urls
- Synonyms dictionary managed via admin panel
- Stopwords and stemming per language

### 10.2 Payment Architecture

**Payment Service Responsibilities:**
- Intent creation → Gateway handoff → Webhook receipt → Order state update
- Idempotency via `payment_intent_id` (prevent double-charges)
- Reconciliation job runs every 15 minutes

**Gateway Priority for UPI:**
```
Primary: Razorpay → Fallback: Cashfree → Last Resort: PayU
```

**Commission Deduction Model:**
- Payout = GMV − Platform Commission (%) − Payment Gateway Fee − Return Adjustments
- Weekly payout cycle (T+7 from delivery confirmation)

### 10.3 Recommendation Engine (Phase 2)

**Models:**
| Use Case | Algorithm |
|---------|-----------|
| Homepage feed | Collaborative Filtering (ALS) |
| "Similar products" | Item2Vec embeddings |
| "Frequently bought together" | Association Rule Mining (FP-Growth) |
| "Recently viewed" | Session-based recency model |
| Email recommendations | Matrix Factorisation + recency boost |

**Feature Store:** Real-time user events via Kafka → Flink → Redis feature store

### 10.4 Fraud Detection

**Rule-Based Triggers (immediate block):**
- > 5 failed payment attempts in 30 minutes from same device
- COD order to undeliverable pin-code
- Seller payout request > 3× 7-day average

**ML Model (async scoring):**
- Gradient Boosted Trees trained on historical chargebacks
- Features: device fingerprint, IP geolocation, purchase history, velocity
- Score threshold: > 0.85 → manual review; > 0.95 → auto-block

---

## 11. Data Models

### Core Entities

```sql
-- Users
users (id, email, mobile, name, role, status, created_at)
addresses (id, user_id, label, line1, line2, city, state, pincode, is_default)

-- Catalogue
categories (id, parent_id, name, slug, level, attributes_schema)
products (id, seller_id, category_id, title, description, brand, status)
product_variants (id, product_id, sku, price, mrp, stock_qty, attributes JSONB)
product_images (id, product_id, variant_id, url, sort_order)

-- Commerce
carts (id, user_id, session_id, created_at, updated_at)
cart_items (id, cart_id, variant_id, qty, unit_price)
orders (id, user_id, status, total_amount, discount, tax, payment_status)
order_items (id, order_id, variant_id, seller_id, qty, unit_price, item_status)
shipments (id, order_id, tracking_number, carrier, status, shipped_at, delivered_at)

-- Payments
payments (id, order_id, gateway, gateway_txn_id, amount, status, method, created_at)
refunds (id, payment_id, amount, reason, status, initiated_at, completed_at)

-- Sellers
sellers (id, user_id, business_name, gstin, pan, bank_account_id, kyc_status)
payouts (id, seller_id, amount, period_start, period_end, status, paid_at)

-- Reviews
reviews (id, order_item_id, user_id, rating, title, body, status, created_at)
```

---

## 12. API Overview

### REST API Conventions

- Base URL: `https://api.shopnow.in/v1`
- Auth: `Authorization: Bearer <JWT>`
- Pagination: cursor-based (`?cursor=<token>&limit=20`)
- Errors: RFC 7807 Problem Details format

### Key Endpoints (MVP)

| Method | Path | Description |
|--------|------|-------------|
| POST | `/auth/register` | Register new user |
| POST | `/auth/login/otp` | Login via mobile OTP |
| GET | `/products` | List / search products |
| GET | `/products/:id` | Product detail |
| POST | `/cart/items` | Add item to cart |
| GET | `/cart` | Get current cart |
| POST | `/orders` | Place order |
| GET | `/orders/:id` | Order detail + tracking |
| POST | `/orders/:id/return` | Initiate return |
| GET | `/seller/products` | Seller product list |
| POST | `/seller/products` | Create product listing |
| GET | `/seller/orders` | Seller order queue |
| PATCH | `/seller/orders/:id` | Update order status |
| GET | `/seller/payouts` | Payout history |

### Webhooks (Outbound)

| Event | Trigger |
|-------|---------|
| `order.placed` | Buyer places order |
| `order.shipped` | 3PL picks up shipment |
| `order.delivered` | Delivery confirmed |
| `payment.success` | Payment gateway confirms |
| `payment.failed` | Payment gateway rejects |
| `return.initiated` | Buyer starts return |
| `refund.completed` | Refund credited |

---

## 13. Security & Compliance

### Authentication & Authorisation
- JWT with RS256 signing; keys rotated every 90 days
- RBAC roles: `buyer`, `seller`, `seller_admin`, `support`, `admin`, `super_admin`
- OAuth 2.0 scopes for third-party seller integrations

### Data Privacy
- PII minimisation: store only what's operationally necessary
- Right to erasure: automated anonymisation pipeline within 30 days of request
- India DPDP Act 2023 compliance: consent management, data localisation
- Cookie consent banner with granular opt-in/opt-out

### Payment Security
- PCI-DSS SAQ-D: no raw PAN storage; card tokens via Razorpay Vault
- 3D Secure 2.0 (3DS2) for card transactions above ₹2,000
- UPI mandate compliance with NPCI guidelines

### Operational Security
- Secrets management via AWS Secrets Manager / HashiCorp Vault
- Dependency scanning in CI pipeline (Snyk / Dependabot)
- Quarterly penetration testing by external firm
- SOC 2 Type II audit target (Month 18)

---

## 14. Release Strategy

### Phase 1 — MVP (Month 1–6)

| Month | Milestone |
|-------|-----------|
| M1 | Auth, User Profile, Category & Product CRUD |
| M2 | Search, PLP, PDP, Cart |
| M3 | Checkout, Payment Integration (UPI + Card + COD) |
| M4 | Order Management, 3PL Integration, Notifications |
| M5 | Seller Portal v1, KYC, Inventory, Basic Analytics |
| M6 | Admin Panel, Reviews, Returns v1, Beta Launch |

### Phase 2 — Full Platform (Month 7–12)

| Month | Milestone |
|-------|-----------|
| M7 | Personalisation Engine, Advanced Search |
| M8 | iOS & Android Apps, Vernacular Support |
| M9 | Ads Platform v1 (Sponsored Products) |
| M10 | Loyalty Program, ShopNow Wallet |
| M11 | Seller Analytics v2, Forecasting Tools |
| M12 | Public Launch, Performance Hardening, SOC 2 Prep |

### Feature Flags
All major features are gated behind feature flags (LaunchDarkly / Unleash) to enable:
- Gradual rollout (1% → 10% → 50% → 100%)
- Instant kill-switch without deployment
- A/B testing of checkout and search variants

---

## 15. Risks & Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| Payment gateway downtime | Medium | Critical | Multi-gateway fallback; graceful degradation to alternative methods |
| Seller KYC fraud | Medium | High | Automated GST validation via govt API; manual spot-checks |
| Counterfeit products | High | High | Brand authorisation programme; AI image duplication detection; buyer reports |
| Search index corruption | Low | High | Daily snapshot; blue/green index with atomic alias swap |
| 3PL API latency | High | Medium | Async polling with exponential backoff; status cache with 5-min TTL |
| Data breach | Low | Critical | Encryption at rest/transit; WAF; quarterly pentest; incident response playbook |
| COD non-delivery fraud | Medium | Medium | Address validation; buyer history scoring; COD cap (₹10,000) for new users |
| Regulatory change (DPDP Act) | Medium | High | Privacy counsel on retainer; modular data processing pipeline |

---

## 16. Open Questions

| # | Question | Owner | Due |
|---|---------|-------|-----|
| Q1 | Which 3PL partners will be integrated at launch — Delhivery, Shiprocket, or both? | Ops Team | M1 Week 2 |
| Q2 | What is the initial commission rate structure by category? | Business | M1 Week 1 |
| Q3 | Should COD be available nationwide or restricted to tier-1/2 cities initially? | Risk/Ops | M2 |
| Q4 | Do we build the wallet in-house or integrate a third-party (e.g., Juspay)? | Engineering | M3 |
| Q5 | What is the seller payout SLA — T+7 or T+14 from delivery? | Finance | M1 |
| Q6 | Which ML infrastructure to use for Phase 2 recommendations — SageMaker or Vertex AI? | Engineering | M5 |
| Q7 | Will we support seller-managed shipping in addition to 3PL-managed? | Product | M2 |

---

## 17. Appendix

### A. Glossary

| Term | Definition |
|------|-----------|
| GMV | Gross Merchandise Value — total value of goods sold through the platform |
| SKU | Stock Keeping Unit — unique product variant identifier |
| BFF | Backend For Frontend — API layer tailored to a specific frontend client |
| 3PL | Third-Party Logistics — external fulfilment/shipping partner |
| PDP | Product Detail Page |
| PLP | Product Listing Page |
| COD | Cash on Delivery |
| UPI | Unified Payments Interface |
| DPDP | Digital Personal Data Protection Act (India, 2023) |
| AWB | Air Waybill — shipment tracking number |
| CPC | Cost Per Click — ad bidding model |

### B. Competitor Benchmarks

| Feature | Amazon IN | Flipkart | Meesho | ShopNow Target |
|---------|-----------|---------|--------|----------------|
| Seller Onboarding | 48 hrs | 24 hrs | 2 hrs | **< 2 hrs** |
| Seller Commission | 8–15% | 5–12% | 0–1.8% | **4–10%** |
| Payout Cycle | T+7 | T+7 | T+7 | **T+7** |
| Return Window | 7–30 days | 7–14 days | 7 days | **7–30 days** |
| Languages | 10 | 10 | 8 | **8 (Phase 2)** |

### C. Related Documents

- `ARCHITECTURE.md` — Detailed system design and ADRs
- `API_SPEC.md` — OpenAPI 3.1 specification
- `DESIGN_SYSTEM.md` — UI component library and brand guidelines
- `RUNBOOK.md` — Operational procedures and incident response
- `DATA_MODEL.md` — Complete ER diagram and migration scripts

---

*This PRD is a living document. Version history tracked in Git. All significant changes require stakeholder sign-off before implementation begins.*
