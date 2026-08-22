# Architecture Principles

**Phase:** Preliminary
**Owner:** Enterprise Architecture Function, Brenmark Telecom
**Approved by:** Architecture Review Board (ARB)

These principles govern every architectural decision made in the Brenmark Telecom BSS/OSS modernization program. Each is written in standard TOGAF format — Name, Statement, Rationale, Implications — and each is binding on delivery teams unless an exception is granted per the process in `04-phase-d-technology-architecture/technology-standards.md`. Principles are numbered for traceability; ADRs and architecture contracts cite them by number (e.g., "P-03").

---

### P-01 — Customer, Product, and Order Are Enterprise Data, Not System Data

**Statement:** Customer, product catalog, and order data are enterprise assets owned by the business, not by any single application. No system may be the sole, ungoverned source of truth for an enterprise data domain.

**Rationale:** Brenmark's core problem — the inability to launch converged bundles — exists precisely because billing, CRM, and order management each grew their own private notion of "customer" and "product." Treating these domains as enterprise assets with a defined system of record (Phase C) is the precondition for any converged product.

**Implications:** Every new system must consume, not duplicate, the designated system of record for a domain via governed APIs. Legacy systems that currently own duplicate copies must migrate to a subscriber/consumer role over the transition period defined in Phase F. New local caches require an explicit reconciliation strategy (see ADR-004).

---

### P-02 — Interoperability Follows TM Forum Open API Standards

**Statement:** All new and modernized BSS/OSS interfaces expose and consume TM Forum Open APIs (e.g., patterns aligned to TMF622 Product Ordering, TMF637 Product Inventory, TMF629 Customer Management) rather than proprietary or point-to-point integration contracts.

**Rationale:** Telecom-specific standards exist precisely to solve the integration fragmentation Brenmark suffers from, and they give Brenmark a market of interchangeable vendors and integrators instead of lock-in to one proprietary integration style.

**Implications:** Every new integration point goes through the API gateway layer (Phase D) rather than direct point-to-point calls. Vendor selection (Phase E) weights Open API conformance heavily. Existing point-to-point integrations must be inventoried and scheduled for retirement.

---

### P-03 — Modernize Incrementally; Never Freeze Revenue-Critical Systems

**Statement:** The program will not require a "big bang" cutover of any revenue-critical system (billing, active provisioning). Modernization proceeds in incrementally shippable, independently valuable waves.

**Rationale:** Brenmark's billing system processes real-time charging for 6M subscribers; a failed big-bang cutover is a business continuity risk the board will not accept, and the 18-month 5G-slicing deadline does not allow time to recover from one.

**Implications:** This principle directly drives the strangler-fig pattern selection over rip-and-replace (see ADR-001). It requires the program to accept a period of dual-write/dual-read complexity (ADR-004) as the cost of avoiding cutover risk.

---

### P-04 — Architecture Decisions Are Traceable and Reversible by Default

**Statement:** Every architecturally significant decision is recorded as an ADR with alternatives considered and consequences stated, and wherever technically feasible, the architecture favors reversible decisions over irreversible ones.

**Rationale:** An 18-month program under board scrutiny cannot afford decisions whose rationale is lost to attrition, nor commitments that can't be unwound if a vendor or approach underperforms.

**Implications:** Solution building blocks are evaluated partly on exit cost (Phase E). ARB will not approve a design that lacks a documented rollback or reversal path for its highest-risk elements.

---

### P-05 — Buy Commodity Capability, Build Differentiated Capability

**Statement:** Where a TM Forum ODA-aligned commercial product exists that meets Brenmark's functional and non-functional requirements, Brenmark buys and configures it rather than building bespoke software. Brenmark builds only where a capability is a genuine competitive differentiator (e.g., converged bundle pricing logic, 5G-slice monetization rules).

**Rationale:** Engineering effort is Brenmark's scarcest resource against an 18-month deadline; commodity BSS/OSS capability (product catalog engines, order orchestration) is well served by mature vendor platforms, and building it in-house is pure schedule and cost risk with no competitive upside.

**Implications:** Vendor evaluation (Phase E) is a first-class activity, not an afterthought. Build-vs-buy is documented per solution building block. In-house builds require ARB justification against this principle.

---

### P-06 — Security and Data Privacy Are Designed In, Not Bolted On

**Statement:** Every new component is designed to enforce data privacy (subscriber PII, location data implied by network-slice usage) and role-based access control from first release, not retrofitted after launch.

