# Architecture Contracts

**Phase:** G — Implementation Governance

## What an Architecture Contract Is

An architecture contract is the formal agreement between the EA function (representing the ARB) and a delivery team, establishing what the team is building, which architecture principles and standards it must conform to, what non-functional targets are binding acceptance criteria, and what happens if either side fails to hold up their end. It is issued at the Contract Sign-Off checkpoint (`governance-framework.md`) and referenced at every subsequent checkpoint through go-live.

Per TOGAF's ADM guidance, an architecture contract is bidirectional: it binds the delivery team to conform to the architecture, but it equally binds the EA function to provide a stable, sufficiently-specified architecture and timely review turnaround — a contract is not a one-way compliance stick, and treating it as one is a fast way to make delivery teams route around governance instead of through it.

## Standard Contract Contents

1. **Scope statement** — which solution building block(s) this contract covers, and explicit non-goals.
2. **Principles cited** — which of the 12 architecture principles this build must conform to, with a statement of how (not just a list of numbers).
3. **Standards cited** — which technology standards apply (from `04-phase-d-technology-architecture/technology-standards.md`).
4. **Disclosed exceptions** — any approved deviations, with expiry dates, referenced explicitly rather than left implicit.
5. **Non-functional acceptance criteria** — binding, measurable targets (per P-11), with the measurement method stated.
6. **Interfaces/dependencies** — what this build consumes and what it exposes, referencing the integration inventory (P-10).
7. **EA function commitments** — review turnaround times, named reviewer, escalation path if the team is blocked awaiting a decision.
8. **Checkpoint schedule** — dates or milestones for Design Conformance Review, Pre-Production Readiness Review, and Post-Go-Live Health Check.
9. **Sign-off** — named accountable individuals on both sides (delivery lead and EA reviewer), dated.

## Worked Example: Order Orchestration Platform — Standard Order Flow (Wave 2)

**1. Scope statement:** This contract covers the Order Orchestration Platform's standard single-domain order-to-activation flow (mobile and broadband, non-bundled) as deployed in Wave 2. Converged-bundle orchestration and 5G-slice orchestration are explicitly out of scope for this contract and are covered by a separate Wave 3 contract.

**2. Principles cited:**
- **P-02** (Open API standards): all order submission and status-callback interfaces must conform to the TM Forum Open API product-ordering pattern.
- **P-09** (automate provisioning by default): standard configurations must complete order-to-activation without human intervention; the exception path is a named, separately-tested flow, not a fallback used by default.
- **P-11** (binding NFRs): see acceptance criteria below.

**3. Standards cited:** API Gateway routing (all traffic through the gateway, no direct calls to Network Inventory or Billing adapters); centralized RBAC for any operator-facing exception-handling UI; centralized logging/tracing for every order transaction.

**4. Disclosed exceptions:** One active exception — the Network Inventory activation-confirmation callback uses a legacy SOAP interface pending the vendor's committed REST delivery date (expires 9 months from this contract's sign-off; see `04-phase-d-technology-architecture/technology-standards.md` for the full exception record).

**5. Non-functional acceptance criteria:**
- Standard order-to-activation completion time: ≤ 15 minutes for 95% of orders, measured end-to-end from order submission to activation-confirmed status.
- Order Orchestration Platform availability: ≥ 99.9% measured monthly.
- Manual exception-path invocation rate: ≤ 20% of total standard-eligible order volume, measured monthly and trending down release over release (per the Phase A success metric).

**6. Interfaces/dependencies:** Consumes: Product Catalog Platform (product/pricing lookup), Customer Domain Service (customer identity), Legacy Billing Adapter (charge instruction), Legacy Network Inventory Adapter (activation request/confirmation). Exposes: order-status API (consumed by CRM and Customer Operations dashboards). All five interfaces are registered in the integration inventory prior to Design Conformance Review.

**7. EA function commitments:** Design Conformance Review turnaround within 5 business days of submission; a named EA reviewer assigned for the life of this contract; any ARB exception request raised by this team is triaged within 3 business days per the governance framework's blocked-team provision.

**8. Checkpoint schedule:** Design Conformance Review — month 8; Pre-Production Readiness Review — month 11; Post-Go-Live Health Check — month 12.5 (30 days after targeted month-11.5 go-live).

**9. Sign-off:** Delivery Lead, Order Orchestration workstream (Responsible per Phase A RACI); EA Reviewer, assigned by Chief Enterprise Architect. Both parties dated sign-off recorded in the compliance register at contract issuance.

## What Happens When a Contract's Terms Are Missed

If Pre-Production Readiness Review finds the ≤15-minute/95th-percentile target unmet, this is a **Must-Fix-Before-Production** finding (per `governance-framework.md`) — the team remediates and re-presents rather than proceeding to go-live with an unmet binding NFR. If the manual exception-path rate exceeds 20% *after* go-live at the Post-Go-Live Health Check, this is reported to the ARB as a health-check finding requiring a remediation plan, but does not retroactively block a go-live that already passed its Pre-Production Review — the two checkpoints exist precisely to catch problems at the earliest checkpoint capable of catching them, not to re-litigate a prior pass.

---

*Fictional case study — see [README](../README.md) for full disclaimer.*
