# Epics & User Stories
## ShopNow E-Commerce Platform

**Version:** 1.0  
**Status:** Draft  
**Owner:** Product / Engineering  
**Last Updated:** 2026-05-29  
**Related:** [PRD.md](./PRD.md) | [ARCHITECTURE.md](./ARCHITECTURE.md)

---

## Table of Contents

- [How to Read This Document](#how-to-read-this-document)
- [Epic Overview Map](#epic-overview-map)
- [Phase 1 — MVP Epics (Month 1–6)](#phase-1--mvp-epics-month-16)
  - [EPIC-01 User Authentication & Identity](#epic-01-user-authentication--identity)
  - [EPIC-02 Product Catalogue Management](#epic-02-product-catalogue-management)
  - [EPIC-03 Search & Discovery](#epic-03-search--discovery)
  - [EPIC-04 Cart & Wishlist](#epic-04-cart--wishlist)
  - [EPIC-05 Checkout & Payments](#epic-05-checkout--payments)
  - [EPIC-06 Order Management & Tracking](#epic-06-order-management--tracking)
  - [EPIC-07 Returns & Refunds](#epic-07-returns--refunds)
  - [EPIC-08 Ratings & Reviews](#epic-08-ratings--reviews)
  - [EPIC-09 Seller Portal](#epic-09-seller-portal)
  - [EPIC-10 Admin Panel & Platform Management](#epic-10-admin-panel--platform-management)
- [Phase 2 — Full Platform Epics (Month 7–12)](#phase-2--full-platform-epics-month-712)
  - [EPIC-11 Personalisation & Recommendations](#epic-11-personalisation--recommendations)
  - [EPIC-12 Mobile Apps (iOS & Android)](#epic-12-mobile-apps-ios--android)
  - [EPIC-13 Seller Analytics & Growth Tools](#epic-13-seller-analytics--growth-tools)
  - [EPIC-14 Sponsored Ads Platform](#epic-14-sponsored-ads-platform)
  - [EPIC-15 Loyalty Program & Wallet](#epic-15-loyalty-program--wallet)
  - [EPIC-16 Vernacular / Multi-language Support](#epic-16-vernacular--multi-language-support)
- [Story Point Reference](#story-point-reference)
- [Global Definition of Done](#global-definition-of-done)
- [Dependency Graph](#dependency-graph)

---

## How to Read This Document

### Story Format
```
STORY-ID | Title
As a [persona], I want [capability], so that [benefit].

Acceptance Criteria (AC):
  AC1: Given [context], when [action], then [outcome]
  AC2: ...

Story Points: N    Priority: Must/Should/Nice    Sprint Target: M1–S1
Dependencies: STORY-XX, STORY-YY
```

### Priority Legend

| Tag | Meaning |
|-----|---------|
| **Must Have** | MVP blocker — platform cannot launch without it |
| **Should Have** | High value; ship in MVP sprint if capacity allows |
| **Nice to Have** | Phase 2 candidate if not completed in Phase 1 |

### Story Point Scale

| Points | Effort |
|--------|--------|
| 1 | Trivial change (< 2 hours) |
| 2 | Small (half-day) |
| 3 | Medium (1 day) |
| 5 | Standard (2–3 days) |
| 8 | Large (4–5 days) |
| 13 | Extra-large (1 week+) — split if possible |

---

## Epic Overview Map

| Epic ID | Title | Phase | Squad | Stories | Est. Points |
|---------|-------|-------|-------|---------|-------------|
| EPIC-01 | User Authentication & Identity | 1 | Platform | 10 | 63 |
| EPIC-02 | Product Catalogue Management | 1 | Catalogue | 12 | 89 |
| EPIC-03 | Search & Discovery | 1 | Search | 8 | 55 |
| EPIC-04 | Cart & Wishlist | 1 | Commerce | 7 | 42 |
| EPIC-05 | Checkout & Payments | 1 | Payments | 12 | 96 |
| EPIC-06 | Order Management & Tracking | 1 | Orders | 11 | 81 |
| EPIC-07 | Returns & Refunds | 1 | Orders | 8 | 58 |
| EPIC-08 | Ratings & Reviews | 1 | Commerce | 7 | 40 |
| EPIC-09 | Seller Portal | 1 | Seller | 14 | 104 |
| EPIC-10 | Admin Panel & Platform Management | 1 | Platform | 10 | 68 |
| EPIC-11 | Personalisation & Recommendations | 2 | ML | 8 | 89 |
| EPIC-12 | Mobile Apps (iOS & Android) | 2 | Mobile | 10 | 104 |
| EPIC-13 | Seller Analytics & Growth Tools | 2 | Seller | 9 | 72 |
| EPIC-14 | Sponsored Ads Platform | 2 | Ads | 8 | 96 |
| EPIC-15 | Loyalty Program & Wallet | 2 | Commerce | 8 | 68 |
| EPIC-16 | Vernacular / Multi-language Support | 2 | Platform | 6 | 42 |
| | **TOTAL** | | | **148** | **1,167** |

---

## Phase 1 — MVP Epics (Month 1–6)

---

## EPIC-01: User Authentication & Identity

**Goal:** Allow buyers, sellers, and admins to securely register, log in, and manage their identities on the platform.  
**Business Value:** Zero revenue without trusted user accounts; foundational to every downstream feature.  
**Squad:** Platform  
**Target Months:** M1

---

### STORY-0101 — Buyer email & password registration

As a new buyer, I want to register with my email and password, so that I can create a personal shopping account.

**Acceptance Criteria:**
- AC1: Given a valid email + password (≥ 8 chars, 1 uppercase, 1 number), when I submit the form, then an account is created and a 6-digit OTP is sent to my email.
- AC2: Given I enter the correct OTP within 10 minutes, then my email is marked verified and I am redirected to the homepage.
- AC3: Given an already-registered email, when I submit the form, then I see "An account with this email already exists."
- AC4: Given an invalid password format, then inline validation shows the requirement not met in real time.
- AC5: Given OTP expires after 10 minutes, when I request a resend, then a new OTP is sent (max 3 resends per 30 minutes).

**Story Points:** 5 | **Priority:** Must Have | **Sprint:** M1-S1  
**Dependencies:** None

---

### STORY-0102 — Mobile OTP login (passwordless)

As a returning buyer, I want to log in using my mobile number and OTP, so that I don't need to remember a password.

**Acceptance Criteria:**
- AC1: Given a valid Indian mobile number (+91 format), when I request an OTP, then a 6-digit SMS OTP arrives within 30 seconds.
- AC2: Given the correct OTP, when I submit it within 10 minutes, then I receive an access token and refresh token.
- AC3: Given 5 failed OTP attempts in 30 minutes, then the account is temporarily locked for 15 minutes.
- AC4: Given a new mobile number not in the system, a new account is auto-created.

**Story Points:** 5 | **Priority:** Must Have | **Sprint:** M1-S1  
**Dependencies:** None

---

### STORY-0103 — Google OAuth2 login

As a buyer, I want to sign in with my Google account, so that I can skip the registration form.

**Acceptance Criteria:**
- AC1: Given I click "Sign in with Google," a Google OAuth2 consent screen opens.
- AC2: Given I approve and Google returns a valid id_token, then a ShopNow account is created/linked and I am logged in.
- AC3: Given the Google email already has a password account, then the accounts are merged and a merge notification email is sent.
- AC4: Given Google OAuth fails, then I see "Google sign-in is temporarily unavailable. Please try another method."

**Story Points:** 5 | **Priority:** Must Have | **Sprint:** M1-S1  
**Dependencies:** STORY-0101

---

### STORY-0104 — Apple OAuth2 login

As an iOS buyer, I want to sign in with Apple, so that I can use my existing Apple ID.

**Acceptance Criteria:**
- AC1: Given "Sign in with Apple" on web/iOS, when I authenticate with Face ID, then I am logged in within 5 seconds.
- AC2: Given Apple's "Hide My Email" option is selected, then a relay email is stored and all platform emails are routed through it.

**Story Points:** 5 | **Priority:** Must Have | **Sprint:** M1-S2  
**Dependencies:** STORY-0103

---

### STORY-0105 — JWT access token & refresh token flow

As the platform, I need short-lived access tokens with background refresh, so that sessions remain secure without forcing re-login.

**Acceptance Criteria:**
- AC1: Access token TTL = 15 minutes; refresh token TTL = 7 days.
- AC2: Given an expired access token, when the client calls `POST /auth/token/refresh` with a valid refresh token, then a new access token is returned.
- AC3: Given a refresh token is revoked (logout), then `POST /auth/token/refresh` returns 401.
- AC4: JWKS endpoint `/.well-known/jwks.json` is publicly accessible and rotates on schedule.

**Story Points:** 8 | **Priority:** Must Have | **Sprint:** M1-S1  
**Dependencies:** STORY-0101

---

### STORY-0106 — User profile management

As a logged-in buyer, I want to view and edit my profile (name, email, mobile), so that my account details stay up to date.

**Acceptance Criteria:**
- AC1: Given I navigate to My Account, I see name, email, mobile, and profile photo.
- AC2: Given I change my email, then an OTP is sent to the new email to verify before the change is committed.
- AC3: Given I upload a profile photo (≤ 2 MB, JPG/PNG), it is resized to 200×200 and stored in S3.

**Story Points:** 3 | **Priority:** Must Have | **Sprint:** M1-S2  
**Dependencies:** STORY-0101

---

### STORY-0107 — Address book management

As a buyer, I want to save multiple delivery addresses and set a default, so that checkout is faster on repeat orders.

**Acceptance Criteria:**
- AC1: Given I add an address with all required fields (name, phone, line1, city, state, pincode), it is saved and appears in my address book.
- AC2: Given I have multiple addresses, I can mark any one as default.
- AC3: Pincode field auto-fills city and state via pin-code lookup API.
- AC4: Maximum 10 saved addresses per account; on reaching limit, oldest non-default is removed or user is prompted to delete.

**Story Points:** 5 | **Priority:** Must Have | **Sprint:** M1-S2  
**Dependencies:** STORY-0101

---

### STORY-0108 — Guest checkout flow

As an unregistered visitor, I want to purchase without creating an account, so that I can buy without friction.

**Acceptance Criteria:**
- AC1: Given I proceed to checkout without logging in, I can enter an email + delivery address and complete purchase.
- AC2: After order confirmation, I am shown a prompt: "Create an account to track your order easily."
- AC3: If I create an account post-purchase using the same email, my order history is merged.

**Story Points:** 8 | **Priority:** Should Have | **Sprint:** M1-S3  
**Dependencies:** STORY-0101, STORY-0501

---

### STORY-0109 — Multi-factor authentication for sellers and admins

As a seller or admin, I need MFA on login, so that privileged accounts are protected against credential theft.

**Acceptance Criteria:**
- AC1: On first login after enablement, I am prompted to register a TOTP authenticator app (Google Authenticator / Authy).
- AC2: On every subsequent login, after entering my password, I must provide the 6-digit TOTP code.
- AC3: MFA is mandatory for all roles: seller, seller_admin, support, admin, super_admin. It is optional for buyers.
- AC4: Given a lost authenticator, I can use a one-time recovery code (10 codes generated at MFA setup).

**Story Points:** 8 | **Priority:** Must Have | **Sprint:** M1-S2  
**Dependencies:** STORY-0101

---

### STORY-0110 — Logout and session revocation

As a buyer, I want to log out of my current session or all sessions, so that I can secure my account if my device is lost.

**Acceptance Criteria:**
- AC1: Clicking "Logout" invalidates the current refresh token and clears local tokens.
- AC2: "Logout of all devices" revokes all active refresh tokens for my account.
- AC3: After logout, any request with the old access token returns 401 within 15 minutes (when the token expires).

**Story Points:** 3 | **Priority:** Must Have | **Sprint:** M1-S2  
**Dependencies:** STORY-0105

---

## EPIC-02: Product Catalogue Management

**Goal:** Allow sellers to create, publish, and manage product listings with rich content; allow the platform to organise products into a navigable category hierarchy.  
**Business Value:** Without a catalogue, there is nothing to sell. Catalogue quality directly drives conversion.  
**Squad:** Catalogue  
**Target Months:** M1–M2

---

### STORY-0201 — Category tree management (admin)

As a platform admin, I want to create and manage a hierarchical category tree, so that products are organised for easy navigation.

**Acceptance Criteria:**
- AC1: I can create a category with name, slug, parent category, and a JSON schema defining required product attributes.
- AC2: The tree supports unlimited depth but the UI enforces a 4-level maximum (root → L1 → L2 → leaf).
- AC3: Deleting a category with active products is blocked; I must reassign products first.
- AC4: Category reordering via drag-and-drop updates `sort_order`.

**Story Points:** 8 | **Priority:** Must Have | **Sprint:** M1-S1  
**Dependencies:** EPIC-10

---

### STORY-0202 — Single product listing creation (seller)

As a seller, I want to create a product listing with title, description, images, and variants, so that buyers can find and purchase my products.

**Acceptance Criteria:**
- AC1: I can enter product title (≤ 500 chars), description (rich text, ≤ 5,000 chars), brand, and select a leaf category.
- AC2: I can add up to 8 images (JPG/PNG/WebP, ≤ 5 MB each) and 1 video (MP4, ≤ 50 MB). First image becomes the thumbnail.
- AC3: I can define variants (colour, size, etc.) with per-variant SKU, price, MRP, and stock quantity.
- AC4: Dynamic attribute fields appear based on the selected category schema (e.g., "Screen Size" appears for Mobiles).
- AC5: Product is saved as "draft" until I explicitly click "Submit for Review" → status transitions to "pending_review."
- AC6: Images are compressed to WebP and stored in S3; CDN URLs are returned.

**Story Points:** 13 | **Priority:** Must Have | **Sprint:** M1-S2  
**Dependencies:** STORY-0201, STORY-0901

---

### STORY-0203 — Bulk product upload via CSV

As a seller with a large catalogue, I want to upload products via CSV, so that I don't have to create hundreds of listings manually.

**Acceptance Criteria:**
- AC1: I can download a category-specific CSV template with required and optional columns.
- AC2: I can upload a CSV (≤ 50,000 rows, ≤ 25 MB).
- AC3: After upload, an async validation job runs; within 5 minutes I receive an email with a row-level error report.
- AC4: Valid rows are imported as draft products; rows with errors are skipped and listed in the report.
- AC5: I can re-upload a corrected file for failed rows without duplicating successful rows (idempotent via SKU matching).

**Story Points:** 13 | **Priority:** Must Have | **Sprint:** M2-S1  
**Dependencies:** STORY-0202

---

### STORY-0204 — Product listing review & approval (admin)

As a platform admin, I want to review submitted product listings before they go live, so that only quality, policy-compliant products are published.

**Acceptance Criteria:**
- AC1: The admin review queue shows all `pending_review` products with seller name, category, and submission time.
- AC2: I can approve a listing (status → `active`) or reject it with a mandatory reason (displayed to seller).
- AC3: Approved products are indexed in OpenSearch within 60 seconds.
- AC4: Seller receives an in-app notification and email on approval or rejection.
- AC5: Auto-approve can be enabled per seller tier (trusted sellers bypass review queue).

**Story Points:** 8 | **Priority:** Must Have | **Sprint:** M1-S3  
**Dependencies:** STORY-0202, EPIC-10

---

### STORY-0205 — Product detail page (buyer)

As a buyer, I want to see a rich product detail page, so that I have all the information I need to make a purchase decision.

**Acceptance Criteria:**
- AC1: Page displays: title, brand, all images (zoomable), video, price, MRP, discount percentage, stock status, seller name, and all variant attributes.
- AC2: Selecting a variant (e.g., "Red / XL") updates price, MRP, stock status, and images without a full page reload.
- AC3: If stock is 0, the "Add to Cart" button is replaced with "Notify Me When Available."
- AC4: Page loads in < 2 seconds (P95) via ISR caching with 30-second revalidation.
- AC5: Page includes structured data (JSON-LD) for Product schema for SEO.
- AC6: Breadcrumb navigation reflects the full category path.

**Story Points:** 8 | **Priority:** Must Have | **Sprint:** M2-S1  
**Dependencies:** STORY-0202

---

### STORY-0206 — Product listing page with filters (buyer)

As a buyer, I want to browse products in a category with filters and sorting, so that I can narrow down to what I want quickly.

**Acceptance Criteria:**
- AC1: Page shows a product grid with thumbnail, title, price, rating, and "Add to Cart."
- AC2: Faceted filters available: price range (slider), brand (multi-select), average rating (1–5 stars), delivery (same-day / next-day), discount percentage.
- AC3: Applying a filter updates results without a full page reload (client-side with URL params synced).
- AC4: Sort options: Relevance, Price: Low to High, Price: High to Low, Newest First, Avg. Customer Review.
- AC5: Pagination: 24 products per page; infinite scroll on mobile.
- AC6: Active filters are shown as removable chips above the grid.

**Story Points:** 8 | **Priority:** Must Have | **Sprint:** M2-S1  
**Dependencies:** STORY-0205, STORY-0301

---

### STORY-0207 — Inventory management (seller)

As a seller, I want to update stock quantities and receive low-stock alerts, so that I can avoid overselling.

**Acceptance Criteria:**
- AC1: From my seller dashboard I can edit stock quantity per variant and save.
- AC2: When stock reaches a configurable threshold (default: 5 units), I receive an email and in-app alert.
- AC3: When stock reaches 0, the variant is automatically marked out-of-stock and the "Add to Cart" button is hidden on the PDP.
- AC4: Inventory changes triggered by order placement and return receipt are applied atomically (no race conditions).

**Story Points:** 5 | **Priority:** Must Have | **Sprint:** M2-S2  
**Dependencies:** STORY-0202

---

### STORY-0208 — Edit and deactivate product listing (seller)

As a seller, I want to edit or deactivate a live listing, so that I can keep my catalogue accurate.

**Acceptance Criteria:**
- AC1: I can edit title, description, images, price, MRP, and attributes of an active product.
- AC2: Price/stock edits go live immediately; content edits (title, description) go back to `pending_review` if auto-approve is not enabled.
- AC3: Deactivating a listing removes it from search results within 60 seconds and shows "Currently Unavailable" on the PDP.
- AC4: Products in active orders cannot be fully deleted; only deactivated.

**Story Points:** 5 | **Priority:** Must Have | **Sprint:** M2-S2  
**Dependencies:** STORY-0202

---

### STORY-0209 — Product image CDN and compression pipeline

As the platform, I need product images compressed and served via CDN, so that page load times remain fast.

**Acceptance Criteria:**
- AC1: On upload, images are converted to WebP and resized to three variants: thumbnail (200×200), card (600×600), full (1200×1200).
- AC2: Images are stored in S3 and served via CloudFront with a 1-year cache TTL.
- AC3: Time from upload to CDN-available URL < 30 seconds.
- AC4: Original image is preserved in S3 for future re-processing.

**Story Points:** 8 | **Priority:** Must Have | **Sprint:** M1-S2  
**Dependencies:** None

---

### STORY-0210 — Product variant grouping

As a buyer, I want colour and size variants displayed as selectable swatches on the PDP, so that I can explore options without navigating to a new page.

**Acceptance Criteria:**
- AC1: Variants sharing the same parent product are displayed as swatches (colour) or buttons (size).
- AC2: Unavailable variants are shown but visually greyed out with a strikethrough on price.
- AC3: Switching variants updates the URL with the variant ID for shareable deep links.

**Story Points:** 5 | **Priority:** Must Have | **Sprint:** M2-S1  
**Dependencies:** STORY-0205

---

### STORY-0211 — Dynamic pricing: flash sales & discounts (seller)

As a seller, I want to create time-limited discounts on my products, so that I can run promotions to boost sales.

**Acceptance Criteria:**
- AC1: I can set a sale price and sale start/end date-time per variant.
- AC2: A countdown timer is shown on the PDP when an active flash sale exists.
- AC3: Sale price is validated to be ≥ cost_price if cost_price is provided (anti-abuse check).
- AC4: The original price and discount percentage are displayed alongside the sale price.
- AC5: When sale ends, price reverts to regular price automatically.

**Story Points:** 8 | **Priority:** Should Have | **Sprint:** M3-S1  
**Dependencies:** STORY-0202, STORY-0205

---

### STORY-0212 — "Notify Me When Available" for out-of-stock variants

As a buyer, I want to be notified when an out-of-stock product is restocked, so that I don't have to keep checking manually.

**Acceptance Criteria:**
- AC1: On an out-of-stock PDP, a "Notify Me" button is visible to logged-in buyers.
- AC2: When the seller restocks (stock > 0), all subscribed buyers receive an email/push notification within 15 minutes.
- AC3: The notification includes the product name, image, current price, and a deep link to the PDP.
- AC4: Maximum 1 email per 24 hours per product per buyer (deduplication).

**Story Points:** 5 | **Priority:** Should Have | **Sprint:** M3-S2  
**Dependencies:** STORY-0207

---

## EPIC-03: Search & Discovery

**Goal:** Enable buyers to find products quickly through keyword search, autocomplete, and faceted filtering.  
**Business Value:** 43% of e-commerce sessions begin with search. Search quality is the single biggest driver of conversion.  
**Squad:** Search  
**Target Months:** M2

---

### STORY-0301 — Full-text product search

As a buyer, I want to type a keyword and see relevant products, so that I can find what I'm looking for without browsing categories.

**Acceptance Criteria:**
- AC1: Search returns results in < 300 ms (P95) for queries matching indexed products.
- AC2: Results are ranked by relevance (BM25 + seller rating boost + sales velocity boost).
- AC3: Typo tolerance handles 1-character edits (e.g., "iphon" → iPhone results).
- AC4: Synonym support (e.g., "mobile" = "phone" = "smartphone").
- AC5: Empty query returns zero results with a "Start typing to search" prompt.
- AC6: Search result page URL is shareable (query encoded in URL params).

**Story Points:** 13 | **Priority:** Must Have | **Sprint:** M2-S1  
**Dependencies:** STORY-0202, STORY-0209

---

### STORY-0302 — Autocomplete / type-ahead suggestions

As a buyer, I want to see search suggestions as I type, so that I can find popular searches faster.

**Acceptance Criteria:**
- AC1: After 2+ characters, up to 8 suggestions appear in a dropdown within 100 ms.
- AC2: Suggestions include: popular search terms, category name matches, and matching product titles.
- AC3: Pressing arrow keys navigates the suggestions list; Enter submits; Escape closes the dropdown.
- AC4: "Recent searches" (last 5) appear when the search box is focused with no text.

**Story Points:** 5 | **Priority:** Must Have | **Sprint:** M2-S1  
**Dependencies:** STORY-0301

---

### STORY-0303 — Search result faceted filtering

As a buyer on the search results page, I want to filter results by price, brand, and rating, so that I narrow down to relevant products.

**Acceptance Criteria:**
- AC1: Filters available: Price Range (slider), Brand (multi-select, shows count), Rating (≥ 4★, ≥ 3★), Discount (≥ 10%, ≥ 25%), Category (breadcrumb refinement).
- AC2: Applying a filter re-queries OpenSearch and updates results without full page reload.
- AC3: Filter counts update dynamically based on current active filters (disjunctive facet counts).
- AC4: URL params reflect all active filters for shareability and back-button support.

**Story Points:** 8 | **Priority:** Must Have | **Sprint:** M2-S2  
**Dependencies:** STORY-0301

---

### STORY-0304 — Search index sync pipeline

As the platform, I need product changes to appear in search within 60 seconds, so that buyers always see current information.

**Acceptance Criteria:**
- AC1: Debezium CDC captures changes to `products` and `product_variants` tables.
- AC2: Changes are published to Kafka topic `catalogue.product.events`.
- AC3: OpenSearch Kafka Connector consumes the topic and updates the index.
- AC4: End-to-end latency (DB write → searchable) < 60 seconds in P99.
- AC5: A full re-index job runs nightly at 02:00 UTC on a staging alias; alias swapped atomically post-validation.

**Story Points:** 8 | **Priority:** Must Have | **Sprint:** M2-S1  
**Dependencies:** STORY-0202

---

### STORY-0305 — Zero-results page with fallback suggestions

As a buyer who searches for something not found, I want helpful fallback suggestions, so that I don't hit a dead end.

**Acceptance Criteria:**
- AC1: When zero results, the page shows: "No results for [query]." + spelling correction if detected + popular categories + trending products.
- AC2: "Did you mean [corrected query]?" link runs a new search.
- AC3: Zero-results events are logged for catalogue gap analysis.

**Story Points:** 3 | **Priority:** Should Have | **Sprint:** M2-S3  
**Dependencies:** STORY-0301

---

### STORY-0306 — Voice search

As a mobile buyer, I want to search using my voice, so that I can search hands-free.

**Acceptance Criteria:**
- AC1: Tapping the microphone icon triggers browser/native speech recognition.
- AC2: Recognised text populates the search input and triggers a search.
- AC3: Displayed only on browsers/devices that support the Web Speech API or native equivalent.

**Story Points:** 5 | **Priority:** Should Have | **Sprint:** M3-S1  
**Dependencies:** STORY-0301

---

### STORY-0307 — Search analytics & query logging

As the platform, I need search query logs, so that we can identify high-volume zero-result queries and improve the catalogue.

**Acceptance Criteria:**
- AC1: Every search query (with result count, selected result position, user ID if logged in) is published to `analytics.event.raw` Kafka topic.
- AC2: A ClickHouse dashboard shows: top queries, zero-result queries, CTR by result position.
- AC3: No PII (email, name) is stored in query logs.

**Story Points:** 5 | **Priority:** Must Have | **Sprint:** M2-S2  
**Dependencies:** STORY-0301

---

### STORY-0308 — Category browse navigation

As a buyer, I want to browse the product catalogue by category using a navigation menu, so that I can discover products I didn't know to search for.

**Acceptance Criteria:**
- AC1: A mega-menu shows L1 categories; hovering expands L2 and L3 sub-categories.
- AC2: Clicking any category opens the PLP filtered to that category.
- AC3: Category tree is cached in Redis with a 1-hour TTL.
- AC4: On mobile, the mega-menu is replaced with a full-screen slide-out drawer.

**Story Points:** 8 | **Priority:** Must Have | **Sprint:** M2-S1  
**Dependencies:** STORY-0201

---

## EPIC-04: Cart & Wishlist

**Goal:** Allow buyers to collect products before purchasing and save items for later.  
**Business Value:** Cart is the entry point to the checkout funnel. Persistent carts reduce abandonment.  
**Squad:** Commerce  
**Target Months:** M2–M3

---

### STORY-0401 — Add to cart and cart management

As a buyer, I want to add products to my cart and manage quantities, so that I can prepare my order before paying.

**Acceptance Criteria:**
- AC1: Clicking "Add to Cart" on PDP or PLP adds the selected variant (default if none selected) to the cart.
- AC2: Cart drawer slides in from the right showing all items, quantities, subtotal, and a "Proceed to Checkout" button.
- AC3: I can change item quantity (1–99) or remove items.
- AC4: If I add a product from a different seller, it is added as a separate shipment group within the same cart (shown visually).
- AC5: Adding an out-of-stock variant shows a toast: "Sorry, this item is out of stock."

**Story Points:** 8 | **Priority:** Must Have | **Sprint:** M2-S2  
**Dependencies:** STORY-0202, STORY-0105

---

### STORY-0402 — Persistent cart (cross-device sync)

As a logged-in buyer, I want my cart to persist across devices and sessions, so that I can add on mobile and checkout on desktop.

**Acceptance Criteria:**
- AC1: Cart state is stored in Redis keyed by `user_id` and synced to PostgreSQL every 5 minutes.
- AC2: Logging in from a new device shows the same cart items.
- AC3: Cart items expire after 30 days of inactivity.
- AC4: If a cart item's price changes while in cart, a notice is shown: "Price updated since you added this item."

**Story Points:** 5 | **Priority:** Must Have | **Sprint:** M2-S2  
**Dependencies:** STORY-0401, STORY-0105

---

### STORY-0403 — Guest cart merge on login

As a guest buyer who added items to cart before logging in, I want my cart items to be preserved after login, so that I don't lose my selections.

**Acceptance Criteria:**
- AC1: Guest cart is keyed by `session_id` stored in a cookie.
- AC2: On login, the guest cart is merged with the existing user cart (no duplicate SKUs; quantity summed if same variant).
- AC3: Merged cart is visible immediately after login without page refresh.

**Story Points:** 5 | **Priority:** Must Have | **Sprint:** M2-S3  
**Dependencies:** STORY-0401, STORY-0402

---

### STORY-0404 — Coupon code application

As a buyer, I want to apply a coupon code at checkout, so that I can get a discount on my order.

**Acceptance Criteria:**
- AC1: A coupon code input field is visible in the cart and checkout pages.
- AC2: On applying a valid code, the discount amount is shown and subtracted from the total.
- AC3: On applying an invalid/expired code, an error message describes why: "Code expired," "Minimum order not met (₹500 required)," etc.
- AC4: Only one coupon can be active at a time. Applying a new one replaces the existing one.
- AC5: Coupon validity is checked against the Promotion Service (not client-side).

**Story Points:** 8 | **Priority:** Must Have | **Sprint:** M3-S1  
**Dependencies:** STORY-0401

---

### STORY-0405 — Wishlist management

As a buyer, I want to save products to a wishlist, so that I can come back to them later.

**Acceptance Criteria:**
- AC1: A heart icon on PDP and PLP cards toggles the product in/out of my wishlist.
- AC2: The Wishlist page shows all saved items with current price, availability, and an "Add to Cart" button.
- AC3: If a wishlisted item's price drops by ≥ 10%, I receive an email notification.
- AC4: Wishlist has a shareable link (public URL); recipient sees the list but cannot edit it.
- AC5: Maximum 200 items per wishlist.

**Story Points:** 5 | **Priority:** Should Have | **Sprint:** M3-S1  
**Dependencies:** STORY-0401

---

### STORY-0406 — Save for later from cart

As a buyer, I want to move a cart item to a "saved for later" list, so that I can reduce my cart total without losing the item.

**Acceptance Criteria:**
- AC1: Each cart item has a "Save for Later" link; clicking it moves the item out of the active cart.
- AC2: Saved items appear in a section below the cart with "Move to Cart" option.
- AC3: Saved items count toward the 200-item wishlist limit.

**Story Points:** 3 | **Priority:** Should Have | **Sprint:** M3-S2  
**Dependencies:** STORY-0401, STORY-0405

---

### STORY-0407 — Real-time price recalculation in cart

As a buyer, I want cart totals to recalculate when I change quantities or apply coupons, so that I always see an accurate total.

**Acceptance Criteria:**
- AC1: Changing quantity updates the line total and cart subtotal within 200 ms.
- AC2: Tax (GST) is calculated and broken out per item based on the product's HSN code and buyer's state.
- AC3: Shipping estimate is shown per seller shipment group based on destination pincode.

**Story Points:** 5 | **Priority:** Must Have | **Sprint:** M2-S3  
**Dependencies:** STORY-0401, STORY-0404

---

## EPIC-05: Checkout & Payments

**Goal:** Convert cart into a confirmed, paid order through a secure, multi-step checkout flow supporting multiple payment methods.  
**Business Value:** Payment conversion is the revenue realisation step. Every percentage point of improvement = significant GMV.  
**Squad:** Payments  
**Target Months:** M3

---

### STORY-0501 — Single-page checkout flow

As a buyer, I want to complete checkout in a clear, minimal flow, so that I can place an order without confusion.

**Acceptance Criteria:**
- AC1: Checkout is a single-page flow with three distinct steps shown as a progress bar: (1) Address, (2) Payment, (3) Review & Place Order.
- AC2: Each step validates before advancing; user cannot skip steps.
- AC3: Review step shows: all items with images, selected address, payment method, subtotal, discount, tax, shipping, and total.
- AC4: Checkout page loads in < 2 seconds (P95) and is not cached (CSR only).
- AC5: On mobile, the order summary is collapsible to save screen space.

**Story Points:** 8 | **Priority:** Must Have | **Sprint:** M3-S1  
**Dependencies:** STORY-0401, STORY-0107

---

### STORY-0502 — UPI payment integration

As a buyer, I want to pay via UPI (VPA or QR), so that I can use my preferred payment app.

**Acceptance Criteria:**
- AC1: I can enter a UPI VPA (e.g., user@ybl) and receive a payment request on my UPI app.
- AC2: A QR code is generated for scan-and-pay via any UPI app.
- AC3: Payment status is polled every 5 seconds for up to 5 minutes; if not completed, payment is marked as timed out.
- AC4: On success, I am redirected to the order confirmation page within 3 seconds.
- AC5: On failure, I see: "Payment failed — [reason from gateway]" with options to retry or choose a different method.

**Story Points:** 8 | **Priority:** Must Have | **Sprint:** M3-S1  
**Dependencies:** STORY-0501

---

### STORY-0503 — Credit/debit card payment

As a buyer, I want to pay by credit or debit card, so that I can use my bank card.

**Acceptance Criteria:**
- AC1: Card details are entered via Razorpay.js hosted fields (no raw card data touches our servers).
- AC2: 3DS2 challenge is triggered for cards where the transaction exceeds ₹2,000.
- AC3: On successful payment, order is confirmed; on decline, a clear message is shown (e.g., "Insufficient funds").
- AC4: I can save my card (tokenised) for future use with a "Save this card" checkbox.
- AC5: Saved cards show last 4 digits and card network logo.

**Story Points:** 8 | **Priority:** Must Have | **Sprint:** M3-S1  
**Dependencies:** STORY-0501

---

### STORY-0504 — Cash on Delivery (COD)

As a buyer, I want to pay cash when my order is delivered, so that I don't need to share card or bank details online.

**Acceptance Criteria:**
- AC1: COD is offered as a payment option when the destination pincode is serviceable by a COD-capable 3PL.
- AC2: COD is not offered if: the order total exceeds ₹10,000 for new accounts (< 3 prior orders), or the buyer has 2+ past COD returns.
- AC3: Selecting COD shows an info message: "Pay ₹[amount] in cash at the time of delivery."
- AC4: COD orders do not require a payment gateway call; the order is confirmed immediately on placement.

**Story Points:** 5 | **Priority:** Must Have | **Sprint:** M3-S1  
**Dependencies:** STORY-0501

---

### STORY-0505 — Net banking payment

As a buyer, I want to pay via net banking from my bank account, so that I have a direct bank transfer option.

**Acceptance Criteria:**
- AC1: A searchable list of 20+ banks is shown with bank logos.
- AC2: Selecting a bank redirects to the bank's net banking portal via Razorpay.
- AC3: On return (success or failure), the buyer is redirected to the appropriate confirmation page.

**Story Points:** 3 | **Priority:** Must Have | **Sprint:** M3-S1  
**Dependencies:** STORY-0501

---

### STORY-0506 — EMI payment options

As a buyer with a credit card, I want to pay in equal monthly instalments, so that I can afford high-value purchases.

**Acceptance Criteria:**
- AC1: For order totals ≥ ₹2,000, EMI options (3/6/9/12 months) are shown per eligible bank.
- AC2: Each EMI option shows the monthly instalment amount and total interest payable.
- AC3: No-cost EMI (merchant-subsidised) is flagged with a "0% interest" badge.
- AC4: EMI processing uses Razorpay's EMI product APIs.

**Story Points:** 8 | **Priority:** Must Have | **Sprint:** M3-S2  
**Dependencies:** STORY-0503

---

### STORY-0507 — Payment retry and gateway fallback

As the platform, I need automatic payment retry with gateway fallback, so that transient gateway failures don't block successful payments.

**Acceptance Criteria:**
- AC1: If the primary gateway (Razorpay) returns a 5xx error, the payment is retried on the secondary gateway (Cashfree) within 2 seconds.
- AC2: Retry is transparent to the buyer; they do not see a failure unless all gateways fail.
- AC3: A single payment intent is never charged twice (idempotency enforced via payment_intent_id).
- AC4: All gateway attempts (success/failure) are logged for reconciliation.

**Story Points:** 8 | **Priority:** Must Have | **Sprint:** M3-S2  
**Dependencies:** STORY-0502, STORY-0503

---

### STORY-0508 — Payment webhook processing

As the platform, I need to receive and process payment status webhooks from gateways, so that order status is updated accurately.

**Acceptance Criteria:**
- AC1: Each gateway webhook endpoint validates the HMAC-SHA256 signature before processing.
- AC2: Webhook processing is idempotent (duplicate webhooks for the same transaction ID have no effect).
- AC3: On `payment.captured` webhook, Order Service is notified via Kafka event to transition order to `CONFIRMED`.
- AC4: On `payment.failed`, Order Service transitions to `PAYMENT_FAILED` and buyer is notified.
- AC5: Unprocessable webhooks are moved to a DLQ with alert.

**Story Points:** 8 | **Priority:** Must Have | **Sprint:** M3-S1  
**Dependencies:** STORY-0502

---

### STORY-0509 — Order confirmation page

As a buyer, I want a clear order confirmation page after payment, so that I have immediate proof of my purchase.

**Acceptance Criteria:**
- AC1: Page shows: order ID, estimated delivery date, itemised list, payment method used, total paid, and delivery address.
- AC2: A "Download Invoice" button generates and downloads a PDF invoice (GST-compliant format).
- AC3: A confirmation email is sent within 60 seconds of order placement.
- AC4: Order confirmation is reachable via a unique URL for 30 days post-order.

**Story Points:** 5 | **Priority:** Must Have | **Sprint:** M3-S2  
**Dependencies:** STORY-0501

---

### STORY-0510 — Buy Now Pay Later (BNPL)

As a buyer, I want BNPL payment options, so that I can split payment interest-free over a short term.

**Acceptance Criteria:**
- AC1: BNPL options (Simpl, LazyPay) are shown at checkout for eligible buyers.
- AC2: Eligibility check is performed via the BNPL provider's API (silent call, < 1 second).
- AC3: Approved buyers complete payment on the BNPL provider's screen.

**Story Points:** 8 | **Priority:** Should Have | **Sprint:** M4-S1  
**Dependencies:** STORY-0501

---

### STORY-0511 — Payment reconciliation job

As the platform finance team, I need automated reconciliation between our payment records and gateway settlement reports, so that discrepancies are caught daily.

**Acceptance Criteria:**
- AC1: A nightly job fetches the gateway settlement report for the previous day.
- AC2: The job compares each settlement with our `payments` table; any mismatch (amount, status) is flagged in the reconciliation table.
- AC3: A daily reconciliation summary email is sent to the finance team.
- AC4: Unmatched items older than 3 days trigger a PagerDuty alert.

**Story Points:** 8 | **Priority:** Must Have | **Sprint:** M4-S2  
**Dependencies:** STORY-0508

---

### STORY-0512 — Address selection in checkout

As a buyer at checkout, I want to choose a saved address or add a new one, so that my order goes to the right place.

**Acceptance Criteria:**
- AC1: My saved addresses are listed with the default pre-selected.
- AC2: I can add a new address inline during checkout without leaving the page.
- AC3: Pincode validation confirms the pin is serviceable (API call to 3PL). Unserviceable pincodes show: "Delivery not available to this pincode."

**Story Points:** 5 | **Priority:** Must Have | **Sprint:** M3-S1  
**Dependencies:** STORY-0107, STORY-0501

---

## EPIC-06: Order Management & Tracking

**Goal:** Allow buyers to track their orders in real time; allow sellers to manage fulfilment; ensure both parties have full order visibility.  
**Business Value:** Post-purchase experience drives retention. 70% of buyers check order status at least twice per order.  
**Squad:** Orders  
**Target Months:** M4

---

### STORY-0601 — My orders list

As a buyer, I want to see a list of all my orders, so that I can track and manage them from one place.

**Acceptance Criteria:**
- AC1: Orders are listed in reverse chronological order with: order ID, date, item thumbnails, total, and current status badge.
- AC2: Filter by status: All, Active, Delivered, Cancelled, Returns.
- AC3: Search by order ID.
- AC4: Each order row links to the order detail page.
- AC5: Paginated at 10 orders per page.

**Story Points:** 5 | **Priority:** Must Have | **Sprint:** M4-S1  
**Dependencies:** STORY-0509

---

### STORY-0602 — Order detail page with real-time status

As a buyer, I want to see the full status and history of a specific order, so that I know exactly where my package is.

**Acceptance Criteria:**
- AC1: Page shows: all items, current status step in a visual timeline (Placed → Confirmed → Shipped → Out for Delivery → Delivered), expected delivery date, shipment tracking number, and delivery address.
- AC2: Timeline auto-refreshes every 60 seconds without a full page reload.
- AC3: Each status transition shows a timestamp.
- AC4: A "Track Shipment" button deep-links to the 3PL's live tracking page.
- AC5: If an order has multiple sellers/shipments, each shipment is shown as a separate tracking row.

**Story Points:** 8 | **Priority:** Must Have | **Sprint:** M4-S1  
**Dependencies:** STORY-0601

---

### STORY-0603 — Real-time shipment tracking via 3PL API

As a buyer, I want live tracking updates from the logistics provider, so that I know when my package will arrive.

**Acceptance Criteria:**
- AC1: Platform polls Delhivery and Shiprocket APIs every 15 minutes for active shipments.
- AC2: Tracking events are stored in `shipment_tracking_events` table and surfaced on the order detail page.
- AC3: "Out for Delivery" event triggers a push notification and SMS to the buyer.
- AC4: If 3PL API is unavailable, last known status is shown with a "Last updated: [time]" label.

**Story Points:** 13 | **Priority:** Must Have | **Sprint:** M4-S1  
**Dependencies:** STORY-0602

---

### STORY-0604 — Order status push, SMS, and email notifications

As a buyer, I want to receive notifications at each order milestone, so that I'm informed without having to check the app.

**Acceptance Criteria:**
- AC1: Notification sent at: Order Confirmed, Order Shipped (with tracking number), Out for Delivery, Delivered, Cancelled.
- AC2: Notifications are sent via Email (all events), SMS (Shipped, Out for Delivery, Delivered), and Push (all events if app installed).
- AC3: Buyer can opt out of SMS notifications from account settings; email and push cannot be fully disabled for transactional events.
- AC4: Notification delivery is async (Kafka consumer); failure to send notification does not block order processing.

**Story Points:** 8 | **Priority:** Must Have | **Sprint:** M4-S1  
**Dependencies:** STORY-0602

---

### STORY-0605 — Order cancellation by buyer

As a buyer, I want to cancel an order before it is shipped, so that I can change my mind without incurring a return.

**Acceptance Criteria:**
- AC1: Cancellation is available if order status is `CONFIRMED` or `PROCESSING`.
- AC2: Buyer selects a cancellation reason from a list (changed mind, ordered by mistake, found better price, other).
- AC3: On cancellation, order status → `CANCELLED`; inventory is restocked; refund is initiated automatically.
- AC4: If order is already `SHIPPED`, cancellation is not allowed; the buyer is advised to initiate a return after delivery.
- AC5: Cancellation confirmation email is sent within 5 minutes.

**Story Points:** 5 | **Priority:** Must Have | **Sprint:** M4-S2  
**Dependencies:** STORY-0602

---

### STORY-0606 — Seller order fulfilment dashboard

As a seller, I want to view incoming orders and update their fulfilment status, so that I can pack and dispatch orders efficiently.

**Acceptance Criteria:**
- AC1: Dashboard shows orders in queue tabs: New Orders, Processing, Ready to Ship, Shipped, Delivered.
- AC2: Clicking an order shows item details, buyer's delivery pincode (not full address), and a "Print Packing Slip" button.
- AC3: I can click "Mark as Packed" → "Generate Shipping Label" → "Mark as Dispatched" (entering the AWB number).
- AC4: Each status update publishes an event to Kafka, which updates the buyer's tracking page.
- AC5: New orders trigger an email and in-app alert to the seller.

**Story Points:** 13 | **Priority:** Must Have | **Sprint:** M4-S1  
**Dependencies:** STORY-0509, STORY-0902

---

### STORY-0607 — Shipping label generation

As a seller, I want to generate a printable shipping label, so that I can hand parcels to the 3PL courier.

**Acceptance Criteria:**
- AC1: Clicking "Generate Label" calls the 3PL API with pickup address, delivery address, and package weight.
- AC2: A PDF label (A5 size) is returned and offered for download/print.
- AC3: The AWB number from the label is auto-populated in the dispatch form.
- AC4: If the 3PL API fails, an error is shown and the seller is advised to retry in 5 minutes.

**Story Points:** 8 | **Priority:** Must Have | **Sprint:** M4-S2  
**Dependencies:** STORY-0606

---

### STORY-0608 — Seller order SLA alerts

As a seller, I want alerts when I haven't dispatched an order within the SLA (24 hours), so that I avoid penalties.

**Acceptance Criteria:**
- AC1: If an order remains in `PROCESSING` for > 20 hours, a warning notification is sent.
- AC2: If an order remains in `PROCESSING` for > 24 hours, a critical alert is sent and the admin is notified.
- AC3: Repeated SLA violations affect the seller's performance score.

**Story Points:** 5 | **Priority:** Should Have | **Sprint:** M4-S3  
**Dependencies:** STORY-0606

---

### STORY-0609 — GST-compliant invoice generation

As a buyer and seller, I want orders to generate a GST-compliant invoice, so that I have proof of purchase for tax purposes.

**Acceptance Criteria:**
- AC1: Invoice includes: seller GSTIN, buyer name, delivery address, itemised HSN codes, CGST/SGST/IGST breakdown, invoice number, and order date.
- AC2: Invoice is generated as a PDF stored in S3; a download link is included in the order confirmation email.
- AC3: Seller can download all invoices for a period from the Seller Portal.

**Story Points:** 8 | **Priority:** Must Have | **Sprint:** M3-S3  
**Dependencies:** STORY-0509

---

### STORY-0610 — Multi-shipment order handling

As a buyer who ordered from multiple sellers, I want to see individual shipment tracking per seller, so that I know when each parcel will arrive.

**Acceptance Criteria:**
- AC1: A multi-seller cart creates a single order with multiple `order_items`, each assigned to a seller.
- AC2: Shipments are created per seller; each has its own tracking number and status timeline.
- AC3: The order detail page groups items by shipment with individual tracking rows.
- AC4: Delivery estimates are shown per shipment, not as a single date.

**Story Points:** 8 | **Priority:** Must Have | **Sprint:** M4-S2  
**Dependencies:** STORY-0602, STORY-0606

---

### STORY-0611 — Order invoice download

As a buyer, I want to download my order invoice as a PDF, so that I have a record for expense claims or warranty purposes.

**Acceptance Criteria:**
- AC1: "Download Invoice" button is visible on the Order Detail page for delivered or confirmed orders.
- AC2: The invoice PDF is served from S3 via a pre-signed URL (valid for 1 hour).
- AC3: PDF is GST-compliant per STORY-0609.

**Story Points:** 2 | **Priority:** Must Have | **Sprint:** M3-S3  
**Dependencies:** STORY-0609

---

## EPIC-07: Returns & Refunds

**Goal:** Provide a self-service, transparent return and refund process that builds buyer trust.  
**Business Value:** Easy returns are the #1 driver of repeat purchase. 89% of buyers check return policy before buying.  
**Squad:** Orders  
**Target Months:** M5

---

### STORY-0701 — Return initiation by buyer

As a buyer, I want to initiate a return for a delivered item, so that I can get a refund for products I'm not satisfied with.

**Acceptance Criteria:**
- AC1: "Return Item" is available on the Order Detail page for items within the return window (default: 7 days from delivery; configurable per category).
- AC2: Buyer selects a return reason from taxonomy: Damaged, Wrong item, Not as described, Changed mind, Defective.
- AC3: For reasons other than "Changed mind," buyer can upload up to 3 photos.
- AC4: After submission, a return request ID is generated and buyer receives an email confirmation with pickup scheduling info.
- AC5: Return window is strictly enforced; the button disappears after expiry.

**Story Points:** 8 | **Priority:** Must Have | **Sprint:** M5-S1  
**Dependencies:** STORY-0602

---

### STORY-0702 — Reverse logistics pickup scheduling

As a buyer, I want the courier to come to my address to pick up the return item, so that I don't have to visit a drop-off point.

**Acceptance Criteria:**
- AC1: After return initiation, the platform creates a reverse pickup request via the 3PL API (Delhivery/Shiprocket).
- AC2: Buyer is shown the scheduled pickup date and time window (e.g., "Tomorrow, 10AM–1PM").
- AC3: Buyer receives an SMS with pickup agent name and contact number on the day of pickup.
- AC4: If pickup fails (buyer not available), it is rescheduled once automatically; second failure triggers admin review.

**Story Points:** 8 | **Priority:** Must Have | **Sprint:** M5-S1  
**Dependencies:** STORY-0701

---

### STORY-0703 — Automated refund processing

As a buyer whose return has been accepted, I want my refund automatically credited, so that I don't have to follow up.

**Acceptance Criteria:**
- AC1: Refund is initiated within 24 hours of QC pass at the warehouse.
- AC2: Refund goes to the original payment method: UPI (1–2 business days), card (5–7 business days), COD → bank transfer (3–5 business days).
- AC3: Buyer receives an email and push notification when refund is initiated with expected credit date.
- AC4: Refund status is tracked on the Order Detail page: Refund Initiated → Refund Processed.
- AC5: Refund failure (e.g., expired card) triggers an alert to support for manual resolution.

**Story Points:** 8 | **Priority:** Must Have | **Sprint:** M5-S2  
**Dependencies:** STORY-0702

---

### STORY-0704 — Return tracking

As a buyer, I want to track the return shipment, so that I know when the seller received my item.

**Acceptance Criteria:**
- AC1: The Order Detail page shows a Return Tracking section with status: Pickup Scheduled → Picked Up → In Transit → Delivered to Seller.
- AC2: Tracking events are sourced from the 3PL reverse logistics API.
- AC3: On "Delivered to Seller," QC review is marked as in progress.

**Story Points:** 5 | **Priority:** Must Have | **Sprint:** M5-S2  
**Dependencies:** STORY-0702

---

### STORY-0705 — Seller return management

As a seller, I want to view, accept, or dispute return requests, so that I can manage my return operations.

**Acceptance Criteria:**
- AC1: Returns portal shows all incoming return requests with reason, buyer photo evidence, and return item tracking status.
- AC2: I can mark a return as QC Passed or QC Failed with a reason after item is received.
- AC3: QC Passed → refund triggered automatically. QC Failed → case escalated to admin for arbitration.
- AC4: I can raise a dispute within 48 hours of QC result with supporting evidence.

**Story Points:** 8 | **Priority:** Must Have | **Sprint:** M5-S2  
**Dependencies:** STORY-0701, STORY-0905

---

### STORY-0706 — Buyer–seller dispute escalation

As a buyer or seller, I want to escalate an unresolved return dispute to the platform, so that a neutral party can make a decision.

**Acceptance Criteria:**
- AC1: Either party can escalate within 48 hours of the dispute being raised.
- AC2: Admin receives the dispute in an arbitration queue with both sides' evidence.
- AC3: Admin makes a decision within 3 business days; both parties are notified.
- AC4: Admin decision is final; refund or rejection is applied automatically.

**Story Points:** 8 | **Priority:** Should Have | **Sprint:** M5-S3  
**Dependencies:** STORY-0705

---

### STORY-0707 — Return window configuration (admin)

As a platform admin, I want to configure return windows by category, so that return policies match product types.

**Acceptance Criteria:**
- AC1: From the admin panel, I can set a return window (0–30 days) per category.
- AC2: Electronics: 7 days. Fashion: 30 days. Perishables: 0 days (no returns). These are the defaults.
- AC3: Category-level setting overrides the platform default for all products in that category.
- AC4: Change takes effect immediately for new orders; existing orders retain the policy at time of purchase.

**Story Points:** 3 | **Priority:** Must Have | **Sprint:** M5-S1  
**Dependencies:** STORY-0201, EPIC-10

---

### STORY-0708 — Instant refund to ShopNow Wallet

As a buyer, I want the option of instant refund to my ShopNow Wallet instead of waiting for bank credit, so that I can use the money immediately.

**Acceptance Criteria:**
- AC1: After QC pass, I am shown two refund options: "Refund to original payment method (5–7 days)" or "Instant refund to ShopNow Wallet."
- AC2: Selecting Wallet option credits the wallet immediately.
- AC3: Wallet balance is usable for future purchases.

**Story Points:** 5 | **Priority:** Nice to Have | **Sprint:** Phase 2  
**Dependencies:** STORY-0703, EPIC-15

---

## EPIC-08: Ratings & Reviews

**Goal:** Allow verified buyers to rate and review products; surface trustworthy social proof to prospective buyers.  
**Business Value:** Products with 10+ reviews convert 30% better. Fake review prevention protects marketplace trust.  
**Squad:** Commerce  
**Target Months:** M5

---

### STORY-0801 — Post-delivery review prompt

As the platform, I want to prompt buyers to review products they've received, so that review volume grows organically.

**Acceptance Criteria:**
- AC1: 3 days after an order is marked "Delivered," a push notification and email is sent: "How was your order? Rate it now."
- AC2: The prompt links directly to the review form pre-filled with the product name and image.
- AC3: Buyers who have already reviewed the item do not receive the prompt.
- AC4: Maximum one review prompt per order item.

**Story Points:** 3 | **Priority:** Must Have | **Sprint:** M5-S1  
**Dependencies:** STORY-0602

---

### STORY-0802 — Submit a product review

As a buyer who received an item, I want to submit a star rating and written review, so that other buyers can make better decisions.

**Acceptance Criteria:**
- AC1: Review form includes: 1–5 star rating (required), title (≤ 100 chars, optional), body (≤ 1,000 chars, optional), and up to 3 photos.
- AC2: Only buyers with a confirmed delivered order for that product can submit a review.
- AC3: Review is saved as `pending_moderation` and displayed after passing the moderation check (within 24 hours).
- AC4: Only one review per buyer per product variant is allowed; editing is permitted for 30 days post-submission.

**Story Points:** 5 | **Priority:** Must Have | **Sprint:** M5-S1  
**Dependencies:** STORY-0801

---

### STORY-0803 — Review display on PDP

As a prospective buyer, I want to see ratings and reviews on the product page, so that I can gauge product quality.

**Acceptance Criteria:**
- AC1: PDP shows: average rating (1 decimal), total review count, rating distribution bar chart (5★ → 1★).
- AC2: Top 3 reviews (highest helpful votes) shown by default; "Show all reviews" expands the full list.
- AC3: Verified Purchase badge shown on reviews from confirmed buyers.
- AC4: Review sorting options: Most Recent, Most Helpful, Highest Rated, Lowest Rated.
- AC5: Each review shows: reviewer first name + last initial, rating, date, title, body, and photos (if any).

**Story Points:** 5 | **Priority:** Must Have | **Sprint:** M5-S1  
**Dependencies:** STORY-0802, STORY-0205

---

### STORY-0804 — Review moderation

As a platform admin, I want a review moderation queue with NLP-assisted spam and abuse detection, so that low-quality content doesn't appear on the platform.

**Acceptance Criteria:**
- AC1: Reviews with flagged keywords, excessive caps, or competitor brand mentions are automatically held for manual review.
- AC2: Admin queue shows: review text, product, reviewer account age, reviewer's order history.
- AC3: Admin can: Approve, Reject (with reason), or Edit and Approve.
- AC4: Rejection emails are not sent (to prevent gaming the system).
- AC5: NLP model flags reviews with > 70% spam probability for priority review.

**Story Points:** 8 | **Priority:** Must Have | **Sprint:** M5-S2  
**Dependencies:** STORY-0802

---

### STORY-0805 — Seller response to reviews

As a seller, I want to respond to buyer reviews, so that I can address concerns publicly.

**Acceptance Criteria:**
- AC1: For each published review on my products, I can submit one response (≤ 500 chars).
- AC2: Seller responses are displayed below the buyer review with a "Seller Response" label.
- AC3: Responses are subject to the same moderation pipeline.

**Story Points:** 3 | **Priority:** Should Have | **Sprint:** M5-S3  
**Dependencies:** STORY-0803

---

### STORY-0806 — Helpful votes on reviews

As a buyer, I want to mark reviews as "helpful," so that the most useful reviews surface to the top.

**Acceptance Criteria:**
- AC1: A "Helpful" button is shown on each review; clicking it increments the helpful count.
- AC2: Each buyer can vote once per review; clicking again removes the vote.
- AC3: Review sort "Most Helpful" orders by helpful count descending.

**Story Points:** 3 | **Priority:** Should Have | **Sprint:** M5-S3  
**Dependencies:** STORY-0803

---

### STORY-0807 — Rating aggregation update job

As the platform, I need product ratings to update in near real-time after new reviews, so that displayed ratings are always current.

**Acceptance Criteria:**
- AC1: When a review is approved, a Kafka event is published.
- AC2: A Kafka consumer recalculates the product's average rating and review count and updates the `products` table and OpenSearch document within 60 seconds.
- AC3: Rating aggregation is an upsert — no race conditions on concurrent reviews.

**Story Points:** 3 | **Priority:** Must Have | **Sprint:** M5-S2  
**Dependencies:** STORY-0802, STORY-0304

---

## EPIC-09: Seller Portal

**Goal:** Provide a comprehensive self-serve portal for sellers to onboard, manage listings, fulfil orders, and get paid.  
**Business Value:** Seller NPS and ease of onboarding are the primary levers for growing supply (more sellers = more products = better buyer experience).  
**Squad:** Seller  
**Target Months:** M1–M5

---

### STORY-0901 — Seller registration

As a new seller, I want to register for a seller account, so that I can start listing products.

**Acceptance Criteria:**
- AC1: Registration form collects: business name, business type (individual/company), email, mobile.
- AC2: Mobile OTP verification is required before proceeding to KYC.
- AC3: After verification, seller is in `pending_kyc` status and redirected to the KYC wizard.

**Story Points:** 5 | **Priority:** Must Have | **Sprint:** M1-S1  
**Dependencies:** None

---

### STORY-0902 — Seller KYC (GST + PAN + bank account)

As a new seller, I want to submit my KYC documents, so that my account can be verified and activated.

**Acceptance Criteria:**
- AC1: KYC wizard collects: GSTIN (validated against GST API), PAN number, bank account number + IFSC (validated via penny drop), and scanned documents upload.
- AC2: GSTIN validation returns the registered business name for the seller to confirm.
- AC3: Documents are stored encrypted in S3; access is limited to admin KYC reviewers.
- AC4: Seller receives an email when their KYC is approved or rejected (with reason).
- AC5: Approval time SLA: < 2 business hours for auto-verification; < 24 hours for manual review.

**Story Points:** 13 | **Priority:** Must Have | **Sprint:** M1-S2  
**Dependencies:** STORY-0901

---

### STORY-0903 — Seller dashboard home

As a seller, I want a dashboard home page showing key metrics, so that I can get a quick performance snapshot.

**Acceptance Criteria:**
- AC1: Shows today's and last 7 days': total revenue, number of orders, units sold, and pending orders count.
- AC2: Displays quick-action cards: "Add Product," "Pending Orders," "Low Stock Alerts."
- AC3: A health scorecard shows: seller rating, order defect rate, and late dispatch rate.

**Story Points:** 5 | **Priority:** Must Have | **Sprint:** M2-S1  
**Dependencies:** STORY-0902

---

### STORY-0904 — Product listing management (seller)

Covered by STORY-0202, STORY-0203, STORY-0207, STORY-0208.

---

### STORY-0905 — Seller order management

Covered by STORY-0606, STORY-0607, STORY-0608.

---

### STORY-0906 — Payout dashboard

As a seller, I want to see my earnings, upcoming payouts, and deduction details, so that I understand my income.

**Acceptance Criteria:**
- AC1: Dashboard shows: total lifetime earnings, earnings this month, next payout date, and next payout amount.
- AC2: A transaction table lists each settled order: order ID, item, GMV, commission deducted, payment gateway fee, net amount.
- AC3: I can download a CSV of transactions for any date range.
- AC4: Payouts run weekly (T+7 from delivery confirmation) and are shown as "Pending" until funds are transferred.

**Story Points:** 8 | **Priority:** Must Have | **Sprint:** M5-S1  
**Dependencies:** STORY-0902, STORY-0606

---

### STORY-0907 — Seller bank account management

As a seller, I want to update or add a bank account for payouts, so that my earnings go to the right account.

**Acceptance Criteria:**
- AC1: I can add a new bank account by entering account number + IFSC; a ₹1 penny drop verifies the account.
- AC2: I can mark an account as default.
- AC3: Changing the default payout account requires OTP verification.
- AC4: Any payout initiated before the change goes to the previously active account.

**Story Points:** 5 | **Priority:** Must Have | **Sprint:** M5-S1  
**Dependencies:** STORY-0902

---

### STORY-0908 — Seller basic analytics

As a seller, I want to see product-level performance metrics, so that I know which listings to prioritise.

**Acceptance Criteria:**
- AC1: Analytics page shows for each product: page views, add-to-cart rate, conversion rate, revenue, and units sold (last 7/30/90 days).
- AC2: Bar chart of daily revenue trend.
- AC3: Data is refreshed every 24 hours (T+1 day lag is acceptable).

**Story Points:** 8 | **Priority:** Should Have | **Sprint:** M5-S2  
**Dependencies:** STORY-0903

---

### STORY-0909 — Seller notification preferences

As a seller, I want to configure which notifications I receive, so that I only get alerts relevant to me.

**Acceptance Criteria:**
- AC1: Notification categories: New Order, Low Stock, Return Request, Payout, KYC Status, Policy Updates.
- AC2: For each category I can enable/disable: Email, SMS, In-app.
- AC3: Transactional notifications (New Order, Return Request) cannot be fully disabled.

**Story Points:** 3 | **Priority:** Should Have | **Sprint:** M5-S3  
**Dependencies:** STORY-0902

---

## EPIC-10: Admin Panel & Platform Management

**Goal:** Give platform administrators the tools to manage users, sellers, content, commissions, and platform health.  
**Business Value:** Without admin tooling, operations teams are blind; platform abuse and quality issues go unaddressed.  
**Squad:** Platform  
**Target Months:** M1–M5

---

### STORY-1001 — Admin user management

As a super admin, I want to manage platform user accounts, so that I can handle account issues and enforce policies.

**Acceptance Criteria:**
- AC1: Search users by email, mobile, or user ID.
- AC2: View user profile, order history, and account status.
- AC3: Actions available: Suspend (temporary), Ban (permanent), Reset Password, Verify Email.
- AC4: All admin actions are logged with admin user ID, action, timestamp, and reason.

**Story Points:** 8 | **Priority:** Must Have | **Sprint:** M1-S3  
**Dependencies:** STORY-0109

---

### STORY-1002 — Admin KYC review queue

As an admin, I want to review and approve/reject seller KYC submissions, so that only verified sellers can list products.

**Acceptance Criteria:**
- AC1: Queue shows all `pending_kyc` sellers sorted by submission time.
- AC2: I can view uploaded documents (GSTIN, PAN, bank proof) with zoom.
- AC3: Approve button activates the seller; Reject shows a mandatory reason field.
- AC4: Approval/rejection triggers a notification to the seller (email + in-app).
- AC5: SLA indicator shows green/amber/red based on time since submission.

**Story Points:** 8 | **Priority:** Must Have | **Sprint:** M1-S3  
**Dependencies:** STORY-0902

---

### STORY-1003 — Commission rate configuration

As a super admin, I want to configure platform commission rates by category, so that pricing is accurate across product types.

**Acceptance Criteria:**
- AC1: Set a commission percentage (0–30%) per leaf or parent category.
- AC2: Child categories inherit parent commission unless overridden.
- AC3: Rate changes apply to new orders only; existing orders use the rate at time of placement.
- AC4: Changes are logged with a before/after value and timestamp.

**Story Points:** 5 | **Priority:** Must Have | **Sprint:** M1-S2  
**Dependencies:** STORY-0201

---

### STORY-1004 — Homepage banner management

As a marketing admin, I want to manage homepage banners and hero images, so that I can promote campaigns without a deployment.

**Acceptance Criteria:**
- AC1: Upload banner image, set destination URL, set start/end date, and set display order.
- AC2: Multiple banners cycle as a carousel.
- AC3: Preview mode shows how the banner looks on desktop and mobile before going live.
- AC4: Banner cache is invalidated upon save.

**Story Points:** 5 | **Priority:** Must Have | **Sprint:** M2-S1  
**Dependencies:** None

---

### STORY-1005 — Product content moderation

As an admin, I want a queue of flagged product listings for review, so that policy-violating content is removed promptly.

**Acceptance Criteria:**
- AC1: Products can be flagged by: buyer reports, automated text scan (profanity, prohibited items list), admin manual flag.
- AC2: Flagged products queue shows: product title, seller, flag reason, and flag count.
- AC3: Admin can: Approve (clear flag), Remove Listing, Suspend Seller, or Escalate.

**Story Points:** 8 | **Priority:** Should Have | **Sprint:** M3-S2  
**Dependencies:** STORY-0202, STORY-1001

---

### STORY-1006 — Financial payout management

As a finance admin, I want to view, approve, and process seller payouts, so that sellers are paid on time.

**Acceptance Criteria:**
- AC1: Payout dashboard shows all payouts in states: Pending Calculation, Pending Approval, Approved, Initiated, Settled.
- AC2: Bulk approval for all payouts in a period with a single confirmation.
- AC3: Payouts are triggered via NEFT/IMPS batch transfer API call to the banking partner.
- AC4: Any payout failure triggers an alert and moves the payout back to Pending with a failure reason.

**Story Points:** 8 | **Priority:** Must Have | **Sprint:** M5-S2  
**Dependencies:** STORY-0906

---

### STORY-1007 — Platform analytics dashboard

As a business admin, I want to see key platform metrics in a dashboard, so that I can monitor platform health.

**Acceptance Criteria:**
- AC1: Dashboard shows (live or T+1): GMV (today, MTD, YTD), order count, active users, new registrations, conversion rate, return rate.
- AC2: Trend charts for GMV and orders over last 30 days.
- AC3: Top 10 sellers by GMV and top 10 products by units sold.
- AC4: Data sourced from ClickHouse; dashboard refreshes every 15 minutes.

**Story Points:** 8 | **Priority:** Should Have | **Sprint:** M5-S2  
**Dependencies:** STORY-0307

---

### STORY-1008 — Seller performance scorecard

As a platform admin, I want to see a performance scorecard per seller, so that I can identify and address underperforming sellers.

**Acceptance Criteria:**
- AC1: Scorecard shows: order defect rate (cancellations + returns / total orders), late dispatch rate, seller rating average, and total complaints.
- AC2: Sellers below threshold (defect rate > 5%) are flagged with a warning badge.
- AC3: Admin can send an automated warning email with improvement guidelines.

**Story Points:** 5 | **Priority:** Should Have | **Sprint:** M5-S3  
**Dependencies:** STORY-1007

---

### STORY-1009 — Feature flag management

As a platform admin, I want a UI to toggle feature flags, so that I can enable/disable features without a deployment.

**Acceptance Criteria:**
- AC1: UI lists all registered feature flags with their current state (on/off) per environment.
- AC2: Flags can be toggled for: all users, specific user IDs, or a percentage rollout.
- AC3: Toggle changes are reflected in Unleash within 5 seconds.
- AC4: All flag changes are logged.

**Story Points:** 5 | **Priority:** Must Have | **Sprint:** M2-S1  
**Dependencies:** None

---

### STORY-1010 — Fraud monitoring dashboard

As a trust and safety admin, I want to see flagged transactions and accounts, so that I can act on fraud in near real-time.

**Acceptance Criteria:**
- AC1: Dashboard shows: fraud score histogram, today's flagged transactions (score > 85), and accounts with multiple failed payment attempts.
- AC2: Admin can manually review an account, override the fraud flag, or block the account.
- AC3: Fraud rule configuration (e.g., "block if > 5 failed payments in 30 min") editable from UI without code change.

**Story Points:** 8 | **Priority:** Should Have | **Sprint:** M5-S3  
**Dependencies:** STORY-1001

---

## Phase 2 — Full Platform Epics (Month 7–12)

---

## EPIC-11: Personalisation & Recommendations

**Goal:** Deliver personalised product recommendations powered by ML to increase CTR, basket size, and session depth.  
**Squad:** ML  
**Target Months:** M7–M8

| Story ID | Title | Points | Priority |
|----------|-------|--------|---------|
| STORY-1101 | Personalised homepage feed | 13 | Must Have |
| STORY-1102 | "Similar products" widget on PDP | 8 | Must Have |
| STORY-1103 | "Frequently bought together" widget | 8 | Should Have |
| STORY-1104 | "Recently viewed" carousel | 5 | Must Have |
| STORY-1105 | Personalised email recommendations | 8 | Should Have |
| STORY-1106 | User event tracking pipeline | 13 | Must Have |
| STORY-1107 | Recommendation model training pipeline | 21 | Must Have |
| STORY-1108 | A/B test framework for recommendations | 13 | Should Have |

---

## EPIC-12: Mobile Apps (iOS & Android)

**Goal:** Launch native-quality mobile apps on iOS and Android using React Native / Expo.  
**Squad:** Mobile  
**Target Months:** M8–M9

| Story ID | Title | Points | Priority |
|----------|-------|--------|---------|
| STORY-1201 | iOS App Store and Google Play setup | 5 | Must Have |
| STORY-1202 | Home, Search, PLP, PDP screens | 13 | Must Have |
| STORY-1203 | Cart and checkout screens | 13 | Must Have |
| STORY-1204 | Order tracking and history screens | 8 | Must Have |
| STORY-1205 | Push notification integration (FCM + APNs) | 8 | Must Have |
| STORY-1206 | Biometric login (FaceID / Fingerprint) | 5 | Should Have |
| STORY-1207 | Offline mode: cart persistence | 5 | Should Have |
| STORY-1208 | Deep linking scheme (shopnow://) | 5 | Must Have |
| STORY-1209 | App performance profiling (< 2s TTI) | 8 | Must Have |
| STORY-1210 | OTA updates via Expo EAS | 5 | Should Have |

---

## EPIC-13: Seller Analytics & Growth Tools

**Goal:** Give sellers data-driven insights and promotional tools to grow their business on the platform.  
**Squad:** Seller  
**Target Months:** M9–M10

| Story ID | Title | Points | Priority |
|----------|-------|--------|---------|
| STORY-1301 | Full seller analytics dashboard (v2) | 13 | Must Have |
| STORY-1302 | Product-level conversion funnel | 8 | Must Have |
| STORY-1303 | Inventory forecasting & replenishment alerts | 8 | Should Have |
| STORY-1304 | Seller coupon creation and management | 8 | Must Have |
| STORY-1305 | Bundle offer creation (buy 2 get 10% off) | 8 | Should Have |
| STORY-1306 | Competitor price benchmarking alerts | 8 | Nice to Have |
| STORY-1307 | Catalogue health score (listing quality) | 8 | Should Have |
| STORY-1308 | Seller growth tips feed | 5 | Nice to Have |
| STORY-1309 | Seller benchmarking vs category average | 8 | Should Have |

---

## EPIC-14: Sponsored Ads Platform

**Goal:** Enable sellers and brands to run CPC-based sponsored product and brand ads to boost product visibility.  
**Squad:** Ads  
**Target Months:** M10–M11

| Story ID | Title | Points | Priority |
|----------|-------|--------|---------|
| STORY-1401 | Sponsored Products: campaign creation | 13 | Must Have |
| STORY-1402 | CPC keyword bidding engine | 21 | Must Have |
| STORY-1403 | Ad auction and ranking integration with search | 13 | Must Have |
| STORY-1404 | Advertiser budget and pacing controls | 8 | Must Have |
| STORY-1405 | Ad performance dashboard (impressions, clicks, ROAS) | 13 | Must Have |
| STORY-1406 | Sponsored Brands: banner ads for brand store | 13 | Should Have |
| STORY-1407 | Ad billing and invoicing | 8 | Must Have |
| STORY-1408 | Ad fraud detection (click fraud) | 8 | Must Have |

---

## EPIC-15: Loyalty Program & Wallet

**Goal:** Reward frequent buyers with cashback coins and provide a platform wallet for fast, seamless payments.  
**Squad:** Commerce  
**Target Months:** M10–M11

| Story ID | Title | Points | Priority |
|----------|-------|--------|---------|
| STORY-1501 | ShopNow Coins: earn on every purchase | 8 | Must Have |
| STORY-1502 | ShopNow Coins: redeem on checkout | 8 | Must Have |
| STORY-1503 | Tier system (Silver / Gold / Platinum) | 8 | Should Have |
| STORY-1504 | ShopNow Wallet: top-up via UPI/card | 8 | Must Have |
| STORY-1505 | ShopNow Wallet: pay at checkout | 5 | Must Have |
| STORY-1506 | Coins expiry and reminder notifications | 5 | Should Have |
| STORY-1507 | Referral program: invite and earn | 8 | Should Have |
| STORY-1508 | Loyalty analytics for admin | 5 | Should Have |

---

## EPIC-16: Vernacular / Multi-language Support

**Goal:** Deliver the platform UI in Hindi and 4 regional languages, unlocking the tier-2/3 buyer market.  
**Squad:** Platform  
**Target Months:** M11–M12

| Story ID | Title | Points | Priority |
|----------|-------|--------|---------|
| STORY-1601 | i18n framework integration (next-intl) | 5 | Must Have |
| STORY-1602 | Hindi UI translation | 8 | Must Have |
| STORY-1603 | Tamil UI translation | 8 | Should Have |
| STORY-1604 | Telugu UI translation | 8 | Should Have |
| STORY-1605 | Language selector in nav + auto-detect from browser | 3 | Must Have |
| STORY-1606 | Product titles and descriptions in Hindi for top categories | 8 | Should Have |

---

## Story Point Reference

| Feature Area | Phase 1 Points | Phase 2 Points | Total |
|-------------|---------------|---------------|-------|
| Auth & Identity | 63 | — | 63 |
| Catalogue | 89 | — | 89 |
| Search | 55 | — | 55 |
| Cart & Wishlist | 42 | — | 42 |
| Checkout & Payments | 96 | — | 96 |
| Orders & Fulfilment | 81 | — | 81 |
| Returns & Refunds | 58 | — | 58 |
| Reviews | 40 | — | 40 |
| Seller Portal | 104 | 72 | 176 |
| Admin Panel | 68 | — | 68 |
| Personalisation | — | 89 | 89 |
| Mobile Apps | — | 104 | 104 |
| Ads Platform | — | 96 | 96 |
| Loyalty & Wallet | — | 68 | 68 |
| Vernacular | — | 42 | 42 |
| **TOTAL** | **696** | **471** | **1,167** |

At an average team velocity of 80 points/sprint (2-week sprint, 5 squads × ~16 pts):
- Phase 1 (696 pts): ~9 sprints = ~18 weeks (aligned with 6-month M1–M6 target)
- Phase 2 (471 pts): ~6 sprints = ~12 weeks (aligned with M7–M12 target)

---

## Global Definition of Done

All stories must meet the following before being marked **Done**:

### Code Quality
- [ ] Code reviewed and approved by at least 1 peer
- [ ] TypeScript strict mode — zero `any` types introduced
- [ ] Unit tests written covering all business logic branches (≥ 80% coverage on changed files)
- [ ] Integration tests pass against a real test database (no mocks for DB calls)
- [ ] ESLint and Prettier pass with zero warnings

### Security
- [ ] No raw PII logged
- [ ] Input validation at API boundary (Zod schema or equivalent)
- [ ] Auth middleware applied to all protected endpoints
- [ ] Secrets not hardcoded — sourced from Vault/Secrets Manager
- [ ] Snyk scan passes — no HIGH or CRITICAL CVEs in new dependencies

### Observability
- [ ] Structured JSON logs for all significant events (request received, response sent, errors)
- [ ] OpenTelemetry span created for the main operation
- [ ] Prometheus metric incremented for success/failure counters
- [ ] Health check endpoint updated if new dependency added

### Documentation
- [ ] API endpoint documented in OpenAPI spec (`API_SPEC.md`)
- [ ] Any schema change accompanied by a migration script
- [ ] Feature flag created in Unleash if the story is behind a flag

### Testing & Deployment
- [ ] CI pipeline passes (lint → type-check → test → build → scan)
- [ ] Deployed to staging and smoke tested
- [ ] PM sign-off: acceptance criteria verified in staging
- [ ] Feature flag defaulted to OFF in production; enabled via flag for rollout

---

## Dependency Graph

```
EPIC-10 (Admin)
  └── STORY-1001, STORY-1002, STORY-1003, STORY-1009
        │
EPIC-01 (Auth)     EPIC-09 (Seller)
  │                   │
  └──────┬────────────┘
         │
    EPIC-02 (Catalogue)
         │
    ┌────┴────┬──────────┐
 EPIC-03   EPIC-04    EPIC-08
(Search)  (Cart)    (Reviews)
              │
         EPIC-05 (Checkout)
              │
         EPIC-06 (Orders)
              │
         EPIC-07 (Returns)
              │
    ┌─────────┴──────────────┐
EPIC-11 (Personalisation)  EPIC-13 (Analytics)
EPIC-12 (Mobile)           EPIC-14 (Ads)
EPIC-15 (Loyalty)          EPIC-16 (Vernacular)
```

**Critical path to MVP launch:**  
EPIC-10 → EPIC-01 → EPIC-02 → EPIC-03 + EPIC-04 → EPIC-05 → EPIC-06 → EPIC-07 + EPIC-08 → EPIC-09

---

*This document is a living backlog. Story estimates are initial sizing and will be re-pointed during sprint planning. Priorities may change based on stakeholder input and technical discoveries.*
