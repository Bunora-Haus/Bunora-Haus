# BUNORA HAUS

### Luxury Commerce. Curated Experiences. Engineered Infrastructure.

**Bunora Haus** is a luxury commerce and experiences business supported by a purpose-built digital platform that unifies retail, customer relationships, payments, logistics, curated workshops, and business operations.

The platform is designed and engineered as a production-oriented commerce ecosystem, combining domain-driven backend architecture, modern web applications, systems programming, secure cloud infrastructure, and integrated business workflows.

[**Official Website**](https://bunorahaus.com) · [**Lead Engineer — Vernan Shikir**](https://github.com/vernan06)

---

## About the Business

Bunora Haus is built around a vision of thoughtful curation, refined customer experiences, and modern luxury retail.

The business aims to bring together carefully selected products, meaningful experiences, and personalized customer engagement through a cohesive digital environment.

Beyond conventional e-commerce, Bunora Haus is designed to support workshops, experience bookings, customer relationships, fulfillment operations, and internal business management.

The objective is to create a scalable foundation where the customer experience and the systems powering the business are developed together.

### Our Philosophy

**Curated Commerce** — A considered approach to products, collections, and discovery.

**Experiences Beyond Retail** — Connecting customers with workshops and curated experiences.

**Customer-Centric Design** — Building intuitive, accessible, and refined digital interactions.

**Engineering Excellence** — Developing reliable, secure, and maintainable systems to support long-term business growth.

---

## The Bunora Haus Platform

The Bunora Haus platform is a custom-engineered commerce and business operations system.

It is designed to manage the complete commercial lifecycle, from product discovery and customer authentication to transactions, fulfillment, communications, and after-sales support.

### Platform Scope

| Business Area | Platform Responsibilities |
|---|---|
| Digital Storefront | Product discovery, collections, merchandising, search, filtering, and responsive shopping experiences |
| Catalogue & Inventory | Product information, variants, availability, stock records, and catalogue administration |
| Customer Identity | Registration, authentication, profiles, saved addresses, sessions, and account security |
| Commerce & Orders | Shopping cart, checkout coordination, order management, and order lifecycle |
| Payments & Finance | Payment processing, transaction records, refunds, and reconciliation |
| Experiences | Workshops, curated events, availability, reservations, and booking management |
| Fulfillment | Shipment creation, logistics integration, delivery tracking, and fulfillment operations |
| Communications | Transactional emails, notifications, and customer messaging workflows |
| Customer Support | Customer inquiries, assistance, and post-purchase service |
| Business Operations | Administrative workflows, internal controls, staff tools, and operational management |

The platform is under active development, with individual capabilities implemented and verified progressively.

---

## Technology Stack

Bunora Haus uses a multi-language technology stack, with each technology selected for a specific architectural responsibility.

| Layer | Technology |
|---|---|
| Backend Application | [Go](https://go.dev/) |
| Systems & Traffic Control | [Rust](https://www.rust-lang.org/) |
| Frontend Framework | [Next.js](https://nextjs.org/) |
| UI Library | [React](https://react.dev/) |
| Frontend Language | [TypeScript](https://www.typescriptlang.org/) |
| Primary Database | [PostgreSQL](https://www.postgresql.org/) |
| Caching & Coordination | [Redis](https://redis.io/) |
| Reverse Proxy | [Caddy](https://caddyserver.com/) |
| Containerization | [Docker](https://www.docker.com/) |
| Deployment Orchestration | [Docker Compose](https://docs.docker.com/compose/) |
| Edge & Security | [Cloudflare](https://www.cloudflare.com/) |
| Object Storage | [Cloudflare R2](https://developers.cloudflare.com/r2/) |
| Production Hosting | [Hostinger VPS](https://www.hostinger.com/vps-hosting) |
| CI/CD | [GitHub Actions](https://github.com/features/actions) |
| Container Registry | [GitHub Container Registry](https://docs.github.com/en/packages) |

### External Service Integrations

The platform architecture supports integrations with:

- [Razorpay](https://razorpay.com/) — Payment processing and refunds.
- [Delhivery](https://www.delhivery.com/) — Direct shipping and fulfillment.
- [Google Identity](https://developers.google.com/identity) — Customer authentication through OpenID Connect.
- [Cloudflare Turnstile](https://developers.cloudflare.com/turnstile/) — Automated-abuse protection.
- [Cloudflare Zero Trust](https://www.cloudflare.com/zero-trust/) — Restricted staff and private application access.
- SMTP — Transactional email and operational communications.

Provider functionality is enabled only after the relevant integration and production acceptance requirements have been satisfied.

---

## System Architecture

The backend follows a **domain-driven modular monolith architecture**.

Instead of distributing every business function across independently deployed microservices, Bunora Haus maintains strongly separated business engines within a unified Go application.

This provides explicit ownership and controlled communication while avoiding unnecessary distributed-system complexity.

### Logical Architecture

```text
                    BUNORA HAUS
                         |
                  CLOUDFLARE EDGE
                DNS / TLS / SECURITY
                         |
                  CLOUDFLARE TUNNEL
                         |
                       CADDY
                         |
               RUST TRAFFIC CONTROLLER
                         |
              +----------+----------+
              |                     |
              v                     v
        CUSTOMER APP             STAFF APP
          Next.js                 Next.js
              |                     |
              +----------+----------+
                         |
                         v
                  GO APPLICATION API
                         |
               DOMAIN ENGINE LAYER
                         |
     +-------------------+-------------------+
     |                   |                   |
     v                   v                   v
   COMMERCE            FINANCE            IDENTITY
   EXPERIENCES         FULFILLMENT        COMMUNICATIONS
   OPERATIONS          SUPPORT            POLICY
                       CORRELATOR
                         |
              +----------+----------+
              |                     |
              v                     v
          POSTGRESQL               REDIS
                         |
                EXTERNAL SERVICES
```

This diagram illustrates the logical system components and their responsibilities, rather than every individual network connection.

---

## The Ten-Engine Architecture

The core Go application is organized into ten distinct business engines.

Each engine owns its domain responsibilities, internal logic, and persistence boundaries.

### 01 — Commerce Engine

Manages the retail commerce lifecycle, including product discovery contracts, shopping interactions, carts, checkout coordination, and order workflows.

### 02 — Finance Engine

Owns financial transactions, payment-provider integration, payment state, refunds, and reconciliation-related operations.

### 03 — Experiences Engine

Supports curated experiences and workshops, including schedules, availability, reservations, and booking lifecycle management.

### 04 — Fulfillment Engine

Manages shipment workflows, carrier integration, tracking, delivery state, and post-purchase logistics coordination.

### 05 — Communications Engine

Handles transactional messaging, notification processing, email delivery, sender identities, and communication workflows.

### 06 — Identity Engine

Manages customer accounts, authentication, password recovery, profiles, sessions, saved addresses, and identity security.

### 07 — Operations Engine

Supports internal business management, administrative processes, catalogue operations, and staff-facing workflows.

### 08 — Support Engine

Manages customer-service processes, support requests, issue handling, and post-purchase assistance.

### 09 — Policy Engine

Provides policy evaluation, authorization, permissions, and enforcement of business and operational access rules.

### 10 — Correlator Engine

Supports cross-domain correlation and workflow coordination while preserving ownership boundaries between engines.

### Engineering Principles Behind Engine Separation

The architecture follows several core rules:

1. **Explicit Domain Ownership** — Every business responsibility belongs to a defined engine.
2. **Controlled Communication** — Engines interact through established contracts rather than unrestricted internal access.
3. **Database Isolation** — Domain-owned PostgreSQL schemas separate persistence responsibilities.
4. **Opaque Cross-Domain References** — Cross-engine relationships avoid tightly coupled cross-schema foreign keys.
5. **Independent Maintainability** — Engine implementations can evolve without unnecessary changes to unrelated domains.
6. **Centralized Deployment, Modular Design** — The application benefits from modular separation without requiring a separate network service for every engine.

This architecture is intended to balance scalability, maintainability, performance, and operational simplicity.

---

## Frontend Engineering

The platform separates its customer-facing storefront from its restricted internal management application.

### Customer Storefront

Built with Next.js, React, and TypeScript, the storefront emphasizes editorial design, product presentation, discovery, responsive layouts, and accessible customer interactions.

Its design direction combines premium visual presentation with practical commerce functionality.

### Internal Staff Application

The staff application is independently deployed and intended for authorized business operations.

It provides a separate interface for administrative and operational workflows, with access controlled through application authorization and infrastructure-level restrictions.

This separation reduces the exposure of internal business functionality to public storefront traffic.

---

## Rust-Based Traffic Engineering

Bunora Haus incorporates a dedicated Rust traffic-control component.

The controller is designed to manage infrastructure-level request handling independently from the business application.

Its architectural scope includes:

- Request classification and routing.
- Health-aware traffic distribution.
- Rate limiting.
- Bounded queues and backpressure.
- Traffic prioritization.
- Timeouts and circuit-breaking behavior.
- Connection management.
- Controlled retries and request safety.
- Request correlation and operational telemetry.
- Graceful connection draining.

Rust is used for this layer because of its memory-safety model, predictable resource management, and suitability for performance-sensitive infrastructure components.

---

## Database & Data Engineering

PostgreSQL serves as the primary transactional data store.

The database architecture reflects the separation of business engines and supports controlled data access.

### Key Design Considerations

- Domain-owned schemas.
- Role-based database permissions.
- Relational constraints and indexing.
- Transactional consistency.
- Forward-only schema migrations.
- Migration integrity validation.
- TLS-protected database connections.
- Persistent production data.
- Encrypted backup workflows.
- Isolated restoration testing.

Redis is used for selected coordination, caching, and traffic-control requirements.

The system is designed to keep durable business records in PostgreSQL rather than relying on transient caching infrastructure.

---

## Security Engineering

Security is a foundational concern across the platform.

### Application Security

- Secure authentication and session handling.
- Customer and staff access separation.
- Role-based authorization.
- Input validation.
- Content Security Policy.
- Secure cookies.
- Explicit provider activation controls.
- Protected administrative routes.

### Infrastructure Security

- Cloudflare edge protection.
- Private origin connectivity.
- Cloudflare Tunnel.
- Cloudflare Zero Trust Access.
- TLS-encrypted communications.
- Restricted service exposure.
- Container network isolation.
- Protected application secrets.

### Data Security

- Domain-scoped database access.
- Dedicated service credentials.
- Encrypted backups.
- Private object storage.
- Independent recovery-key management.
- Controlled database migration and restoration procedures.

Security-sensitive operations are subject to dedicated verification before production activation.

---

## Infrastructure & DevOps

Bunora Haus is engineered for reproducible, controlled deployment on a Linux VPS.

The production architecture combines containerized application services with Cloudflare's edge and infrastructure services.

### Infrastructure Components

**Docker & Docker Compose**

Provide repeatable application packaging, service configuration, and runtime orchestration.

**GitHub Actions**

Support automated build, validation, and release workflows.

**GitHub Container Registry**

Stores versioned container artifacts for deployment.

**Cloudflare**

Provides DNS, edge connectivity, security, private access, and object-storage integrations.

**Caddy**

Provides origin-side HTTP routing and reverse-proxy functionality.

**PostgreSQL & Redis**

Provide transactional persistence and selected runtime coordination.

### Release Engineering

The deployment process is designed around:

1. Source-controlled changes.
2. Automated verification.
3. Immutable release artifacts.
4. Explicit production configuration.
5. Forward-only database migrations.
6. Controlled deployment.
7. Health and security checks.
8. Backup and recovery verification.
9. Traceable release checkpoints.

This approach emphasizes reliability and reproducibility over ad hoc production changes.

---

## Engineering Objectives

Bunora Haus is developed with several long-term objectives.

**Maintainable Architecture**

Keep business domains independent and understandable as platform complexity increases.

**Security and Reliability**

Protect customer data, business operations, and production infrastructure through layered controls.

**Performance**

Design application and infrastructure components to use resources efficiently and provide responsive experiences.

**Operational Efficiency**

Use practical infrastructure choices appropriate to business requirements rather than introducing unnecessary hosting complexity.

**Scalability**

Maintain a foundation capable of supporting additional products, customers, experiences, operational workflows, and integrations.

**Engineering Ownership**

Build a platform whose architecture, application logic, deployment systems, and operational procedures can be understood, maintained, and improved as one coherent system.

---

## Development Status

**Bunora Haus is under active development.**

The platform is being delivered through progressive implementation, integration, and verification of its business capabilities.

The public website and the underlying commerce platform have separate release requirements. Features are made publicly available only after completing their applicable production acceptance checks.

The presence of a technology or integration in this overview does not imply that every associated business workflow is currently live.

---

## About This Repository

This is the public-facing GitHub repository for Bunora Haus.

It provides an overview of the business, software architecture, engineering approach, technology stack, and development direction.

The production application source code, infrastructure credentials, private configuration, and internal operational documentation are maintained separately.

This repository is intended for public information and technical presentation.

It is not a distribution of the production commerce application.

---

## Project Leadership

### Vernan Shikir

**Founder · Lead Software Engineer · Systems Architect**

[GitHub Profile](https://github.com/vernan06)

Bunora Haus is independently architected and engineered by Vernan Shikir, who leads the technical direction, system design, backend architecture, infrastructure engineering, security architecture, and full-stack development of the platform.

The engineering work spans the complete application lifecycle, including domain modeling, systems programming, database architecture, frontend development, cloud infrastructure, deployment automation, and production verification.

The platform reflects a focus on building technically rigorous software systems that support real business operations.

---

## Official Website

**[www.bunorahaus.com](https://bunorahaus.com)**

For information about the business, visit the official website.

---

### Built by Vernan Shikir

**Lead Software Engineer — Bunora Haus**

*Architecting the systems. Engineering the platform. Building the business.*

**Bunora Haus — Engineered for Commerce. Designed for Experience.**
