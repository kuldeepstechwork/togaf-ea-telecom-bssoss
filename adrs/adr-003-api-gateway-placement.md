# ADR-003: TM Forum Open API Gateway Placement

**Status:** Accepted

## Context

The strangler-fig strategy (ADR-001) requires a consistent way for new components (Product Catalog, Order Orchestration, Customer Domain Service) to reach legacy systems (billing, CRM, network inventory) without each new component building its own bespoke integration to each legacy system's native interface. A decision is required on where API gateway enforcement sits architecturally — specifically, whether it is a single centralized ingress/egress point or a set of distributed, per-component gateways.

## Decision

We will implement a **single centralized API Gateway/Strangler Layer** as the sole ingress and egress point between all new components, all channels, and all legacy systems. No new component integrates directly with a legacy system's native interface; every such integration is a thin adapter (Legacy Billing Adapter, Legacy Network Inventory Adapter) sitting behind the same centralized gateway, which enforces authentication, schema validation against TM Forum Open API patterns, rate limiting, and routing uniformly for all traffic (see `04-phase-d-technology-architecture/reference-architecture.md`).

## Alternatives Considered

1. **Distributed gateways, one per new component (e.g., Product Catalog has its own gateway to Billing; Order Orchestration has its own gateway to Network Inventory).** Rejected because: (a) it reproduces, at a smaller scale, exactly the integration fragmentation this program exists to eliminate — each component team would make independent decisions about auth, schema validation, and versioning, and P-10 (one owner, one governance record per integration) becomes unenforceable without a central point to audit against; (b) it multiplies the number of places a legacy-system change (e.g., a billing API version bump) has to be coordinated, increasing operational risk rather than reducing it.

2. **No dedicated gateway layer; new components call legacy systems' native interfaces directly, translating internally.** Rejected because: (a) it directly violates P-02 (Open API standards) by baking legacy-specific translation logic into every consuming component rather than centralizing it once; (b) every future legacy retirement or replacement (e.g., eventually replacing the network inventory system) would require changing every consuming component's integration code, rather than changing one adapter behind a stable gateway contract — this directly undermines the reversibility principle (P-04) that the whole strangler strategy depends on.

## Consequences

**Positive:** A single enforcement point makes P-02 and P-10 compliance auditable and governable in practice, not just in principle — the compliance register (Phase G) can inspect gateway logs rather than needing to audit every component individually. Legacy system replacement or retirement, when it eventually happens, requires changing the relevant adapter behind the gateway, not every consumer.

**Negative (accepted trade-off):** The centralized gateway is a single point of failure for all order and catalog traffic if not built to the 99.95% availability target set in Phase D — this raises the criticality (and cost) of the gateway component itself above what any individual distributed gateway would have carried alone. It also introduces a coordination bottleneck: every new integration must go through the centrally-governed gateway team's onboarding process, which is slower per-integration than a component team standing up its own point-to-point call, a cost accepted in exchange for governability.

## Stakeholders / Governance Affected

Architecture Review Board (approving body); all solution-building-block delivery teams (bound by this decision as a mandatory dependency, per the sequencing note in `05-phase-e-opportunities-and-solutions/solution-building-blocks.md`); Head of InfoSec (the gateway is the central enforcement point for P-06 access control across all cross-system traffic).

---

*Fictional case study — see [README](../README.md) for full disclaimer.*
