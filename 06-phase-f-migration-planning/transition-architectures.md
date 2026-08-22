# Transition Architectures

**Phase:** F — Migration Planning

## Why Named Transition States Matter

TOGAF Phase F distinguishes the as-is and to-be baselines from one or more explicit **transition architectures** — intermediate states the organization deliberately passes through and operates in for a meaningful period, not just a snapshot mid-migration. Naming and documenting these states matters because each one has its own risk profile, its own operational procedures, and its own governance obligations that differ from both the as-is and the to-be state. Skipping this step and treating migration as a single undifferentiated "in progress" period is a common cause of operational surprises in modernization programs — teams discover mid-transition that nobody defined what "correct" looks like for the intermediate state they're actually running in.

This program defines two named transition architectures, corresponding to the wave boundaries in `migration-roadmap.md`.

## Transition Architecture 1: "Gatewayed Legacy" (post-Wave 1, months 7–12)

**What's true at this state:**

- The API Gateway/Strangler Layer is live and enforced; all *new* integration traffic must route through it.
- The Legacy Billing Adapter and Legacy Network Inventory Adapter expose legacy capability via TM Forum Open API-conformant endpoints.
- The Customer Domain Service holds a reconciled, authoritative customer record — but the Product Catalog and Order Orchestration platforms are **not yet live**; product definitions and order capture still run on the legacy CRM/Billing modules.
- Some legacy-to-legacy point-to-point integrations (the original nightly batch sync) still exist and run in parallel with the new gateway traffic, because the systems they update (legacy product tables, legacy order records) haven't yet been superseded.

**Why this state is necessary:** Standing up the gateway and adapters before the catalog/orchestration platforms exist lets Brenmark validate that legacy systems can reliably respond to API traffic — including under production load — before betting the higher-value catalog and orchestration capability on that assumption. It also gives delivery teams a working integration surface to build and test the Product Catalog and Order Orchestration platforms against in Wave 2, rather than building those platforms against a moving target.

**What's explicitly NOT true yet at this state (and must not be assumed):** There is no single product catalog; no cross-domain orchestration; the manual handoff process described in the as-is business architecture is still the operational reality for customers. Frontline staff training for Phase H has not yet begun in earnest, because there is no new workflow to train them on. Any stakeholder communication during this window (see Phase H) must be explicit that this is infrastructure work with no visible customer-facing change yet — a risk the change management plan addresses directly, since a silent 5-6 month period with no visible progress can otherwise be misread by stakeholders as the program stalling.

**Governance obligation specific to this state:** The integration inventory (P-10) must show, for every legacy-to-legacy link still running, an explicit target retirement wave — an "unretired, unscheduled" legacy link found during this transition state is treated as a Blocking finding under Phase G, precisely because this is the state where such links are easiest to lose track of.

## Transition Architecture 2: "Dual-Catalog Reconciliation" (post-Wave 2, months 12–18, overlapping Wave 3)

**What's true at this state:**

- The Product Catalog Platform is authoritative and live for all *new* single-domain product sales; the Order Orchestration Platform handles standard, single-domain order-to-activation automatically.
- The legacy Billing system's internal product tables **still exist and are still read by the billing engine's rating logic** — they are kept consistent with the new Product Catalog via the Dual-Write Reconciliation Service (ADR-004), on a defined reconciliation interval, not real-time.
- Converged bundles and 5G-slice products are being defined and tested in the Product Catalog but have **not yet launched commercially** (that's Wave 3's milestone) — this state is the immediate precursor to bundle/slice launch, not the launch state itself.
- Two definitions of "product" now concurrently exist in production: the authoritative one (Product Catalog) and the reconciled shadow copy (legacy billing tables) — this is the specific condition principle P-01 is normally written to prevent, tolerated here only because it is time-boxed and governed under ADR-004, not a permanent architecture decision.

**Why this state is necessary:** The billing engine's rating logic cannot be modified to read directly from the new Product Catalog without touching the financial ledger itself — which Phase A explicitly puts out of scope. The reconciliation approach lets new product definitions go live for customers immediately while the legacy billing engine keeps working from its own (now-derived, not authoritative) copy, avoiding the alternative of blocking the entire Product Catalog launch on a billing-engine change that isn't otherwise justified.

**Risk specific to this state:** Reconciliation lag or failure creates a window where a customer-visible product (in the catalog) doesn't yet correctly rate in billing, or vice versa. This is the operational overhead quantified in the business case (~15%, ~24 months) and is the primary reason ADR-004 mandates active monitoring and a defined maximum reconciliation lag, with automatic alerting to Billing Operations if lag exceeds threshold.

**Exit condition:** This transition state ends — and the legacy billing product tables become formally deprecated — only once reconciliation-service monitoring shows sustained accuracy and lag within threshold across at least one full billing cycle post-Wave-3 bundle launch, per the criteria set in ADR-004. Exiting this state is a Phase G governance checkpoint, not an automatic calendar event.

## Relationship to the To-Be Architecture

Neither transition architecture is the program's end state. The to-be architecture (Phase B/C/D) describes the state the program is *aiming at*; these two transition architectures describe states Brenmark actually operates in in production for months at a time along the way, each with governance obligations the to-be architecture itself does not have (because the to-be architecture, by definition, no longer carries transitional dual-write or partial-gateway conditions).

---

*Fictional case study — see [README](../README.md) for full disclaimer.*
