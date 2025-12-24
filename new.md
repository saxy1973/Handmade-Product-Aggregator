# Handmade Products Aggregator System

**MVP Scope Summary**
 
Handmade Product Aggregator System MVP enables artisans to create storefronts, list products, accept secure payments, manage orders, and update parcel tracking, while allowing buyers to discover handmade products via fast search and personalized recommendations.
## 1. Product Overview and Description
Handmade Product Aggregator System is a global curated marketplace for individual artisans and small handmade brands who do not have their own ecommerce platform. It provides them with storefronts, fast product discovery, secure payments, transparent commissions, and easy order and parcel tracking. Buyers get trusted, personalized access to unique handmade items worldwide with quick search, relevant recommendations, and clear delivery visibility.

## 2. Problem Statement
Individual artisans and small handmade brands worldwide struggle to sell online because they lack ecommerce platforms, technical skills, and marketing reach. They rely on social media DMs, messaging apps, and local fairs, which create low trust for buyers, no standardized pricing, limited discoverability, and poor order tracking. Buyers who want authentic handmade items face scattered options, inconsistent information, and fear of fraud.

Target users are small sellers who do not have their own platform, including individual artisans and small handmade brands worldwide, across all handmade item categories. The marketplace must justify pricing for both buyers and sellers, offer more traffic to sellers, and build a highly trustable platform with an average sales commission, integrated payments, a seller dashboard, order management, fast parcel tracking, and optimized performance (fast search, recommendations, and authentication).

## 3. Goals
### -Business Goals
* Acquire at least 200 active sellers and 2,000 active buyers within 6 months of launch.
* Reach monthly GMV of $15,000 within 6 months with an average commission of 10–15%.
* Achieve a repeat purchase rate of 30% of buyers within 3 months of their first order.
Maintain a dispute rate below 3% of total orders.
### -User Goals
* Enable artisans and small handmade brands to launch a storefront in under 30 minutes.
Help sellers increase traffic and sales beyond offline and social channels.
* Provide buyers with fast, accurate search and personalized recommendations so they can quickly find relevant handmade items.
* Build buyer trust via verified sellers, transparent pricing, secure checkout, and easy near real-time parcel tracking with minimal delay.
### -Non-Goals
* No in-house logistics/warehousing in v1; shipping is handled by sellers or external couriers.
* No advanced marketing/ad campaign tools for sellers in v1.
* No B2B wholesale or bulk-order flows in v1.

## 4. User Stories
### -Buyer

* As a buyer, I want to browse and search handmade products quickly by category, price, location, and style so that I can find what I like without waiting.
As a buyer, I want personalized recommendations based on my preferences and history so that I see items that match my taste.
* As a buyer, I want transparent pricing (item, shipping, fees) so that I understand what I am paying for.
* As a buyer, I want to track my parcel in near-real time with minimal delay so that I always know where my order is and when it will arrive.
* As a buyer, I want a fast login or guest checkout so that authentication does not slow me down.
### -Seller (Artisan / Small Brand)

* As a seller, I want to register and create my storefront easily so that I can start selling without my own website.
* As a seller, I want to add and manage products (photos, descriptions, prices, stock) so that my catalog is always up to date.
* As a seller, I want clear information about commission and payouts so that I can set fair prices.
* As a seller, I want a dashboard that shows my orders, revenue, commissions, and payouts so that I can manage my business.
* As a seller, I want to update order status and tracking information so that buyers see accurate parcel status.
### -Platform Admin

