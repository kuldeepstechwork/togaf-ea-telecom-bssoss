# Capability Map

**Phase:** B — Business Architecture

This capability map rates Brenmark's core BSS/OSS-relevant business capabilities on a 1–5 maturity scale, as-is versus target (18-month) state. Maturity is rated using a standard capability maturity convention:

**1 = Ad hoc/manual** · **2 = Repeatable but siloed** · **3 = Defined and documented, still siloed** · **4 = Managed and integrated** · **5 = Optimized, shared, and API-governed**

## Capability Maturity Ratings

| Capability | As-Is Maturity | Target Maturity | Gap | Notes |
|---|:---:|:---:|:---:|---|
| Customer identity & 360 view | 2 | 5 | 3 | No shared customer ID across billing/CRM today; target is a single governed Customer Domain service. |
| Product catalog management | 1 | 5 | 4 | Largest gap in the map — today, product definition exists as disconnected tables in two systems with no catalog concept at all. |
| Order capture | 2 | 5 | 3 | Order capture exists (in CRM) but cannot express cross-domain products. |
| Order orchestration / fulfillment | 1 | 4 | 3 | Today fulfillment is manual human coordination; target is automated orchestration with a deliberately retained manual exception path (capped at 4, not 5, by design — see P-09). |
| Network provisioning (standard config) | 2 | 5 | 3 | Manual work-order driven today; target is closed-loop API-driven activation for standard cases. |
| 5G network-slice product management | 1 | 4 | 3 | Does not exist today in any form; target reaches "managed and integrated" within 18 months, with further optimization expected in a follow-on program. |
| Billing & charging (financial ledger) | 4 | 4 | 0 | Deliberately unchanged — mature, audited, and out of scope (see Phase A scope boundaries and ADR-001). |
| Usage-based billing for non-traditional products (e.g., slice) | 1 | 3 | 2 | New capability; reaches "defined and documented" within scope, with deeper optimization deferred beyond the 18-month program. |
| Case management / customer support | 3 | 4 | 1 | CRM case management itself is reasonably mature; the gap is entirely about visibility into a unified customer/order view, closed by the shared Customer Domain service. |
| API/integration governance | 1 | 5 | 4 | No integration inventory or governance today (per P-10); target is full API-gateway-mediated governance. |
| Data governance (customer/product/order domains) | 2 | 4 | 2 | Some data governance exists for financial data (regulatory driven); none for product/customer/order until this program. |
| Security & access control across shared data | 2 | 5 | 3 | Today access control is per-system; target is unified RBAC across the shared data layer per P-06. |
| Vendor/partner product interoperability | 1 | 3 | 2 | No Open API exposure today; target reaches basic external partner exposure, with full partner ecosystem maturity a candidate for a follow-on program. |
| Organizational change readiness (staff process/tooling) | 2 | 4 | 2 | Addressed directly by the Phase H change management plan, not a byproduct of the technical rollout. |

## Reading the Map

Two things stand out and directly explain this program's priorities. First, **Product Catalog Management carries the single largest gap (4 points)** — this is the capability most directly responsible for the "no converged bundles" business problem, and it is why Phase E's vendor evaluation and solution building blocks treat catalog platform selection as the highest-stakes single decision in the program (see ADR-002). Second, **Billing & charging (financial ledger) is intentionally left at its current maturity of 4** — it is already a well-run capability, and the architecture strategy (ADR-001) is designed specifically so that this program does not need to touch it to succeed. A capability map that showed billing needing uplift would suggest a different, riskier strategy than the one this program has chosen.

Order Orchestration and 5G-Slice Product Management are deliberately targeted at 4, not 5 — both retain a defined manual exception path or defer full optimization to a follow-on program, consistent with the incremental modernization principle (P-03) and the explicit non-goal of eliminating all manual handling in the first 18 months (P-09 targets ≤20% manual handling, not zero).

---

*Fictional case study — see [README](../README.md) for full disclaimer.*
