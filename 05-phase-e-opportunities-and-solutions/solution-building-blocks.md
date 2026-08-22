# Solution Building Blocks

**Phase:** E — Opportunities & Solutions

## Purpose

This document decomposes the required capabilities identified in Phase B (capability map) and Phase C (application architecture) into discrete Solution Building Blocks (SBBs) — the buildable-or-buyable units the program actually procures or engineers. Each SBB is evaluated against the buy-vs-build principle (P-05): buy commodity capability, build only genuine differentiation.

## Solution Building Block Decomposition

| Solution Building Block | Realizes Capability (Phase B) | Buy or Build | Rationale |
|---|---|---|---|
| **API Gateway / Strangler Layer** | API/integration governance | Buy (commercial API management platform) + configure | Commodity capability; mature vendor products exist; no competitive differentiation in building a gateway in-house. |
| **Product Catalog Platform** | Product catalog management | Buy (vendor platform) + build (Brenmark-specific bundle/pricing rules configuration) | Core engine is commodity; converged-bundle and slice pricing logic is where Brenmark's commercial differentiation lives, so that layer is configured/extended, not left as vendor default. |
| **Order Orchestration Platform** | Order orchestration/fulfillment | Buy (vendor platform) + build (Brenmark-specific fulfillment workflow for slice activation) | Same buy/build split logic as catalog: orchestration engine is commodity, the specific cross-domain workflow logic for Brenmark's three domains is configured. |
| **Customer Domain Service** | Customer identity & 360 view | Build (thin service) on top of buy (identity/master-data-management tooling where applicable) | Brenmark's specific customer-record reconciliation logic (merging CRM and Billing partial records) is idiosyncratic enough that a thin purpose-built service was judged lower-risk than forcing it into a generic MDM product's data model — see Gap Analysis for the rejected alternative. |
| **Network-Slice Orchestration Adapter** | 5G network-slice product management | Build | No commodity product in Brenmark's evaluated vendor set adequately covers slice orchestration integration specific to Brenmark's network equipment vendor mix; this is treated as a genuine build, coordinated with Network Engineering's parallel 5G capital program. |
| **Dual-Write Reconciliation Service** | Data governance (transitional) | Build | Bespoke by necessity — reconciliation logic must match Brenmark's specific legacy billing schema; no vendor product addresses this transitional need generically. |
| **Legacy Billing Adapter (API-fronting)** | Application architecture (financial ledger integration) | Build (thin adapter) | Thin translation layer exposing the legacy billing engine's existing capabilities as Open API-conformant endpoints; not a rebuild of billing logic itself. |
| **Legacy Network Inventory Adapter** | Network provisioning integration | Build (thin adapter) | Same pattern as the billing adapter — thin API-fronting layer, not a network inventory replacement. |
| **RBAC / Access Control Uplift** | Security & access control | Buy (existing enterprise identity provider, extended) | Brenmark already operates an enterprise identity provider for other systems; extending it is lower-risk and lower-cost than a new access-control build. |

## How SBBs Map to Architecture Contracts

Each SBB above becomes the basis for one or more architecture contracts (Phase G) once a delivery team is assigned. The Product Catalog Platform and Order Orchestration Platform SBBs are the two with vendor selection decisions attached — see `vendor-evaluation.md`. The four "build" or "thin adapter" SBBs (Customer Domain Service, Network-Slice Orchestration Adapter, Dual-Write Reconciliation Service, Legacy Adapters) are engineered in-house by Brenmark delivery teams under EA-issued contracts, without a vendor evaluation step, because Phase E's gap analysis found no vendor product addressing these needs at acceptable cost/risk (see `gap-analysis.md`).

## Sequencing Dependency Note

The Legacy Billing Adapter and Legacy Network Inventory Adapter SBBs are prerequisite building blocks for nearly every other SBB in this list — the Product Catalog and Order Orchestration platforms cannot be meaningfully tested end-to-end until they can reach billing and network inventory through a stable adapter contract. This dependency directly shapes the wave sequencing in `06-phase-f-migration-planning/migration-roadmap.md`, where the adapters are built in Wave 1 ahead of the platforms that depend on them.

---

*Fictional case study — see [README](../README.md) for full disclaimer.*