* As an admin, I want to review and approve sellers and products so that marketplace quality stays high.
* As an admin, I want to view GMV, commission revenue, and top-performing sellers/products so that I can optimize growth.
* As an admin, I want basic tools to manage disputes, refunds, and fraudulent activity so that platform trust is maintained.
## Functional Requirements
### -Seller Onboarding & Storefront (Priority: High)
* Seller registration via email/phone and basic KYC/verification.
* Seller profile including brand story, location, profile image, and social links.
* Auto-generated storefront URL/page listing the seller’s products, ratings, and reviews.
### -Product Catalog Management (Priority: High)
* Create/read/update/delete products with title, description, price, quantity, photos, category, tags, and optional variants (e.g., size, color).
* Product states: draft, active, out-of-stock.
* Bulk upload (simple CSV or UI batch) in a later iteration.
### -Discovery, Search & Recommendations (Priority: High)
* Fast search with filters: category, price range, rating, location, tags.
* Search must use indexed fields or a search engine; target P95 latency <200–300ms for first page results.
* Curated collections (e.g., “New Arrivals”, “Best Sellers”, “Gifts under $50”, “Trending Near You”).
* Personalized “For You” section that ranks products based on user behaviour (views, clicks, carts, purchases), category preferences, and price sensitivity.
* Basic recommendation logic in v1: combine global popularity signals with per-user preferences; designed so ranking runs on a limited candidate set per user (sub-linear with total catalog size).
### -Pricing, Commission & Payments (Priority: High)
* Global setting for default commission percentage (e.g., 10–15%) with potential overrides per seller later.
* Per-order calculation of commission and seller payout at checkout.
* Seller-facing breakdown of item price, commission, and expected payout on product and order views.
* Buyer-facing display of full price (item + shipping + any applicable fees) before payment.
* Integration with payment gateway(s) for secure card and local payment methods; no raw card storage.
### -Checkout, Orders & Parcel Tracking (Priority: High)
* Cart and single-item checkout flows.
* Order creation upon successful payment, with immutable order ID.
* Order states: placed, confirmed, shipped, out for delivery (if supported), delivered, cancelled, refunded.
* Sellers can update shipment and tracking info (courier, tracking ID, status).
* Optional integration with courier APIs where available; tracking information refreshed asynchronously and cached.
* Buyer order history page showing per-order timeline and current parcel status with minimal lag.
* Target tracking view performance: P95 <300ms, with tracking calls to external APIs cached to avoid blocking UI.
### -Authentication & Authorization (Priority: High)
* Support for email/OTP login and at least one social login provider (e.g., Google).
* Guest checkout for buyers with email + phone, with option to create an account post-purchase.
* Short login/signup flow (≤ 2 UI steps for social/OTP) to minimize friction.
* Token-based auth (e.g., JWT) so most requests verify tokens locally with O(1) cost and minimal DB lookups.
### -Trust, Ratings & Reviews (Priority: Medium)
* Verified seller badge after passing basic KYC.
* Buyers can rate products and sellers and leave short text reviews after delivery.
* Product and seller average ratings kept as precomputed fields to avoid scanning all reviews on each read.
* Basic reporting for inappropriate content.
### -Admin & Moderation (Priority: Medium)
* Admin portal to manage users, sellers, products, and orders.
* Ability to approve/reject sellers and products.
* Configuration of global commission rate and some marketplace-wide parameters.
* Dispute and refund handling workflows (mainly manual in v1).
## User Experience
### -Entry Point & First-Time User Experience
Buyers land on the web app through SEO, social media, or referrals. The homepage highlights curated collections, featured artisans, and trust signals (“Verified artisans”, ratings, secure payments). Buyers can browse and search without logging in. When they choose to purchase, they see a minimal-friction flow: either quick OTP/social login or guest checkout with basic details.

Sellers discover a prominent “Become a Seller” call-to-action. Clicking it leads to a guided onboarding wizard: account creation (with OTP/social), business details and KYC, and first product listing. Progress steps are clearly indicated and can be saved/resumed.

### -Core Experience – Buyer
The buyer explores curated collections or directly searches using keywords and filters. Search results load quickly, returning a relevant first page in under a second, even as the catalog grows. A “For You” section highlights products aligned with the buyer’s past behaviour and preferences.

On the product page, the buyer sees multiple images, detailed descriptions, seller story, rating, and transparent pricing. When adding to cart and checking out, the system validates fields inline and displays a clear order summary. After successful payment, the buyer is redirected to an order confirmation page and can immediately see their order in “My Orders” with initial status and, once available, tracking details from the seller or courier.

### -Core Experience – Seller
The seller signs in and lands on a dashboard showing an overview of orders, revenue, commissions paid, and upcoming payouts. From the dashboard, the seller can manage products, update stock, and see performance metrics.

When a new order arrives, the seller receives a notification, confirms the order, prepares shipment, and enters or updates tracking information. Status changes automatically reflect for the buyer. The seller can view payout summaries and understand earnings per order with a clear commission breakdown.

