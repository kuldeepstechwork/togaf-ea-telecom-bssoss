# Architecture Vision & Scope

**Phase:** A — Architecture Vision

## Problem Statement

Brenmark Telecom serves approximately 6 million subscribers across mobile and fixed broadband, on a BSS/OSS estate that grew organically over roughly two decades: a monolithic billing system as the financial system of record, a CRM system that maintains its own separate customer record, and a network inventory/order management system that requires manual, department-to-department handoffs to provision service. None of the three shares a common product catalog or a common customer/order data model.

The consequence is threefold, and each consequence maps to a specific commercial deadline the business is exposed to:

1. **No converged bundles.** Brenmark cannot sell a single product that combines mobile, broadband, and (in future) a 5G network slice, because no system can express such a product across all three domains simultaneously. Competitors offering converged bundles are winning share in the segments Brenmark's product team has flagged as highest-growth.
2. **Multi-day provisioning.** A new service order requires manual coordination between CRM, billing, and network operations staff, typically taking 3–7 business days from order to activation. This is both a customer-experience liability and a direct cost (see business case) in manual labor.
3. **No path to 5G-slice monetization.** The Board has mandated that Brenmark be able to monetize 5G network slicing — selling differentiated network capacity/SLA as a product — within 18 months. The current OSS has no data model, orchestration integration, or billing construct capable of representing a network slice as a sellable, billable, orderable product.

## Target State Vision

Within 18 months, Brenmark will operate a BSS/OSS architecture in which:

- A single, authoritative **product catalog** (TM Forum Open API–aligned) can describe any sellable product — including mobile, broadband, and 5G network slices, individually or bundled — and every sales channel consumes that same catalog.
- **Order-to-activation for standard product configurations is automated end-to-end**, reducing the default provisioning path from days to minutes; manual handoff becomes the exception path for non-standard orders, not the default for all orders.
- **5G network slices are orderable, billable products** from the same catalog and order-management flow as any other product, with orchestration integration to the network layer capable of instantiating and metering a slice.
- The legacy billing system remains the system of record for financial transactions and continues operating without a disruptive cutover, reached via a governed API layer rather than direct, bespoke integrations from every consuming system.

This vision is deliberately an evolution of the existing billing estate, not a replacement of it — see `06-phase-f-migration-planning/migration-roadmap.md` and ADR-001 for why.

## Scope Boundaries

### In Scope

- Product catalog consolidation into a single TM Forum Open API–aligned system of record (Phase C, Phase E).
- Order management and provisioning orchestration redesign for automated order-to-activation.
- Customer/order/product data architecture: entity models, systems of record, integration patterns.
- A TM Forum Open API gateway/strangler layer in front of the legacy billing, CRM, and network inventory systems.
- Network-slice orchestration integration sufficient to support ordering, activation, and usage-based billing of a 5G slice as a product.
- Vendor selection for the new product catalog and order orchestration layer.
- Organizational change management for CRM, billing operations, and network operations staff whose workflows change.

### Explicitly Out of Scope (and Why)

| Out of scope | Why |
|---|---|
| **Replacing the core billing engine's financial ledger/rating logic** | The billing engine's rating and financial-ledger functions are stable, regulator-audited, and not the source of the bundling/provisioning problem. Replacing them adds multi-year risk for no benefit to the 18-month mandate — this is the central premise behind the strangler-fig decision in ADR-001. |
| **Retail/physical store point-of-sale hardware refresh** | A hardware refresh is a separate capital program with its own business case; it doesn't block converged-product launch or slice monetization. |
| **Network core / RAN 5G build-out** | This program integrates with network orchestration to *sell and meter* a slice; it does not design or fund the underlying 5G radio/core network build-out, which is a Network Engineering capital program running in parallel. |
| **CRM replacement** | The CRM's *sales and case-management* functions are adequate; only its lack of a shared customer/order view is in scope, and that gap is closed via the shared data architecture (Phase C), not a CRM replacement. |
| **International/roaming billing overhaul** | Out of scope for this program's 18-month horizon; flagged as a candidate for a follow-on program once the domestic converged-bundle capability is proven. |
| **Full decommissioning of the legacy order-management system** | Full decommissioning is a multi-year outcome that depends on this program's success; this program builds the strangler layer and migrates capability incrementally, but does not commit to a legacy shutdown date within the 18-month window (see Phase F transition architectures). |

## Success Metrics

| Metric | Baseline (as-is) | Target (18 months) |
|---|---|---|
| Time to launch a new converged bundle product | Not currently possible | ≤ 4 weeks from product definition to market availability |
| Standard order provisioning time (order to activation) | 3–7 business days | ≤ 15 minutes for standard configurations |
| Manual handoff rate for standard orders | ~100% | ≤ 20% (exception path only) |
| 5G network slice: order-to-activation capability | Not supported | Supported, with usage-based billing |
| Product catalog systems of record | 3 (billing, CRM, order mgmt, each partial) | 1 (authoritative, Open API–exposed) |
| Point-to-point undocumented integrations (per integration inventory) | Baseline TBD at Phase C completion | Reduced ≥ 60% vs. Phase C baseline, remainder routed through API gateway |

---

*Fictional case study — see [README](../README.md) for full disclaimer.*
