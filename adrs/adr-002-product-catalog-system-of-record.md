# ADR-002: Product Catalog System of Record Placement

**Status:** Accepted

## Context

Brenmark's core business problem is that no single system can describe a product spanning mobile, broadband, and 5G-slice domains. Product definitions today live partially in the billing system's product tables (mobile-focused) and partially in the network inventory system (broadband service definitions), with no shared model. A decision is required on where the single authoritative product definition will live going forward, given that the billing engine's financial ledger is explicitly out of scope for replacement (ADR-001).

## Decision

We will designate the new, separately procured **Product Catalog Platform** (Vendor B / Northolt BSS Cloud, per `05-phase-e-opportunities-and-solutions/vendor-evaluation.md`) as the sole system of record for product definitions — including mobile, broadband, 5G-slice, and bundle products. The legacy billing system's internal product tables become a **derived, reconciled copy**, kept consistent via the Dual-Write Reconciliation Service (see ADR-004), not an independent source of truth. All sales channels and the Order Orchestration Platform consume product data exclusively from the Product Catalog Platform via TM Forum Open API.

## Alternatives Considered

1. **Designate the legacy billing system's product tables as the enterprise system of record, extended to cover broadband and slice products.** Rejected because: (a) the billing system's product model was designed for mobile rating/charging, not for describing bundles or 5G-slice SLA parameters (capacity, latency, throughput), and extending it risks entangling new product-definition logic with the financial ledger logic that Phase A explicitly protects from change; (b) it would make every future product-catalog change subject to the billing system's release cycle and regulatory change-control process, which is slower and higher-friction than the standalone catalog platform's, directly working against the 18-month timeline.

2. **Designate the network inventory system as the system of record, since it already models the broadband and (in future) network-slice domain closest to the physical network.** Rejected because: (a) the network inventory system's data model is oriented around network resources and capacity, not commercial product/pricing constructs (price plans, bundle composition, channel availability) — extending it to be a commercial product catalog would require building commerce capability the vendor evaluation confirmed is not that system's strength (see Vendor D's evaluation in `vendor-evaluation.md`, scoring low on converged-bundle commerce modeling); (b) it would put commercial product decisions (pricing, bundling, channel rules) under Network Engineering's change-control process rather than under Product/Commercial ownership, which is an organizationally awkward fit given who actually needs to move fastest on product decisions.

## Consequences

**Positive:** A single, purpose-built commercial product model becomes possible, directly enabling converged bundles and slice products (the program's core mandate). Product/Commercial teams gain direct, fast-cycle control over product definitions without depending on billing or network release cycles.

**Negative (accepted trade-off):** The billing engine's rating logic still reads from its own internal product tables, meaning the Product Catalog is not literally the only place product data exists — it is the only *authoritative* place, with the billing tables as a governed derivative. This requires the reconciliation mechanism in ADR-004 and its associated ~15% transitional operational overhead. There is also switching cost and migration effort to move the currently-siloed mobile and broadband product definitions into the new catalog before Wave 2 can go live, a dependency explicitly sequenced in `06-phase-f-migration-planning/migration-roadmap.md`.

## Stakeholders / Governance Affected

Architecture Review Board (approving body, Head of Data & Analytics accountable for data governance of the new domain); Head of Product/Commercial (primary beneficiary and business owner of the new catalog); VP Billing & Revenue Systems (consulted, given the reconciliation dependency touching billing's product tables).

---

*Fictional case study — see [README](../README.md) for full disclaimer.*
