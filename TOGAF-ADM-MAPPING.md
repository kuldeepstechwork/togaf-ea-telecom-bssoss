# TOGAF ADM Phase Mapping

This table maps each phase of the TOGAF Architecture Development Method (ADM) to the folder in this repository containing its artifacts, for the Brenmark Telecom BSS/OSS modernization program.

| ADM Phase | Folder | Contents |
|---|---|---|
| **Preliminary** | [`00-preliminary/`](./00-preliminary/) | Architecture principles (8–12, TOGAF format) and how the Architecture Review Board (ARB) is constituted, meets, and enforces those principles. |
| **Phase A — Architecture Vision** | [`01-phase-a-vision-and-scope/`](./01-phase-a-vision-and-scope/) | Problem statement, target-state vision, explicit in/out-of-scope boundaries, stakeholder map with RACI, the business case with full cost/ROI math, and a CxO-level executive summary. |
| **Phase B — Business Architecture** | [`02-phase-b-business-architecture/`](./02-phase-b-business-architecture/) | As-is and to-be business process/capability narratives (each with a Mermaid diagram), and a capability map with 1–5 maturity ratings (as-is vs. target). |
| **Phase C — Information Systems Architecture** | [`03-phase-c-information-systems-architecture/`](./03-phase-c-information-systems-architecture/) | Data architecture (customer, product catalog, order, network inventory domains) and application architecture (as-is application landscape vs. to-be ODA-aligned landscape), each with integration-pattern narrative and a Mermaid diagram. |
| **Phase D — Technology Architecture** | [`04-phase-d-technology-architecture/`](./04-phase-d-technology-architecture/) | The strangler-fig / TM Forum Open API gateway reference architecture (with an explicit "when NOT to use this pattern" section) and the approved technology standards catalog with an exceptions process. |
| **Phase E — Opportunities & Solutions** | [`05-phase-e-opportunities-and-solutions/`](./05-phase-e-opportunities-and-solutions/) | Decomposition of required capabilities into solution building blocks, a weighted vendor evaluation across four platform vendors, and a prioritized as-is-to-to-be gap analysis. |
| **Phase F — Migration Planning** | [`06-phase-f-migration-planning/`](./06-phase-f-migration-planning/) | The phased migration roadmap (Mermaid Gantt chart across waves/quarters) and named transition architectures describing intermediate states between as-is and to-be. |
| **Phase G — Implementation Governance** | [`07-phase-g-implementation-governance/`](./07-phase-g-implementation-governance/) | Implementation governance process (compliance checkpoints, non-compliance handling) and the architecture contract template/example used between the EA function and delivery teams. |
| **Phase H — Architecture Change Management** | [`08-phase-h-change-management/`](./08-phase-h-change-management/) | Organizational change impact assessment, training plan, communications plan, and adoption metrics for the modernization program. |
| **Requirements Management** (cross-cutting) | Embedded throughout Phases A–H | TOGAF's central Requirements Management activity is not a standalone folder; requirements are captured and traced within the Vision & Scope and Gap Analysis documents, and revisited at each ARB checkpoint per `07-phase-g-implementation-governance/governance-framework.md`. |
| **Decision Records** (cross-cutting) | [`adrs/`](./adrs/) | Five Architecture Decision Records covering the program's most consequential and hardest-to-reverse choices, referenced from the phase documents where each decision is first introduced. |

---

*Fictional case study — see [README](./README.md) for full disclaimer.*