### -Advanced Features & Edge Cases
* Payment failures show clear error messages and allow retry without losing cart state.
* Out-of-stock products are not purchasable and are visually indicated.
* Inactive sellers may be soft-hidden after a threshold of inactivity.
* For tracking, if courier APIs fail, the UI shows the latest known status and a user-friendly fallback message.
### -UI/UX Highlights
* Mobile-first, image-forward design emphasizing products and artisan stories.* 
* Strong trust signals near critical actions: badges, secure-payment indicators, and review summaries.
* Clear progress indicators in checkout and onboarding flows.
* Consistent and fast perceived performance: skeleton loaders and optimistic UI where safe.
## Narrative
Riya, an artisan who handcrafts jewelry, has been selling primarily via Instagram DMs. She spends hours answering the same questions about price, shipping, and delivery, and many buyers drop off because they are uncomfortable sending money directly or cannot track their parcels.

She signs up for the Handmade Product Aggregator System. In a single evening, she verifies her identity, sets up her storefront, and adds her first 20 products. The interface helps her price items correctly by clearly showing the average commission and expected payout. From then on, she manages everything from one dashboard: new orders, shipments, tracking IDs, and payouts.

Meanwhile, Alex, a buyer who loves unique handmade items, visits the Handmade Product Aggregator System. He types “silver handmade bracelet” and instantly sees a relevant list of products, filtered by his preferred price range and style. A personalized “For You” section surfaces Riya’s jewelry because similar products have performed well with buyers like him. After a quick OTP login and a simple checkout, Alex places an order.

Throughout the delivery journey, Alex checks the “My Orders” page to track his parcel in near real-time, synced from the courier. When the bracelet arrives, he leaves a positive review, which boosts Riya’s visibility and trust score. The platform earns a fair commission and reinvests in better discovery, tools, and security. Over time, the platform becomes the default destination for buyers like Alex and a core revenue channel for artisans like Riya.

## Success Metrics
### -User-Centric Metrics
* Active buyers (last 30 days).
* Active sellers (at least one product and one login in last 30 days).
* Repeat purchase rate.
* Average search latency (P95) and recommendation click-through rate.
* Buyer satisfaction (e.g., NPS, app rating, or survey score).
### -Business Metrics
* Monthly GMV and commission revenue.
* Average order value.
* Seller retention after 3 and 6 months.
* Conversion rate from visit to purchase.
### -Technical Metrics
* Search and recommendation response time (P95, target <300ms for core flows).
* Checkout success rate (successful payments / initiated).
* Uptime (target ≥ 99.5%).
* Error rates on auth, checkout, and tracking API calls.
### -Tracking Plan
Track key events such as: seller_signup_completed, seller_verified, product_created, product_published, product_viewed, search_performed, recommendation_clicked, product_added_to_cart, checkout_started, payment_succeeded, payment_failed, order_status_changed, tracking_viewed, review_submitted.

## Technical Considerations
### -Technical Needs
* Web application composed of: buyer-facing marketplace, seller dashboard, and admin console.
* Backend services for auth, users, sellers, products, search, orders, payments, tracking, and recommendations.
* Relational database (or equivalent) with indices on key fields (seller_id, buyer_id, category, tags, status).
* Search engine or search index for fast full-text search and filtering.
* Background workers for async tasks (e.g., updating recommendations, refreshing courier tracking, sending notifications).
### -Integration Points
* Payment gateway(s) for payments and payouts.
* Optional courier APIs for parcel tracking.
* Email/SMS provider for OTPs and transactional notifications.
### -Data Storage & Privacy
* User and seller data stored securely with encryption for sensitive fields.
* No storage of raw card data; rely on gateway tokens.
* Clear policies for data retention, deletion on request, and consent for communications.
### -Scalability & Performance
* Search, recommendation, and tracking endpoints designed for sub-linear growth in cost as catalog and user base grow, using indexes, caching, and precomputed aggregates.
* Use caching (e.g., Redis) for frequently accessed data such as popular products, user preference summaries, and recent tracking statuses.
* Design order and tracking lookups as O(1) key-based queries with appropriate indexing.
* Ensure auth is token-based so most protected requests avoid DB lookups for session state.
### -Potential Challenges
* Preventing fraud (fake sellers, fake reviews, payment abuse).
* Handling internationalization: currencies, shipping assumptions, and regulations as the platform scales.
* Keeping recommendation quality high without overcomplicating early implementation.
* Ensuring courier integrations degrade gracefully when APIs are slow or unavailable.
## Milestones & Sequencing
### -Project Estimate
Scope: Small-to-medium MVP. Target 4–6 weeks for initial release with a fast-moving team.

### -Team Size & Composition
Small team (2–3 people):