**Rationale:** Telecom subscriber and location data carries regulatory obligations (telecom-sector privacy regulation and general data protection obligations); retrofitting access control after a system holds live subscriber data is materially more expensive and carries breach exposure in the interim.

**Implications:** Every architecture contract (Phase G) requires a completed data classification and access control design before implementation approval. Network-slice telemetry, which can reveal subscriber location and behavior, is classified as sensitive PII by default.

---

### P-07 — One Product Catalog, Multiple Channels

**Statement:** There is exactly one authoritative product catalog capable of describing any sellable product — mobile, broadband, or 5G network slice, individually or bundled — and every sales channel (retail, digital, partner) consumes it via the same API contract.

**Rationale:** This is the direct architectural answer to Brenmark's core business problem: converged bundles are impossible while three systems each hold an incompatible partial view of "product."

**Implications:** The legacy billing system's internal product tables become a consumer, not a source, of catalog data during the transition (see ADR-002 on system-of-record placement). Any channel-specific product logic must be expressed as catalog configuration, not channel-side code.

---

### P-08 — Network Slicing Is Treated as a Sellable Product from Day One

**Statement:** The product catalog and order management data models are designed to represent a 5G network slice as a first-class orderable, billable product — with its own SLA parameters, capacity, and pricing dimensions — not bolted on as a special case after launch.

**Rationale:** The board's 18-month mandate is specifically 5G-slice monetization; if the to-be data model cannot natively express a network slice as a product, the program fails its primary mandate regardless of what else it delivers.

**Implications:** Data architecture (Phase C) must validate the product and order models against network-slicing use cases before ARB sign-off, not as a later extension. Network orchestration integration (see ADR-005) is scoped into Phase D, not deferred to a "phase 2."

---

### P-09 — Automate Provisioning; Eliminate Manual Handoffs as the Default Path

**Statement:** The target architecture automates end-to-end order-to-activation for standard product configurations. Manual handoffs are the explicit exception path for non-standard orders, not the default for all orders.

**Rationale:** Days-long manual provisioning is a named business problem in this program's mandate; an architecture that reduces provisioning time only for some products, while leaving the default path manual, does not solve the problem it was funded to solve.

**Implications:** Order orchestration (Phase C/E) must support closed-loop automation to network inventory and activation systems. Exception-path volume is tracked as an operational KPI (Phase H) and is expected to shrink, not stay flat, release over release.

---

### P-10 — Every Integration Has One Owner and One Governance Record

**Statement:** Every system-to-system integration in scope has a named accountable owner and is registered in the architecture's integration inventory; no integration exists that the EA function cannot enumerate.

**Rationale:** Brenmark's current-state integration sprawl (undocumented point-to-point links between billing, CRM, and order management) is itself part of why change is currently slow and risky; an unmanaged integration inventory would simply reproduce the current problem inside the new architecture.

**Implications:** The API gateway (Phase D) is also the enforcement point for this principle — unregistered point-to-point traffic is treated as a non-compliance finding under Phase G governance.

---

### P-11 — Non-Functional Requirements Are Binding, Not Aspirational

**Statement:** Availability, latency, and throughput targets for BSS/OSS components (e.g., real-time charging availability, order API latency) are stated as binding acceptance criteria in every architecture contract, with explicit measurement methods.

**Rationale:** BSS/OSS systems are revenue-critical infrastructure; an architecture that meets functional scope but silently degrades availability or performance is a regression Brenmark's customers and board will not tolerate.

**Implications:** Solution building blocks (Phase E) are evaluated against stated NFR targets, not just functional fit. Architecture contracts (Phase G) are non-compliant by default if NFR acceptance testing is skipped.

---

### P-12 — Change Is a Planned Program Activity, Not a Side Effect of Delivery

**Statement:** Organizational change (new processes, retraining, role changes for CRM/billing/network operations staff) is planned and resourced as explicitly as the technical migration, with its own roadmap and success metrics.

**Rationale:** A converged BSS/OSS platform changes how customer service, billing operations, and network operations staff do their jobs; treating this as an unplanned by-product of the technical rollout is a proven cause of adoption failure in platform modernization programs.

**Implications:** Phase H (`08-phase-h-change-management/`) is resourced and tracked with the same rigor as the technical phases, with its own budget line in the business case (Phase A).

---

*Fictional case study — see [README](../README.md) for full disclaimer.*
