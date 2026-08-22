# Business Case

**Phase:** A — Architecture Vision
**Note:** All figures in this document are invented for the purposes of this fictional case study and are illustrative only. They are constructed to be internally consistent and plausible for a ~6M-subscriber operator, not to represent real financial data.

## Summary

The modernization program requires an estimated **$18.4M** in capital investment over 18 months, plus an estimated **15% ongoing operational overhead** on affected systems during a ~24-month dual-write transition period (see ADR-004). Against this, the program is projected to deliver **$50.7M** in combined cost-avoidance ($27.4M — already net of the capex and transition opex above, since both are included in the To-Be cost totals used to compute it) and new-revenue benefit ($23.3M) over a 3-year horizon, for a **net 3-year benefit of approximately $50.7M relative to as-is** and a **payback period of approximately 22 months** from program start. The largest single benefit driver is new converged-bundle and 5G-slice revenue, not cost savings — this is a growth investment, not primarily a cost-reduction program.

## Capex/Opex Line Items

| Line Item | Type | Estimate | Basis |
|---|---|---|---|
| TM Forum Open API gateway/strangler layer — build | Capex | $4.6M | 230 person-months blended engineering effort @ $20K/person-month (architecture, integration, API, QA roles blended) |
| Product catalog platform — license + implementation | Capex | $3.8M | Vendor license (see `05-phase-e-opportunities-and-solutions/vendor-evaluation.md`) + 90 person-months implementation |
| Order orchestration platform — license + implementation | Capex | $3.2M | Vendor license + 70 person-months implementation |
| Network-slice orchestration integration | Capex | $2.1M | 105 person-months, includes network-side interface work coordinated with Network Engineering's parallel 5G capital program |
| Data migration & reconciliation tooling | Capex | $1.4M | 70 person-months; supports the dual-write reconciliation strategy in ADR-004 |
| Security/access-control uplift (P-06) | Capex | $0.9M | 45 person-months, PII classification and access control redesign for shared data layer |
| Program management, ARB operation, architecture governance overhead | Capex | $1.3M | 18 months at a blended governance/PM run rate |
| Training & change management (Phase H) | Capex | $1.1M | Included below and cross-referenced in `08-phase-h-change-management/change-management-plan.md` |
| **Total Capex** | | **$18.4M** | |
| Dual-write/reconciliation operational overhead | Opex (recurring, 24 months) | $2.6M/yr (≈ $5.2M over 24 months) | Estimated 15% overhead on affected billing/CRM/order-management run costs (~$17.3M/yr baseline run cost × 15%) during transition, per ADR-004 |
| Steady-state platform run cost (post-transition), net of legacy decommission savings | Opex (ongoing, from month 25) | −$1.9M/yr (net saving) | New platform run cost of $3.1M/yr offset by $5.0M/yr in retired legacy licensing, hosting, and manual-provisioning labor cost |

## 3-Year TCO: As-Is vs. To-Be

| | Year 1 | Year 2 | Year 3 | 3-Year Total |
|---|---|---|---|---|
| **As-Is (do nothing) run cost** | $17.3M | $17.8M* | $18.3M* | $53.4M |
| **To-Be capex** | $12.9M | $5.5M | $0 | $18.4M |
| **To-Be transition opex (dual-write overhead)** | $2.6M | $2.6M | $0 | $5.2M |
| **To-Be steady-state run cost (from month 25)** | $0 | $0 | $2.4M** | $2.4M |
| **To-Be total cost** | $15.5M | $8.1M | $2.4M | $26.0M |

\* As-is run cost assumed to grow ~3%/yr with subscriber growth and no efficiency gain, since the legacy estate's manual-provisioning cost structure does not improve on its own.
\*\* Year 3 reflects roughly 8 months of full steady-state run cost following transition completion at month 25, i.e., ~8/12 × $3.1M − 8/12 × $5.0M legacy saving ≈ $2.4M net for the partial year shown; from month 25 onward the steady-state run rate is a **net $1.9M/yr saving** versus as-is, as shown in the opex line above.

**3-year cost comparison: As-Is $53.4M vs. To-Be $26.0M → $27.4M lower total cost of ownership over 3 years**, before counting new revenue (below). This TCO comparison alone does not fully capture the business case, because the as-is column assumes Brenmark simply absorbs the inability to sell converged bundles or slices — the revenue case below is what actually justifies board approval.

## Revenue Case: Converged Bundles and 5G-Slice Monetization

| Revenue Driver | Assumption | Year 1 (partial, post-launch) | Year 2 | Year 3 |
|---|---|---|---|---|
| Converged bundle uptake | Bundles launch month 10; reach 8% of base by end Y1, 18% by end Y2, 25% by end Y3; ARPU uplift $6/mo per bundled subscriber vs. standalone | $1.7M | $7.8M | $10.8M |
| 5G network-slice monetization | Slice product launches month 16 (within 18-month mandate); enterprise/IoT slice customers ramp to 40 accounts by end Y2, 120 by end Y3, avg. $18K/account/yr | $0.1M | $0.7M | $2.2M |
| **Total incremental revenue** | | **$1.8M** | **$8.5M** | **$13.0M** |

Three-year cumulative incremental revenue: **$23.3M**. The $27.4M TCO improvement above is already net of the $18.4M capex and the $5.2M transition opex, since both are included in the To-Be cost totals used to compute it — no further subtraction of capex/opex is needed. Combining the $27.4M TCO improvement with the $23.3M incremental revenue gives a **net 3-year benefit of approximately $50.7M** relative to the as-is baseline of a $53.4M run cost with no ability to sell converged bundles or slices at all.

## Payback Period (Shown as Arithmetic)

- Cumulative net cash outlay by end of Year 1 (capex $12.9M + transition opex $2.6M, less $1.8M new revenue): **$13.7M net outflow**
- By end of Year 2 (add Year 2 capex $5.5M + opex $2.6M, less Year 2 revenue $8.5M and Year 2 legacy-saving delta versus as-is run cost, estimated at ~$3.0M for the year): net position ≈ $13.7M + $5.5M + $2.6M − $8.5M − $3.0M = **$10.3M cumulative net outflow at end of Year 2**
- Month-by-month within Year 3: steady-state net benefit runs at roughly $1.9M/yr saving + revenue run-rate exceeding $13M/yr by year end; the cumulative position crosses breakeven at approximately **month 22** from program start.

**Payback period: ≈ 22 months.** This is inside the 3-year horizon and roughly aligned with — slightly longer than — the board's 18-month mandate deadline, because the mandate deadline is a *capability* deadline (slice monetization must be *possible* by month 18), not a *breakeven* deadline; the business case does not require breakeven by month 18, only that the capability exists by then, which the roadmap in Phase F is built to satisfy.

## Governance Note

This business case is owned by the Program Director and reviewed by the ARB and CTO at each quarterly health review; any capex variance exceeding 10% of the approved $18.4M triggers mandatory escalation to the Board Technology Committee per the escalation path in `00-preliminary/governance-framework-setup.md`.

---

*Fictional case study — see [README](../README.md) for full disclaimer.*
