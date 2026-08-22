# Vendor Evaluation: Product Catalog & Order Orchestration Platform

**Phase:** E — Opportunities & Solutions
**Note:** Vendor and product names below are invented for this fictional case study and do not refer to any real company or product.

## Scope of This Evaluation

This evaluation covers the combined **Product Catalog Platform** and **Order Orchestration Platform** solution building blocks (see `solution-building-blocks.md`), the single highest-stakes buy decision in the program, since these two platforms are what make converged bundles and slice monetization technically possible at all. Four vendors were evaluated; each submitted a response to Brenmark's RFP and completed a proof-of-concept against a representative converged-bundle and slice-ordering scenario.

## Evaluated Vendors (Fictional)

- **Meridian Commerce Suite** ("Vendor A") — established BSS platform vendor, broad telecom customer base
- **Northolt BSS Cloud** ("Vendor B") — cloud-native challenger vendor, TM Forum ODA-native architecture
- **Cascade Digital Commerce** ("Vendor C") — mid-market BSS vendor with strong catalog engine, weaker orchestration
- **Ferro OSS/BSS Platform** ("Vendor D") — network-orchestration-heavy vendor, weaker commerce/catalog depth

## Weighted Evaluation Criteria

| Criterion | Weight | Rationale for Weight |
|---|---:|---|
| TM Forum Open API conformance (out-of-box) | 20% | Directly enforces P-02; poor conformance means Brenmark absorbs integration cost the vendor should have. |
| Converged-bundle & multi-domain product modeling | 20% | Directly addresses the core business problem (Phase A); this is the single most important functional fit criterion. |
| 5G network-slice product/orchestration support | 15% | Directly addresses the board's 18-month mandate. |
| Implementation timeline fit (≤ 12 months to first go-live) | 15% | Program must hit the 18-month deadline; a platform that cannot implement within 12 months structurally endangers the mandate. |
| Total cost of ownership (license + implementation + 3-yr run) | 10% | Must fit the business case in `01-phase-a-vision-and-scope/business-case.md`. |
| Vendor lock-in / exit cost | 10% | Enforces P-04 (reversibility); a platform with proprietary, non-portable data models scores poorly here regardless of functional fit. |
| Reference customer base in telecom BSS | 5% | De-risks the selection with proven operational history at comparable scale. |
| Partner/systems-integrator ecosystem depth | 5% | Affects delivery risk and future extensibility. |

## Scoring (1–5 scale per criterion, weighted)

| Criterion | Weight | Vendor A | Vendor B | Vendor C | Vendor D |
|---|---:|:---:|:---:|:---:|:---:|
| Open API conformance | 20% | 3 | 5 | 4 | 3 |
| Converged-bundle modeling | 20% | 4 | 5 | 4 | 2 |
| 5G-slice support | 15% | 2 | 4 | 2 | 5 |
| Implementation timeline fit | 15% | 2 | 4 | 4 | 3 |
| TCO | 10% | 3 | 4 | 4 | 2 |
| Lock-in / exit cost | 10% | 2 | 4 | 3 | 3 |
| Reference base in telecom | 5% | 5 | 3 | 3 | 4 |
| Partner/SI ecosystem | 5% | 5 | 3 | 3 | 3 |
| **Weighted Total (out of 5)** | | **3.00** | **4.30** | **3.50** | **3.05** |

*(Weighted total = Σ(criterion score × weight); e.g., Vendor B = 5(.20)+5(.20)+4(.15)+4(.15)+4(.10)+4(.10)+3(.05)+3(.05) = 1.00+1.00+0.60+0.60+0.40+0.40+0.15+0.15 = 4.30.)*

## Recommendation: Vendor B — Northolt BSS Cloud

Vendor B scores highest overall and, more importantly, wins decisively on the three criteria most tied to program success: Open API conformance, converged-bundle modeling, and implementation timeline fit. Its cloud-native, ODA-native architecture is a direct fit for the strangler-fig reference architecture (Phase D) — it was designed to sit behind an API gateway and integrate with legacy systems rather than assuming it is the only system in the estate, which is exactly Brenmark's situation.

## Why the Runners-Up Lost

- **Vendor D (Ferro)** scored highest on 5G-slice orchestration specifically (5/5) — reflecting genuine strength in network-side orchestration — but scored weakest on converged-bundle commerce modeling (2/5) and Open API conformance (3/5), the two highest-weighted criteria. Selecting Vendor D would have solved the board's slice mandate narrowly while leaving the broader converged-bundle problem under-addressed, which was judged an unacceptable trade given Phase A's problem statement treats both as co-equal drivers. Vendor D's slice-orchestration strength is preserved in the architecture regardless — the Network-Slice Orchestration Adapter SBB is built in-house and can integrate with Vendor D's network-side tooling later if needed without re-opening this platform decision.
- **Vendor C (Cascade)** scored competitively on TCO and timeline (4/5 each) with a genuinely strong catalog engine, but its orchestration capability was materially weaker (order orchestration was a partner add-on, not native), which conflicts with treating orchestration as core, not supplementary, to solving the manual-handoff problem (Phase B). It was the closest runner-up and remains the recommended fallback if Vendor B contract negotiations fail.
- **Vendor A (Meridian)** is the most established vendor with the deepest telecom reference base and partner ecosystem (5/5 on both), which matters for delivery risk — but its architecture predates the Open API/ODA generation of BSS platforms, scoring weakest on conformance (3/5) and worst of all four on implementation timeline fit (2/5) and lock-in (2/5). Its estimated implementation timeline of 16–20 months for full catalog + orchestration capability structurally conflicts with the 18-month mandate once integration and testing time is added, and was disqualifying on its own even before considering the other criteria.

## Governance Note

This recommendation was presented to the ARB for approval per the RACI in `01-phase-a-vision-and-scope/stakeholder-map.md` (Program Director Responsible, ARB Chief EA Accountable, CTO Consulted). Final commercial terms remain subject to Procurement negotiation; the exit-cost criterion above (Vendor B: 4/5) was a specific negotiating point to secure contractual data-portability commitments before signature, consistent with P-04.

---

*Fictional case study — see [README](../README.md) for full disclaimer.*
