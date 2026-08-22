# Governance Framework Setup

**Phase:** Preliminary
**Purpose:** Establish the Architecture Review Board (ARB) and the governance mechanisms that keep the BSS/OSS modernization program aligned to the principles in `architecture-principles.md` for the life of the program.

## Why Governance Is Established Before Phase A

TOGAF's Preliminary Phase exists to answer "how will we govern architecture work here?" before any scoping begins, and Brenmark's context makes that sequencing non-optional rather than procedural. Three systems (billing, CRM, order management) currently evolve independently, each with its own change process and none with visibility into the others' roadmaps — which is a root cause of the fragmentation this program exists to fix. Standing up a single governance body first prevents the modernization program from recreating the same fragmentation with new technology.

## Architecture Review Board (ARB) — Constitution

**Chartered by:** Brenmark CTO, on the mandate of the CEO and Board Technology Committee.

**Standing membership:**

| Role | Represents | Voting? |
|---|---|---|
| Chief Enterprise Architect (Chair) | EA function | Yes |
| VP Billing & Revenue Systems | Billing domain | Yes |
| VP Customer Operations | CRM / customer service domain | Yes |
| VP Network Engineering | Network inventory / OSS domain | Yes |
| Head of InfoSec | Security & compliance | Yes |
| Head of Data & Analytics | Enterprise data domain | Yes |
| Program Director, BSS/OSS Modernization | Delivery | Non-voting (advisory) |
| Procurement/Vendor Management Lead | Commercial | Non-voting (advisory) |
| Rotating: Solution Architects presenting a contract | Delivery teams | Non-voting for own submission |

Quorum is five of six voting members, and the Chief Enterprise Architect holds tie-breaking authority. Non-voting advisory members attend every session and their input is recorded in minutes, but only the six standing roles above cast binding votes — this keeps decision accountability with the business and security leaders who own the domains affected, while giving delivery and procurement a direct channel to raise concerns without slowing decisions.

## Cadence

- **Standing ARB session:** bi-weekly, 90 minutes, fixed calendar slot for the duration of the program.
- **Architecture contract review:** any solution architect may request a slot to present a contract for sign-off (see `07-phase-g-implementation-governance/architecture-contracts.md`); requests are triaged within 5 business days.
- **Principle exception requests:** reviewed at the next standing session, or within 3 business days via written ballot if the requesting team is blocked and cannot wait for the next session.
- **Quarterly architecture health review:** a full review of gap-analysis progress, principle-compliance findings, and roadmap variance against the Phase F roadmap, presented to the CTO and Board Technology Committee.

## Escalation Path

1. **Solution-architect level:** disagreements on implementation detail within an approved contract are resolved between the solution architect and the assigned EA reviewer.
2. **ARB level:** disagreements on architecture direction, principle interpretation, or contract approval are brought to the standing ARB session. A simple majority of voting members decides.
3. **CTO level:** a voting member may escalate an ARB decision to the CTO if they believe it materially conflicts with business strategy or risk appetite. The CTO's decision is final for operational matters.
4. **Board Technology Committee:** reserved for decisions with material capital commitment (see business case thresholds in `01-phase-a-vision-and-scope/business-case.md`) or decisions that would change the program's 18-month commitment to the board. This escalation path is used rarely — by design, escalating past the CTO is itself a signal the decision under dispute is program-defining rather than routine.

## Principles Enforcement

- Every architecture contract (Phase G) must cite which principles (P-01 through P-12) it satisfies and disclose any principle it deviates from, with justification.
- Non-compliance findings are logged in the program's compliance register (owned by the EA function) and categorized as **Advisory**, **Must-Fix-Before-Production**, or **Blocking**, per the process in `07-phase-g-implementation-governance/governance-framework.md`.
- Principle exceptions are time-boxed: an approved exception carries an expiry date and must be re-justified at renewal, not granted permanently by default. This prevents "temporary" exceptions from becoming silent permanent architecture debt — a failure mode common enough in large modernization programs that ARB treats an expired, unrenewed exception as an automatic Blocking finding.
- Any exception affecting P-01 (data ownership) or P-06 (security/privacy) requires unanimous voting-member approval, not simple majority, reflecting the higher cost of getting these two wrong.

## Governance Artifacts Maintained by the EA Function

- The architecture principles register (`00-preliminary/architecture-principles.md`)
- The compliance/exception register (referenced from Phase G)
- The integration inventory (per P-10), reviewed at each quarterly health review
- ARB meeting minutes and decision log, retained for the life of the program plus 2 years for audit purposes

---

*Fictional case study — see [README](../README.md) for full disclaimer.*