* 1 Product-oriented developer (can handle PRD, UX, and basic design).
* 1 Full-stack engineer (or 2 engineers if you want to go faster and split front/back).
### -Suggested Phases
**Phase 1** – Core Marketplace MVP (3 weeks)

* Buyer: browsing, fast search, filters, basic “For You” logic, checkout, and simple order status (placed, confirmed, shipped, delivered).
* Seller: onboarding, storefront, product management, basic dashboard, manual tracking input.
* Platform: payments integration, commission logic, minimal admin console.

**Phase 2** – Trust, Tracking & Personalization (2 weeks)

* Improve parcel tracking UX and introduce courier API integration with caching.
* Enhance recommendations using more behavioural signals.
* Add ratings, reviews, and verified seller badges.
* Improve performance tuning on search and auth latency.

**Phase 3** – Optimization & Scaling (ongoing)

* Iterate on analytics, fraud controls, and UX refinements.
* Add small improvements to seller tools (reporting, payouts) and buyer discovery.

## Appendix: Technology Stack & Architecture (Coding Perspective)

Application will follow a modular, service-oriented architecture with a single deployable backend (for MVP) and clear domain boundaries: Auth, Users/Sellers, Products & Search, Orders & Payments, Tracking, Recommendations, and Admin.

### Backend

* Language/Framework: Node.js with TypeScript using a structured web framework (e.g., NestJS or Express + modules) for strong typing, predictable APIs, and easier scaling.
* API Style: RESTful JSON APIs; versioned (/api/v1/...) with clear separation between buyer, seller, and admin endpoints.
* Authentication: JWT-based auth with refresh tokens; short-lived access tokens validated locally by all services.
* Background Processing: Job queue (e.g., BullMQ on Redis) for async tasks such as updating recommendations, refreshing courier tracking, sending emails/SMS, and recomputing aggregates.

### Frontend

* Web Technology: React (or Next.js for SSR/ISR) for fast page loads and good SEO for product and storefront pages.
* State Management: Lightweight client-side state (React Query / SWR) for caching API responses and keeping UI responsive.
* Styling/UI: Component library or design system (e.g., Tailwind CSS + custom components) tuned for mobile-first, image-forward cards and grids.

### Data & Storage

* Primary Database: Relational database such as PostgreSQL for strong consistency and relational modelling (users, sellers, products, orders, payouts, reviews).
* Indexing: Database indexes on seller_id, buyer_id, category, tags, status, created_at to keep reads O(1)/O(log n) for critical queries (orders, tracking, dashboards).
* Search: Dedicated search index (e.g., Elasticsearch, OpenSearch, or Meilisearch) for full-text search, filters, and relevance scoring; product data is synced from the primary DB.
* Caching: In-memory cache (e.g., Redis) for:
  + Popular products and curated collections
  + User preference summaries (for “For You” recommendations)
  + Recent tracking statuses and courier responses

### Recommendations

* Data Inputs: Product views, clicks, add-to-cart, purchases, category preferences, and price bands.
* Implementation:
  + Batch jobs (e.g., scheduled workers) compute global popularity scores and lightweight per-user preference vectors.
  + Online API uses a pre-filtered candidate set per user (by category/price) and ranks them by a mix of global popularity + user affinity scores.
* Storage: Aggregated metrics stored as precomputed tables or Redis hashes for low-latency reads.

### Payments & Tracking Integration

* Payments: Integration with a PCI-compliant payment gateway via server-side SDK/REST; server handles order and commission calculation, gateway handles tokens; strictly no raw card storage.
* Payouts: Use the same or a compatible provider that supports seller payouts and split payments (or start with manual payouts, but API-ready models).
* Courier APIs:
  + Simple HTTP client modules to poll supported courier APIs.
  + Background workers to refresh tracking status and write to DB/Redis; UI reads cached data for P95 <300ms.

### Security & Compliance

* Secrets Management: Environment variables managed by a secrets store (e.g., cloud provider secrets manager).
* Data Protection: Encryption at rest (DB, backups) and in transit (HTTPS only).
* Access Control: Role-based access (buyer, seller, admin) enforced at API level with middleware/guards.

### DevOps & Deployment

* Hosting: Cloud-based deployment (e.g., containerized with Docker) for backend and frontend.
* CI/CD: Automated tests and deployment pipeline on each main-branch push.
* Observability:
  + Structured logging (JSON) with correlation IDs per request.
  + Metrics on latency (search, checkout, tracking), error rates, and job queues.
