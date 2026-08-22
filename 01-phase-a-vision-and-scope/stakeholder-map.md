# Stakeholder Map

**Phase:** A — Architecture Vision

Stakeholder analysis for the BSS/OSS modernization program, capturing each stakeholder's primary concerns and their RACI role across the program's major decision categories. This map is reviewed and refreshed at each quarterly architecture health review (see `00-preliminary/governance-framework-setup.md`).

## Stakeholder Concerns

| Stakeholder | Primary Concern |
|---|---|
| **CEO / Board Technology Committee** | Meeting the 18-month 5G-slicing mandate; program cost vs. board-approved budget; reputational/competitive risk of a stalled or failed modernization. |
| **CTO** | Technical feasibility of the 18-month timeline; overall program risk; alignment with broader technology strategy beyond BSS/OSS. |
| **VP Billing & Revenue Systems** | Zero disruption to real-time charging and revenue assurance; regulatory audit continuity; the billing system remaining system of record for financial data. |
| **VP Customer Operations** | Customer service staff's ability to see one customer view across mobile/broadband/slice products; call-handling time; case-management continuity during transition. |
| **VP Network Engineering** | Network inventory accuracy; orchestration integration not destabilizing existing provisioning for current products; network-slice orchestration readiness on the network side. |
| **Head of InfoSec** | Data privacy/PII handling for the new shared customer and location-adjacent (slice usage) data; access control across a newly shared data layer; audit trail. |
| **Head of Data & Analytics** | Data quality and governance of the new authoritative product/customer/order domains; avoiding a new generation of shadow copies. |
| **Head of Product / Commercial** | Speed to market for converged bundles; catalog flexibility for future product innovation; competitive positioning. |
| **Procurement / Vendor Management** | Vendor commercial terms, contract exit costs, avoidance of lock-in inconsistent with P-04. |
| **Program Director, BSS/OSS Modernization** | Delivery feasibility of the roadmap; resourcing; cross-team dependency management. |
| **Solution Architects / Delivery Teams** | Clear, stable architecture contracts; realistic non-functional targets; tooling and platform readiness. |
| **Frontline CRM / Billing / Network Ops Staff** | Job impact of new workflows; adequacy of training; system usability during transition (see Phase H). |
| **Regulatory / Compliance Function** | Continued compliance with telecom billing regulation and data protection obligations through and after the transition. |
| **External Customers (represented via Product/Commercial)** | Faster provisioning; new converged product availability; no billing errors or service disruption during transition. |

## RACI — Program-Level Decision Categories

R = Responsible, A = Accountable, C = Consulted, I = Informed

| Decision Category | CEO/Board | CTO | VP Billing | VP Cust. Ops | VP Network Eng. | Head InfoSec | Head Data & Analytics | Program Director | ARB (Chief EA) |
|---|---|---|---|---|---|---|---|---|---|
| Program charter & budget approval | A | R | C | C | C | I | I | C | C |
| Architecture principles & scope (Phase A) | I | A | C | C | C | C | C | C | R |
| Business/data/application architecture (Phase B/C) | I | I | C | C | C | C | R | I | A |
| Technology standards & reference architecture (Phase D) | I | C | I | I | I | C | I | I | A/R |
| Vendor selection (Phase E) | I | A | C | C | C | C | I | R | C |
| Migration roadmap & sequencing (Phase F) | I | A | R | C | C | I | I | R | C |
| Architecture contract sign-off (Phase G) | I | I | I | I | I | C | I | I | A |
| Principle exception approval | I | I | C | C | C | C (P-06 veto) | C | I | A |
| Organizational change plan (Phase H) | I | I | C | R | C | I | I | A | C |
| Go-live / cutover decision per wave | I | A | R | C | R | C | I | R | C |

## Notes on RACI Interpretation

- **CTO is Accountable, not Responsible,** for most program-level decisions — the CTO owns the outcome to the Board but delegates execution and detailed judgment to the ARB (chaired by the Chief Enterprise Architect) and the Program Director, consistent with the governance structure in `00-preliminary/governance-framework-setup.md`.
- **Head of InfoSec holds an explicit veto-consulted role** on any decision touching P-01 (data ownership) or P-06 (security/privacy) exceptions — reflected as "C (P-06 veto)" above — because those two principles require unanimous ARB approval to override, not simple majority.
- **VP Billing & Revenue Systems is Responsible for go-live decisions** because the billing system carries the highest business-continuity risk of any component in scope; no wave goes live without their sign-off regardless of ARB approval.
- Frontline staff and external customers are not board-level decision stakeholders but are represented through VP Customer Operations and Head of Product/Commercial respectively, and are directly engaged through the communications and training activities in Phase H.

---

*Fictional case study — see [README](../README.md) for full disclaimer.*
