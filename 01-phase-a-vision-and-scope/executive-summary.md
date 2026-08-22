# Executive Summary

**Audience:** CEO, Board Technology Committee, Executive Leadership
**Program:** BSS/OSS Modernization — Brenmark Telecom

## The Problem

Brenmark cannot sell a single product that combines mobile, broadband, and (soon) 5G network slicing, because our billing, CRM, and network order-management systems each keep their own incompatible view of "customer" and "product." Provisioning a new service takes 3–7 days because staff manually coordinate across three disconnected systems. The Board has mandated 5G network-slicing monetization within 18 months; our current systems have no way to represent a network slice as something we can sell, bill, and activate.

## The Recommendation

Adopt a "strangler fig" modernization strategy: place a standards-based (TM Forum Open API) integration layer in front of the existing billing, CRM, and network systems, and build one authoritative product catalog and order-management capability behind it. Legacy systems keep running — we are not replacing the core billing engine — but new products, including converged bundles and 5G slices, are built on the new layer from day one. Capability moves off the legacy systems incrementally over time, not in a single risky cutover.

We rejected a full rip-and-replace of the BSS/OSS estate as too slow and too risky to meet an 18-month deadline, and rejected building new capability in a disconnected greenfield system as a path that would leave our existing 6M subscribers permanently stuck on the old, disconnected estate.

## Cost and Timeline

- **Investment:** approximately **$18.4M** in capital over 18 months, plus a temporary ~15% operational overhead on affected systems for roughly 24 months while old and new systems run in parallel.
- **Return:** approximately **$27.4M** in lower 3-year total cost of ownership versus doing nothing, plus approximately **$23.3M** in new converged-bundle and 5G-slice revenue over 3 years.
- **Payback period:** approximately **22 months** from program start.
- **Capability deadline (the Board's mandate):** 5G network-slice ordering, activation, and billing capability live by **month 18** — ahead of financial payback, which is expected by month 22.

## Key Risk

The largest risk is not technical failure — it's the temporary complexity of running two versions of "the truth" about customers and products side by side while we migrate. We are managing this with a dedicated reconciliation process and a defined 24-month sunset window, governed by a standing Architecture Review Board with representation from Billing, Customer Operations, Network Engineering, and Security, reporting to the CTO.

## What We're Asking For

Approval of the $18.4M capital program and the 18-month roadmap, with quarterly checkpoints where the Architecture Review Board reports progress against cost, schedule, and the capability milestones above.

---

*Fictional case study — see [README](../README.md) for full disclaimer.*
