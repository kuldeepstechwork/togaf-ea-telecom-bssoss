# Change Management Plan

**Phase:** H — Architecture Change Management

## Why This Is a First-Class Program Workstream

Per architecture principle P-12, organizational change is planned and resourced as explicitly as the technical migration, not treated as an automatic by-product of it. The BSS/OSS modernization program changes how three distinct staff populations do their jobs — Customer Operations (CRM/case management), Billing Operations, and Network Operations — and it does so unevenly across the roadmap's waves, which creates a specific risk: long quiet periods (see Transition Architecture 1 in Phase F) followed by sudden, concentrated workflow change (Wave 3's bundle/slice launch). A change plan that doesn't account for that rhythm risks staff experiencing the change as abrupt and poorly communicated, regardless of how well the technical migration itself goes.

## Organizational Change Impact

| Staff Population | Current Workflow | New Workflow | Impact Level |
|---|---|---|---|
| Customer Operations (CSRs) | Manually re-key orders between CRM and Billing; rely on undocumented tenured-staff knowledge for product-code translation | Capture orders directly against unified Product Catalog; system handles cross-domain decomposition | High — role shifts from manual translator to order-exception handler and customer-experience owner |
| Billing Operations | Manually update billing upon receiving network confirmation via email/ticket | Billing account setup triggered automatically via API; billing ops shifts to monitoring reconciliation-lag alerts (per ADR-004) and exception handling | High — role shifts from manual processor to exception/anomaly monitor |
| Network Operations | Receive manual work-order tickets; manually check capacity and schedule provisioning | Standard configurations auto-provision via API; network ops handles only non-standard/exception orders and capacity planning | Medium-High — reduces routine ticket volume substantially, shifts focus to exceptions and capacity management |
| Customer Operations Management | Manage staff performing manual coordination work | Manage staff performing exception-handling and customer-experience work; new reporting metrics (exception rate, resolution time) replace old ones (manual processing volume) | Medium — management KPIs and staffing model need updating alongside frontline workflow |

## Training Plan

Training is sequenced to the migration roadmap, not delivered all at once:

- **Pre-Wave 1 (month 2):** Awareness-level briefing for all affected staff populations — what's changing, why, and the overall timeline. No workflow training yet, since no new workflow exists yet at this point.
- **Wave 2 lead-up (months 9–11):** Hands-on training for Customer Operations and Billing Operations on the standard-order automated flow, using the Order Orchestration Platform's staging environment, ahead of Wave 2 go-live.
- **Wave 3 lead-up (months 13–15):** Targeted training for Customer Operations and Network Operations on converged-bundle sales workflows and slice-product handling, including new exception-path procedures specific to bundles.
- **Ongoing:** A living knowledge base replaces the previously undocumented, tenured-staff-held product-code translation knowledge identified as a risk in the as-is business architecture — this is treated as a direct risk-mitigation outcome of the program, not just a training-logistics artifact.

## Communications Plan

| Audience | Channel | Cadence | Content |
|---|---|---|---|
| All affected frontline staff | Town halls + team briefings | Start of each wave | What's changing this wave, what's not changing yet, where to raise concerns |
| Frontline staff during quiet/infrastructure waves (e.g., Transition Architecture 1) | Short written updates from workstream leads | Monthly | Explicit reassurance that the program is progressing even though no visible workflow change has occurred yet — directly addressing the "silent progress" risk flagged in `06-phase-f-migration-planning/transition-architectures.md` |
| Customer Operations management | Dedicated briefing | Each checkpoint (Phase G) | Staffing/KPI implications of upcoming changes, ahead of go-live, not after |
| Executive leadership | Quarterly architecture health review (existing forum) | Quarterly | Change-readiness metrics alongside technical progress, so change management is visibly part of program health, not a separate afterthought report |
| External customers | Product/Commercial-led marketing and service communications | At Wave 3 launch | New converged bundle and slice product availability — this is a commercial, not change-management, communication, but timed against the same roadmap |

## Adoption Metrics

| Metric | Baseline | Target (by end of Wave 4) |
|---|---|---|
| Manual exception-path invocation rate (standard orders) | 100% (as-is) | ≤ 20% (per Phase A success metric and the Wave 2 architecture contract's NFR target) |
| Staff-reported confidence in new workflow (post-training survey) | N/A (new metric) | ≥ 75% "confident" or "very confident" |
| Knowledge-base usage (queries/month) as a proxy for reduced dependency on undocumented tenured-staff knowledge | N/A (new metric) | Sustained usage, tracked as a leading indicator rather than a single target — a very low usage rate could indicate either full workflow confidence or knowledge-base inadequacy, so this metric is reviewed qualitatively alongside the confidence survey, not in isolation |
| Customer Operations attrition rate during transition | Current baseline attrition rate | No statistically significant increase attributable to the program (tracked jointly with HR) |
| Time from go-live to staff proficiency (per wave) | N/A (new metric) | ≤ 4 weeks to reach steady-state handling times for the new workflow |

## Ownership

Per the Phase A RACI, VP Customer Operations is Responsible for this plan's execution, with the Program Director Accountable for its integration into the overall roadmap. Progress against adoption metrics is reported at the quarterly architecture health review alongside technical and financial program health, ensuring change management is never treated as a separate, lower-priority track from the technical migration.

---

*Fictional case study — see [README](../README.md) for full disclaimer.*
