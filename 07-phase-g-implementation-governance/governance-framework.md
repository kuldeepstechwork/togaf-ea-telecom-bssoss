# Implementation Governance Framework

**Phase:** G — Implementation Governance

## Purpose

Phase G governs the gap between an approved architecture (Phases B–F) and what delivery teams actually build. Its central mechanism is the **architecture contract** (detailed in `architecture-contracts.md`), backed by a compliance-checkpoint and non-compliance-handling process defined here.

## Compliance Checkpoints

Every solution building block (per `05-phase-e-opportunities-and-solutions/solution-building-blocks.md`) passes through four mandatory checkpoints before production go-live, each owned by the ARB:

| Checkpoint | Timing | What's Reviewed | Gate Owner |
|---|---|---|---|
| **Contract Sign-Off** | Before delivery work begins | Architecture contract terms (scope, principles cited, NFR targets, exceptions disclosed) | ARB (Chief EA accountable) |
| **Design Conformance Review** | Mid-delivery, at detailed design completion | Conformance to cited principles and technology standards; API schema conformance to TM Forum Open API patterns | EA function (delegated reviewer) |
| **Pre-Production Readiness Review** | Before go-live | NFR test evidence (per P-11); security/access-control sign-off (P-06); integration inventory registration (P-10) | ARB + Head of InfoSec |
| **Post-Go-Live Health Check** | 30 days after go-live | Actual vs. target NFRs in production; any compliance drift since Pre-Production Review | EA function, reported to ARB at next standing session |

A solution building block may not proceed past a checkpoint without an explicit pass; a checkpoint may be passed conditionally with a logged remediation item and a deadline, but conditional passes are visible in the compliance register, not treated as equivalent to a clean pass.

## Non-Compliance Categories and Handling

| Category | Definition | Handling |
|---|---|---|
| **Advisory** | A deviation from a standard or principle that carries low risk and doesn't block production (e.g., a documentation gap) | Logged in the compliance register; must be remediated within 60 days but does not block go-live |
| **Must-Fix-Before-Production** | A deviation that creates meaningful operational or compliance risk if unaddressed (e.g., missing NFR test evidence) | Blocks Pre-Production Readiness Review pass; delivery team must remediate and re-present |
| **Blocking** | A deviation that violates a unanimous-approval principle (P-01, P-06) without an approved exception, or an unregistered integration (P-10) | Immediately escalated to the ARB chair; production deployment is halted until resolved or a valid exception is retroactively sought and approved (exceptions are not typically granted retroactively, and a delivery team should expect this path to be harder and slower than seeking the exception up front) |

## Handling an Expired, Unrenewed Exception

As established in `04-phase-d-technology-architecture/technology-standards.md`, every approved exception carries a mandatory expiry date. An exception that lapses without a renewal request is automatically reclassified as a **Blocking** finding — not Advisory — because an expired exception represents a standard the organization already judged necessary to eventually enforce; the delivery team does not get the benefit of the doubt for having previously received permission to deviate.

## Architecture Contracts as the Enforcement Instrument

The architecture contract (see `architecture-contracts.md`) is the vehicle through which every checkpoint above is actually executed — it is issued at Contract Sign-Off, referenced at Design Conformance Review, and its NFR/security terms are the acceptance criteria checked at Pre-Production Readiness Review. A solution building block without a signed architecture contract cannot legitimately pass any subsequent checkpoint; contracts are not paperwork produced after the fact.

## Reporting Cadence

The EA function maintains a live compliance register (Advisory / Must-Fix / Blocking findings, by solution building block) and reports a summary at every standing ARB session. The quarterly architecture health review (per `00-preliminary/governance-framework-setup.md`) includes a compliance-register trend view to the CTO and Board Technology Committee — a rising Blocking-finding count is treated as a program-health signal in its own right, independent of the delivery roadmap's on-time status, because a program that is "on schedule" while accumulating unresolved Blocking findings is building up architecture debt that will surface later, typically at the worst possible time (production incident, audit, or a difficult legacy retirement).

---

*Fictional case study — see [README](../README.md) for full disclaimer.*
