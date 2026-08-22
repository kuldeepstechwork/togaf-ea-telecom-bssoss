# ADR-001: Strangler-Fig Modernization vs. Full Rip-and-Replace

**Status:** Accepted

## Context

Brenmark's board has mandated 5G network-slicing monetization within 18 months, and the business requires converged (mobile + broadband + slice) bundled products to compete effectively. The current BSS/OSS estate — a monolithic billing system, a disconnected CRM, and a manual-handoff network inventory/order management system — cannot support either requirement without significant architectural change. The billing system performs real-time charging for approximately 6 million subscribers and is regulator-audited; it is Brenmark's most business-critical and highest-continuity-risk system in scope.

## Decision

We will modernize using a **strangler-fig pattern**: a TM Forum Open API–conformant gateway and a new Product Catalog and Order Orchestration layer are placed in front of the legacy billing, CRM, and network inventory systems. New capability — including converged bundles and 5G-slice products — is built on this new layer. Legacy systems, particularly the billing engine's financial ledger, remain in place and are reached via API rather than replaced. Capability migrates off legacy systems incrementally over time, governed by named transition architectures (see `06-phase-f-migration-planning/transition-architectures.md`), rather than through a single cutover event.

## Alternatives Considered

1. **Full BSS/OSS rip-and-replace.** Replace billing, CRM, and network inventory/order management with a new integrated platform in a single program. Rejected because: (a) full replacement of a real-time charging engine for 6M subscribers is a multi-year undertaking under any realistic estimate, incompatible with the 18-month mandate; (b) it concentrates all migration risk into one or a small number of large cutover events, which the business's risk appetite for its revenue-critical billing system will not accept; (c) illustrative cost modeling put full replacement capex at 3–4x the strangler-fig approach's $18.4M estimate, with a payback period extending well beyond the 3-year horizon evaluated in the business case.

2. **Greenfield BSS/OSS for new products only, legacy untouched indefinitely.** Build an entirely separate, modern BSS/OSS stack exclusively for new converged/slice products, leaving all 6M existing subscribers permanently on the legacy stack with no path to migrate. Rejected because: (a) it does not solve the underlying fragmentation problem for the existing subscriber base, meaning most of Brenmark's revenue would remain on a system unable to ever offer bundles; (b) it creates a second permanent BSS/OSS estate to operate and govern indefinitely, which is a materially worse long-term operating-cost and complexity outcome than a bounded transition; (c) it violates architecture principle P-01 (customer/product/order as enterprise data) by design, since it deliberately creates a second, disconnected customer/product universe rather than solving the original disconnection.

## Consequences

**Positive:** The program can deliver converged bundles and slice monetization within the 18-month mandate without betting the entire program on a high-risk big-bang cutover of the billing engine. Legacy capability retirement can proceed incrementally and be paused or adjusted without stranding the new capability, satisfying principle P-04 (reversibility).

**Negative (accepted trade-off):** The strangler layer must maintain dual-write consistency between the legacy billing system's product tables and the new Product Catalog for an estimated 24 months (see ADR-004), introducing reconciliation complexity and an estimated 15% ongoing operational overhead on affected systems during that period — quantified in `01-phase-a-vision-and-scope/business-case.md`. The architecture also carries two concurrent "views" of certain data (legacy and new) during the transition, a condition normally disallowed by P-01, tolerated here only because it is explicitly time-boxed and governed.

## Stakeholders / Governance Affected

Architecture Review Board (approving body); VP Billing & Revenue Systems (primary risk owner, sign-off required on go-live per Phase A RACI); CTO and Board Technology Committee (accountable for the 18-month mandate outcome this decision is designed to satisfy).

---

*Fictional case study — see [README](../README.md) for full disclaimer.*
