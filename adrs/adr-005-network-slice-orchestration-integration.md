# ADR-005: Network-Slice Orchestration Integration Approach

**Status:** Accepted

## Context

The board's 18-month mandate requires Brenmark to monetize 5G network slicing — selling differentiated network capacity/SLA as an orderable, billable product. This requires integration between the commercial layer (Product Catalog, Order Orchestration) and the network layer capable of instantiating, activating, and metering a network slice. The selected Product Catalog/Order Orchestration vendor (Vendor B / Northolt BSS Cloud, per ADR-002 and the vendor evaluation) scored only moderately (4/5) on 5G-slice orchestration support, while a competing vendor (Vendor D / Ferro OSS/BSS Platform) scored highest specifically on slice orchestration (5/5) but weakest on the commerce/catalog capability the program needs most broadly. A decision is required on how to deliver slice orchestration integration without re-opening the platform vendor decision.

## Decision

We will **build a dedicated Network-Slice Orchestration Adapter** as an in-house solution building block, integrating Brenmark's chosen Order Orchestration Platform (Vendor B) with the network layer's slice-capable orchestration tooling — coordinated directly with Network Engineering's parallel 5G core/RAN capital program rather than depending on the commercial BSS/OSS vendor to provide this integration natively. This adapter is scoped as a genuine build (not a thin adapter) because no evaluated vendor's out-of-box slice orchestration integration adequately fit Brenmark's specific network equipment vendor mix (see the gap analysis's treatment of G-03).

## Alternatives Considered

1. **Select Vendor D (strongest on slice orchestration) as the primary Product Catalog/Order Orchestration platform instead of Vendor B, prioritizing the board's slice mandate above the broader converged-bundle capability.** Rejected because: (a) Vendor D scored weakest of all four evaluated vendors on converged-bundle commerce modeling and Open API conformance — the two highest-weighted criteria in the evaluation — meaning this choice would solve the narrower slice-mandate problem while leaving the broader (and, per the business case, larger-value) converged-bundle problem under-addressed; (b) the business case shows converged-bundle revenue ($23.3M cumulative 3-year projection driver, primarily from bundles rather than slice revenue in years 1–2) as the larger near-term value driver, making a platform choice optimized narrowly for slice orchestration a poor fit for the program's overall value proposition.

2. **Adopt Vendor D's slice-orchestration module as a bolt-on alongside the Vendor B platform, integrating the two vendor products directly with each other.** Rejected because: (a) it introduces a second commercial vendor relationship and contract into the critical path for the highest-priority mandate item (5G-slice launch), adding procurement and integration timeline risk that a single-vendor, EA-owned adapter build avoids; (b) it creates exactly the kind of vendor-to-vendor point-to-point integration principle P-10 is designed to prevent, and would need to route through the centralized API Gateway anyway (per ADR-003) — at which point building a purpose-fit adapter behind that gateway, rather than integrating two vendor products' native interfaces to each other, was judged the architecturally cleaner and more governable path.

## Consequences

**Positive:** Brenmark's platform decision (ADR-002/vendor evaluation) is optimized for its largest and most broadly-applicable business value driver (converged bundles) without being compromised by the narrower slice-orchestration requirement, while the slice requirement is still met on the mandate timeline via a dedicated, EA-governed build. The adapter's build-vs-buy status (P-05) is explicit and defensible: it exists because the gap analysis confirmed no adequate commodity option existed for Brenmark's specific integration need, not as a default preference for building.

**Negative (accepted trade-off):** Brenmark carries the engineering cost and delivery risk of an in-house build (estimated at 105 person-months, per the business case) for slice orchestration, rather than relying on a vendor's pre-built, presumably more battle-tested integration. This build sits on the critical path for the board's mandate (Wave 3, per the migration roadmap), making it one of the higher-risk single components in the entire program from a schedule-risk perspective, and it is coordinated with a parallel Network Engineering capital program whose own timeline is a dependency this architecture does not fully control.

## Stakeholders / Governance Affected

Architecture Review Board (approving body); VP Network Engineering (primary technical dependency owner, given coordination required with the parallel 5G capital program); CTO and Board Technology Committee (this decision directly determines whether the board's core mandate deadline is achievable, making schedule variance on this specific adapter a mandatory escalation trigger per the roadmap governance terms in `06-phase-f-migration-planning/migration-roadmap.md`).

---

*Fictional case study — see [README](../README.md) for full disclaimer.*
