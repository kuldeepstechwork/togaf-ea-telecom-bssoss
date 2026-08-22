# ADR-004: Dual-Write Reconciliation Strategy for the Transition Period

**Status:** Accepted

## Context

ADR-002 designates the new Product Catalog Platform as the sole authoritative system of record for product data, while the legacy billing engine's rating logic continues to read from its own internal product tables (which cannot be changed to read directly from the new catalog without touching the financial ledger, out of scope per Phase A). This creates a specific, named transition-state problem, described as "Dual-Catalog Reconciliation" in `06-phase-f-migration-planning/transition-architectures.md`: two representations of "product" exist concurrently in production, and a decision is required on how they are kept consistent, how consistency is measured, and how the transition state eventually ends.

## Decision

We will implement a **scheduled, one-directional reconciliation service** (the Dual-Write Reconciliation Service SBB) that reads authoritative product changes from the Product Catalog Platform and applies corresponding updates to the legacy billing system's internal product tables on a defined interval, with active lag monitoring and automatic alerting to Billing Operations if reconciliation lag exceeds a defined threshold. The legacy tables are explicitly a **derived, non-authoritative copy** — no write path exists from the legacy billing tables back to the Product Catalog. The reconciliation service is retired, and the legacy tables formally deprecated, only once monitoring shows sustained accuracy and lag within threshold across at least one full billing cycle following the Wave 3 bundle launch (the exit condition defined in the transition architecture document).

## Alternatives Considered

1. **True bidirectional dual-write, with both systems treated as co-authoritative and conflicts resolved by a defined precedence rule.** Rejected because: (a) bidirectional consistency is a substantially harder distributed-systems problem than one-directional reconciliation, requiring conflict detection and resolution logic on both write paths rather than one; (b) it directly conflicts with principle P-01 (every domain has exactly one system of record) in a way one-directional reconciliation does not — one-directional reconciliation has a clear single authority with a governed derivative, while bidirectional dual-write has no single authority at all, which is a materially worse compliance posture for a transitional mechanism that Phase G governance must be able to audit.

2. **Real-time synchronous replication instead of scheduled/interval-based reconciliation.** Rejected for the transition period because: (a) it would require the legacy billing system to accept synchronous inbound calls on every catalog change, which risks impacting the billing engine's real-time charging performance — a risk Phase A's scope boundary (no changes to the financial ledger's core function) is specifically designed to avoid; (b) real-time replication raises the operational stakes of any reconciliation-service outage from "growing lag, monitored and alertable" to "hard synchronous coupling failure," which is a worse failure mode for a transitional component that is explicitly intended to be temporary and eventually removed — over-engineering resilience into a temporary component was judged not worth the cost relative to a scheduled approach with a defined, monitored lag tolerance.

## Consequences

**Positive:** The billing engine's core rating/charging performance and change-control process remain untouched, preserving the regulatory-audit continuity and low-risk posture that justified the strangler-fig approach in the first place (ADR-001). The reconciliation service's one-directional design keeps the compliance story simple: exactly one authoritative source, one governed derivative, auditable by Phase G governance.

**Negative (accepted trade-off):** This is the specific mechanism generating the ~15% operational overhead on affected systems for an estimated 24 months, quantified in the business case. It introduces a real (if monitored and bounded) risk window where a product visible in the catalog has not yet propagated to billing's rating tables, requiring active operational monitoring (Billing Operations role change, addressed in the Phase H change management plan) rather than being a "fire and forget" background process.

## Stakeholders / Governance Affected

Architecture Review Board (approving body; this decision was reviewed under P-01's requirement, though ultimately it does not require unanimous approval as an *exception* to P-01 — it is deemed a compliant, time-boxed implementation of P-01 given the clear single-authority design, a distinction the ARB minutes record explicitly to avoid ambiguity in future audits); VP Billing & Revenue Systems (primary operational risk owner, given the reconciliation lag risk to rating accuracy); Billing Operations staff (direct workflow impact, per Phase H).

---

*Fictional case study — see [README](../README.md) for full disclaimer.*
