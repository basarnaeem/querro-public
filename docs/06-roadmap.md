# Roadmap

## How to read this document

Querro is in active development by a solo founder and dates here are real, not aspirational. The roadmap is organized in three horizons: the current build sprint (April–May 2026), the v2.0 build (May–June 2026), and the post-v2.0 trajectory (Q3 2026 onward). Each horizon names a single anchoring goal, the work required to reach it, and the decision criteria that gate moving to the next.

This document is updated in step with the production build. The version of this file at any given moment reflects the current state of the plan, not a frozen snapshot.

## Horizon 1 — The composition architecture sprint (April 25 to May 5, 2026)

**Anchoring goal:** A single end-to-end working slice of the five-dimensional composition architecture in production, replacing the current static questionnaire.

This is the most architecturally important sprint in the project's history. Every downstream feature in the platform — document pre-fill, country research, sector research, financial models, risk register — assumes the composition engine exists. Until this sprint completes, everything downstream is blocked.

The slice being built covers: the investment banking question library, all eight investment banking mandate types, one fully developed business model overlay (regional banking), one fully developed sub-industry pack, two priority jurisdiction packs (United States and Pakistan, the latter chosen because the founder has a clean test fixture from prior deal work), and three state mode overlays (Shariah-compliant, state-owned, and privatization). The composition engine itself is implemented, the per-segment dimension selection user interface is built, and the existing operational page is refactored to render from the composed output rather than from the static library.

By the end of this sprint, the platform demonstrates that the same engagement metadata routed through the composition engine produces a meaningfully different and more relevant question set than the static version. The improvement is visible to a senior banker reviewing the output. This is the gating criterion for moving to Horizon 2.

## Horizon 2 — The v2.0 build (May 6 to June 8, 2026)

**Anchoring goal:** A feature-complete v2.0 of the platform that demonstrates every layer of the long-term value proposition end-to-end on at least one realistic engagement.

The v2.0 build adds five major feature areas on top of the composition foundation laid in Horizon 1.

**Documents.** Users upload source materials — pitchbooks, financials, board decks, regulatory filings — and the platform stores them page-by-page, tags each page against the engagement's question schema, and pre-fills the questionnaire with proposed answers anchored to specific page citations. Each pre-filled answer is reviewed by the user before it commits to the engagement record.

**Country research.** A structured country research brief generated for each jurisdiction in the engagement, covering macro context, regulatory environment, sector positioning, and recent transaction activity. Generated content is grounded in cited sources surfaced at the time of generation.

**Sector research.** A parallel structured brief at the sub-industry level, covering competitive dynamics, peer set, valuation benchmarks, and current sector themes.

**Information gaps and risk register.** Two reciprocal features. The information gap detector identifies questions that are unanswered, weakly answered, or flagged for verification, and surfaces them as a follow-up checklist. The risk register synthesizes flagged items across the engagement into a structured, editable register that the deal team can refine before it lands in the briefing memo.

**First financial model templates.** Three spreadsheet-format model templates, each tailored to a specific intersection of mandate type, business model, and sub-industry: a regional bank sell-side merger model, a SaaS company growth-equity model, and a manufacturing buyout model with a leveraged-buyout output schedule. These three are chosen because they cover the three dominant deal types in the target US middle-market segment.

The v2.0 build is gated on a paper test: a complete kickoff workflow run end-to-end on the founder's own historical deal experience, producing a briefing memo, a country and sector research package, a populated risk register, and a financial model template. If the resulting outputs would have been useful in the original engagement, v2.0 is feature-complete. If they would not, the relevant feature areas are extended before the gate is cleared.

## Horizon 3 — Pilot and pre-seed (Q3 2026)

**Anchoring goal:** Three to five pilot customers signed, all on free six-month pilot terms, in exchange for product feedback and case-study rights.

After v2.0 is feature-complete on June 8, the focus shifts from build to distribution. The first ninety days of customer development are deliberately concentrated, with the founder personally driving outreach to managing directors and senior partners at named US middle-market boutique firms. The full target list is not published in this document.

Three channels run in parallel.

