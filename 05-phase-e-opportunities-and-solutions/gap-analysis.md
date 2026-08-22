# Gap Analysis

**Phase:** E — Opportunities & Solutions

## Purpose

This gap analysis translates the capability maturity gaps identified in `02-phase-b-business-architecture/capability-map.md` into specific, prioritized architectural gaps that the solution building blocks (`solution-building-blocks.md`) and migration roadmap (Phase F) must close. Gaps are prioritized using a simple Impact × Urgency scoring, reflecting both business value and the 18-month mandate deadline.

## Prioritized Gap Register

| # | Gap | Impact (1–5) | Urgency (1–5) | Priority Score | Closing Mechanism |
|---|---|:---:|:---:|:---:|---|
| G-01 | No unified product catalog spanning mobile/broadband/slice | 5 | 5 | 25 | Product Catalog Platform SBB (Vendor B) |
| G-02 | No automated cross-domain order orchestration | 5 | 5 | 25 | Order Orchestration Platform SBB (Vendor B) |
| G-03 | No 5G network-slice product/orchestration integration | 5 | 5 | 25 | Network-Slice Orchestration Adapter SBB (build) |
| G-04 | No unique/shared customer identifier across CRM and Billing | 4 | 4 | 16 | Customer Domain Service SBB (build) |
| G-05 | No API gateway / integration governance | 4 | 4 | 16 | API Gateway/Strangler Layer SBB (buy + configure) |
| G-06 | Legacy billing/network systems not API-addressable | 4 | 4 | 16 | Legacy Billing Adapter + Legacy Network Inventory Adapter SBBs |
| G-07 | No mechanism to keep legacy billing product tables consistent with new catalog during transition | 3 | 4 | 12 | Dual-Write Reconciliation Service SBB (build); governed by ADR-004 |
| G-08 | No unified RBAC/access control across new shared data domains | 4 | 3 | 12 | RBAC/Access Control Uplift SBB (extend existing enterprise IdP) |
| G-09 | No integration inventory / undocumented point-to-point links | 3 | 3 | 9 | Populated as part of API Gateway rollout; enforced under P-10 |
| G-10 | Frontline staff workflows and training not yet redesigned for automated orchestration | 3 | 3 | 9 | Phase H change management plan |
| G-11 | No usage-based billing construct for non-traditional (slice) products | 3 | 3 | 9 | Order Orchestration + Legacy Billing Adapter jointly (charge-instruction extension) |
| G-12 | No defined legacy decommissioning path/timeline beyond this program | 2 | 2 | 4 | Deliberately deferred — flagged as a candidate for a follow-on program per Phase A scope boundaries |

## How Priority Drove Sequencing

The top three gaps (G-01, G-02, G-03) share the maximum priority score and map directly to Brenmark's three named business problems from Phase A (no converged bundles, slow provisioning, no slice monetization) — all three are addressed in the earliest delivery waves of the migration roadmap (Phase F), not sequenced by convenience. G-06 (legacy adapters) is lower-scored individually but is a hard technical prerequisite for G-01/G-02/G-03 to be testable at all, which is why — despite its middling priority score — it is scheduled in Wave 1 ahead of the higher-scored platform builds (see the sequencing dependency note in `solution-building-blocks.md`).

G-12 (legacy decommissioning path) scores lowest and is explicitly not solved by this program — consistent with the Phase A scope boundary that this program builds the strangler layer and begins incremental migration, but does not commit to a legacy shutdown date within 18 months.

## Gaps Considered But Not Adopted as Separate Line Items

Two gaps were evaluated during Phase E and deliberately folded into existing SBBs rather than tracked separately, to avoid solution-building-block sprawl:

- **A generic Master Data Management (MDM) platform for customer data** was considered as a way to close G-04, but rejected in favor of the thin, purpose-built Customer Domain Service — a full MDM platform procurement and implementation was judged to add 6+ months of vendor selection and implementation time that the 18-month mandate cannot absorb, for a capability (multi-domain golden-record MDM) broader than what Brenmark's two-source (CRM + Billing) reconciliation problem actually requires.
- **A separate "billing modernization" gap** (upgrading the financial ledger's own technology stack) was raised by some Billing stakeholders during Phase E workshops but was excluded from the gap register entirely, because it is out of scope per Phase A — the financial ledger is stable and not a source of the business problems this program is funded to solve; including it would have diluted focus and budget away from the mandate-critical gaps above.

---

*Fictional case study — see [README](../README.md) for full disclaimer.*
