# Technology Standards

**Phase:** D — Technology Architecture

## Purpose

This document defines the approved technology stack and standards for the BSS/OSS modernization program, and the process by which a delivery team may request an exception. Standards exist to enforce the architecture principles (`00-preliminary/architecture-principles.md`) consistently across every solution building block, not as arbitrary tooling preference.

## Approved Standards

| Area | Standard | Enforces |
|---|---|---|
| Integration contract | TM Forum Open API family (product-ordering, product-catalog, customer-management, and resource-inventory API patterns) | P-02 |
| API transport | REST/JSON over HTTPS for synchronous calls; event-driven pub/sub for asynchronous state propagation | P-02, P-10 |
| API gateway | Centralized gateway enforcing schema validation, auth, and rate limiting for all cross-system traffic | P-10 |
| Identity & access | Centralized RBAC provider; no application-local user/role store for new components | P-06 |
| Data classification | Every new data entity tagged at creation with a classification (Public / Internal / Confidential / Restricted-PII) | P-06 |
| Reference framework | TM Forum Open Digital Architecture (ODA) functional decomposition for all new components | P-05, P-07 |
| Environment/deployment | Container-based deployment with environment parity (dev/test/staging/prod) for all new components | P-11 (supports NFR testability) |
| Observability | Centralized logging, tracing, and metrics for every gateway-routed transaction | P-04, P-11 (supports reversibility and NFR verification) |
| Documentation | Every registered integration carries an OpenAPI/TM Forum schema definition in the integration inventory | P-10 |

## Explicit Non-Standards (Deprecated Going Forward)

- New point-to-point integrations bypassing the API gateway are non-compliant by default (violates P-10) unless an approved exception exists.
- New application-local customer or product data stores that duplicate the Customer Domain or Product Catalog systems of record are non-compliant (violates P-01) without an approved exception.
- Batch file-based nightly integration patterns (the as-is CRM–Billing sync method) are not approved for any new integration; existing batch integrations are grandfathered only until their replacement is scheduled in the Phase F roadmap.

## Exceptions Process

No standard in this document is presented as absolute in every conceivable circumstance — the exceptions process exists precisely because real delivery constraints sometimes justify a deviation, and pretending otherwise would just push non-compliant work underground rather than through governance.

1. **Request submission:** A solution architect submits a written exception request to the ARB, citing the specific standard, the reason compliance isn't feasible or isn't the right call for this case, the proposed alternative, and a proposed expiry date.
2. **Review:** Reviewed at the next standing ARB session (bi-weekly) or via written ballot within 3 business days if the requesting team is blocked (per the escalation cadence in `00-preliminary/governance-framework-setup.md`).
3. **Approval threshold:** Simple majority of voting ARB members, **except** exceptions touching P-01 (data ownership) or P-06 (security/privacy), which require unanimous voting-member approval.
4. **Time-boxing:** Every approved exception carries a mandatory expiry date. An exception with no renewal request logged before its expiry automatically becomes a Blocking non-compliance finding under Phase G governance — it does not silently continue.
5. **Renewal:** Renewal requires re-justification, not automatic rollover; the requesting team must show why the underlying constraint that justified the exception still holds.
6. **Register:** All exceptions, approved or rejected, are logged in the compliance/exception register maintained by the EA function, with the deciding ARB session's minutes attached for traceability.

## Example Exception (Illustrative)

An exception was granted early in the program for the Network Inventory system's activation-confirmation callback, which could only be delivered via a legacy SOAP interface rather than the standard REST/JSON pattern, because the network inventory vendor's committed REST API delivery date fell outside the program's first migration wave. The exception was approved by simple majority (not touching P-01/P-06), with an 9-month expiry tied to the vendor's committed REST delivery date, and a requirement that the SOAP traffic still route through the API gateway (satisfying P-10) even though its payload format was non-standard. This illustrates the exceptions process working as intended: a real constraint, a bounded and justified deviation, and a concrete renewal/expiry condition rather than an indefinite carve-out.

---

*Fictional case study — see [README](../README.md) for full disclaimer.*