**Founder cold outreach.** Direct LinkedIn and email contact with senior bankers at the priority target firms. Volume target is roughly ten qualified outbound contacts per week, calibrated against time available alongside continued product development.

**Conference presence.** Speaker slots and roundtable participation at mid-market deal conferences — ACG Capital Connection, Axial Concord Summit, M&A Source events, regional CFA society sessions. Booth presence is treated as low-leverage and avoided.

**Content marketing.** A weekly long-form post from the founder's account on LinkedIn, focused on a structured-thinking topic that exists inside the platform — for example, the questions a banker should ask when running a kickoff for a regional bank engagement. The post itself demonstrates the platform's value without explicitly pitching it. A gated PDF of the underlying question framework serves as a lead magnet.

The Q3 2026 horizon ends with a clear go/no-go on a pre-seed funding round. If three or more pilots have signed and the build is on track, the founder begins a structured pre-seed conversation with a small set of vertical-SaaS-focused early-stage investors and professional-services-focused angels in Q4 2026. If pilot traction is weaker than expected, the pre-seed is delayed and the additional time is spent on product and on the next round of customer development.

## Horizon 4 — Conversion, hiring, and seed (Q4 2026 to Q1 2027)

**Anchoring goal:** Convert three of five pilots to paid commercial agreements; build the foundation of a small team; close a pre-seed or seed round at standard early-stage terms.

The first paid customers fund the first non-founder hires. The hiring sequence is engineering-led: composition library scaling and sub-industry pack expansion are content-bound work that benefits enormously from a second senior practitioner contributing alongside the founder, and from a backend engineer dedicated to the financial model template stack. A first sales hire — likely a former associate or vice president at a mid-market boutique — is added once the customer feedback loop is mature enough to support a commission-led role.

The seed round, when it closes, funds runway through Q1 2028 and supports a team of seven to nine. The use of funds is straightforward: two to three additional engineers, one designer, one customer success manager, sustained content authoring against the long tail of the sub-industry library, and the SOC 2 Type II audit required to sell into US enterprise customers.

## Horizon 5 — Beyond v2.0 (2027 and beyond)

The architecture is built so that the platform extends naturally beyond the initial investment banking beachhead without re-engineering the engine.

**2027 expansion within investment banking.** The remaining business model overlays roll out across the forty-nine identified categories, prioritized by deal volume in the target segment. Sub-industry coverage scales toward the full one hundred sixty-three. Jurisdiction coverage extends to the United Kingdom, Canada, Singapore, and the Gulf states for firms running cross-border mandates. Document pre-fill quality is improved through cumulative user feedback and the curated evaluation set described in [Evaluation](04-evaluation.md). A pitchbook and information memorandum auto-draft feature ships, with the same deterministic-compiler-plus-bounded-AI architecture that the briefing memo uses.

**2028 expansion across professions.** The architecture's mandate dimension is designed to accept additional professions. Law (M&A legal, regulatory advisory), management consulting (strategy engagements, due diligence consulting), and audit and risk advisory are the highest-priority adjacencies. Each requires a new profession base and a new mandate set; the engine, the schema, and the user interface do not change. The first profession expansion targets a single named firm partnership, not a horizontal launch.

**2029 and beyond.** The long-run vision is that Querro becomes the operating system for every professional engagement: investment banking, legal advisory, management consulting, and audit. The engagement record, structured well at the source, drives every output the engagement requires across its full lifecycle. Software handles modeling, drafting, due diligence management, and information synthesis. Humans handle relationships, judgment, and accountability. The labor implications of this trajectory are discussed in [Economic Impact](07-economic-impact.md).

## What this roadmap commits to and what it does not

This document commits to the architectural shape of the platform, the development sprint dates through June 2026, the customer segment focus through 2026, and the long-term professional-services-OS vision.

It does not commit to specific feature dates beyond the v2.0 milestone, to specific funding amounts, to specific named pilot customers, or to specific product features in the 2028-and-beyond horizon. Those commitments are made in private with the parties who will execute against them. Updates to this document over time will reflect dates and decisions as they are actually made.
