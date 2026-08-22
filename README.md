# Brenmark Telecom — BSS/OSS Modernization: A TOGAF ADM Case Study

**Disclaimer:** This is an illustrative TOGAF Enterprise Architecture case study modeling common, publicly known challenges in telecom BSS/OSS modernization — not a real engagement. Brenmark Telecom is an invented name, not affiliated with any real company, and nothing here is based on confidential information from any real employer or client. All figures, vendor names, and technical details are constructed for this exercise.

---

## Program Overview

This repository is a complete Enterprise Architecture work product for a fictional BSS/OSS modernization program at **Brenmark Telecom**, a mid-size telecom operator (~6M subscribers, mobile + fixed broadband). It follows the TOGAF Architecture Development Method (ADM) from Preliminary Phase through Phase H, and is aligned throughout to TM Forum Open Digital Architecture (ODA) and Open API principles — the industry-standard reference framework for BSS/OSS interoperability. Every artifact in this repository was produced as if by the architecture function running this program: principles, business/data/application/technology architecture, vendor evaluation, migration roadmap, governance, and Architecture Decision Records (ADRs).

## The Business Problem

Brenmark's billing system, CRM, and network inventory/order management system each maintain their own view of the customer, product, and order — there is no shared product catalog or customer/order data model across them. As a direct result:

- Brenmark cannot launch **converged bundles** (mobile + broadband + 5G network slice) because no system of record can express a bundled product spanning all three domains.
- Provisioning a single new service requires **manual handoffs between departments** and takes days, not the minutes competitors and customers now expect.
- Brenmark's board has mandated **5G network-slicing monetization within 18 months** — a capability the current OSS architecture has no path to support without fundamental change.

Leadership commissioned this EA engagement to define, govern, and sequence a BSS/OSS modernization program capable of meeting that mandate without destabilizing the revenue-critical legacy estate.

## How to Read This Repository

Every document here is written in **decision-voice**, not build-voice. You will not find "we built X using Y technology." You will find "we considered options A, B, and C; we chose B because of these quantified trade-offs; here is what governance body owns this decision and what it costs Brenmark if we're wrong." That is deliberate — this repository exists to demonstrate architectural judgment, not implementation effort. Costs, timelines, and vendor names throughout are invented and clearly illustrative; they exist to show the *mechanics* of a real cost-benefit and vendor-selection process, not to represent real figures.

Start with [`TOGAF-ADM-MAPPING.md`](./TOGAF-ADM-MAPPING.md) for a one-page map of every ADM phase to its folder. Read the phases roughly in order — later phases assume decisions made in earlier ones (particularly Phase A's scope boundaries and Phase C's data/application architecture).

## Repository Structure

| Phase | Folder | What's Inside |
|---|---|---|
| Preliminary | [`00-preliminary/`](./00-preliminary/) | Architecture principles; ARB governance setup |
| A — Vision & Scope | [`01-phase-a-vision-and-scope/`](./01-phase-a-vision-and-scope/) | Vision, scope, stakeholders, business case, exec summary |
| B — Business Architecture | [`02-phase-b-business-architecture/`](./02-phase-b-business-architecture/) | As-is/to-be business architecture, capability map |
| C — Information Systems Architecture | [`03-phase-c-information-systems-architecture/`](./03-phase-c-information-systems-architecture/) | Data architecture, application architecture |
| D — Technology Architecture | [`04-phase-d-technology-architecture/`](./04-phase-d-technology-architecture/) | Reference architecture, technology standards |
| E — Opportunities & Solutions | [`05-phase-e-opportunities-and-solutions/`](./05-phase-e-opportunities-and-solutions/) | Solution building blocks, vendor evaluation, gap analysis |
| F — Migration Planning | [`06-phase-f-migration-planning/`](./06-phase-f-migration-planning/) | Migration roadmap, transition architectures |
| G — Implementation Governance | [`07-phase-g-implementation-governance/`](./07-phase-g-implementation-governance/) | Governance framework, architecture contracts |
| H — Architecture Change Management | [`08-phase-h-change-management/`](./08-phase-h-change-management/) | Organizational change management plan |
| — | [`adrs/`](./adrs/) | Five architecturally significant decisions in ADR format |

See [`TOGAF-ADM-MAPPING.md`](./TOGAF-ADM-MAPPING.md) for the full phase-by-phase index.

---
*Fictional case study — see disclaimer above for full context.*
