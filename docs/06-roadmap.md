# Roadmap

## How to read this document

Querro is in active development and dates here are real, not aspirational. The roadmap is organized in five horizons: the current composition sprint (April–May 2026), the v2.0 build (May–June 2026), pilot rollout (Q3 2026), conversion and hiring (Q4 2026), and the longer-term expansion. Each horizon names a single anchoring goal and the decision criteria that gate moving to the next.

## Horizon 1 — Composition architecture sprint (April 25 to May 5, 2026)

**Anchoring goal:** A single end-to-end working slice of the five-dimensional composition architecture in production, replacing the current static questionnaire.

This is the most architecturally important sprint in the project's history. Every downstream feature in the platform — document pre-fill, country research, financial models — assumes the dynamic question engine exists. Until this sprint completes, those features remain blocked on the foundation.

The slice being built covers: the investment banking content library, all eight investment banking mandate types, one fully developed business model module, the corresponding sub-industry module, two priority jurisdiction modules, and three state mode modules. The dynamic question engine itself is implemented, the per-segment configuration interface is built, and the existing questionnaire pages are refactored to render from the engine's output rather than from the static library.

The gating criterion for moving to Horizon 2: the platform demonstrates that the same engagement metadata produces a meaningfully different and more relevant question set than the static version. The improvement is visible to a senior banker reviewing the output.

## Horizon 2 — The v2.0 build (May 6 to June 8, 2026)

**Anchoring goal:** A feature-complete v2.0 that demonstrates every layer of the long-term value proposition end-to-end on at least one realistic engagement.

The v2.0 build adds four major feature areas on top of the composition foundation laid in Horizon 1.

**Document pre-fill.** Users upload source materials — pitchbooks, financials, board decks, regulatory filings — and the platform extracts structured answers from them, mapped to the composed questionnaire with page-level citations. Each pre-filled answer is reviewed by the user before it commits to the engagement record.

**Country research.** A structured country research brief generated for each jurisdiction in the engagement, covering macro context, regulatory environment, sector positioning, and recent transaction activity. Generated content is grounded in cited sources.

**Information gaps and risk register integration.** The information gap detector identifies questions that are unanswered, weakly answered, or flagged for verification, and surfaces them as a follow-up checklist. The risk register — already live in version 1 — is more tightly integrated with the composed questionnaire so that flagged items propagate correctly across engagement segments.

**First financial model templates.** Three spreadsheet-format model templates, each tailored to a specific intersection of mandate type, business model, and sub-industry. These three are chosen because they cover the dominant deal types in the target US middle-market segment.

The v2.0 build is gated on a paper test: a complete kickoff workflow run end-to-end on a realistic deal scenario, producing a briefing memo, country and sector research package, populated risk register, and financial model template. If the resulting outputs would have been useful in a real engagement, v2.0 is feature-complete.

## Horizon 3 — Pilot rollout (Q3 2026)

**Anchoring goal:** Three to five pilot customers signed, all on free six-month pilot terms, in exchange for product feedback and case-study rights.

After v2.0 is feature-complete on June 8, the focus shifts from build to distribution. The first ninety days of customer development are concentrated, with the founder personally driving outreach to managing directors and senior partners at named US middle-market boutique firms.

Three channels run in parallel.

**Founder cold outreach.** Direct LinkedIn and email contact with senior bankers at priority target firms. Volume target is roughly ten qualified outbound contacts per week, calibrated against time available alongside continued product development.

**Conference presence.** Speaker slots and roundtable participation at mid-market deal conferences — ACG Capital Connection, Axial Concord Summit, M&A Source events, regional CFA society sessions. Booth presence is treated as low-leverage and avoided.

**Content marketing.** A weekly long-form post from the founder's account on LinkedIn, focused on a structured-thinking topic that exists inside the platform. The post demonstrates the platform's value without explicitly pitching it. A gated PDF of the underlying question framework serves as a lead magnet.

The Q3 2026 horizon ends with a clear go/no-go on a pre-seed funding round. If three or more pilots have signed and the build is on track, the founder begins a structured pre-seed conversation with a small set of vertical-SaaS-focused early-stage investors and professional-services-focused angels in Q4 2026.

## Horizon 4 — Conversion, hiring, and seed (Q4 2026 to Q1 2027)

**Anchoring goal:** Convert three of five pilots to paid commercial agreements; build the foundation of a small team; close a pre-seed or seed round.

The first paid customers fund the first non-founder hires. The hiring sequence is engineering-led: composition library scaling and module expansion are content-bound work that benefits from a second senior practitioner and a backend engineer dedicated to the financial model stack. A first sales hire — likely a former associate or vice president at a mid-market boutique — is added once the customer feedback loop is mature enough to support a commission-led role.

The seed round, when it closes, funds runway through Q1 2028 and supports a team of seven to nine. Use of funds: two to three additional engineers, one designer, one customer success manager, sustained content authoring across the long tail of the content library, and the SOC 2 Type II audit required to sell into US enterprise customers.

## Horizon 5 — Expansion (2027 and beyond)

**Within investment banking.** The remaining business model modules roll out across the forty-nine identified categories, prioritized by deal volume in the target segment. Sub-industry coverage scales toward the full one hundred sixty-three. Jurisdiction coverage extends to the United Kingdom, Canada, Singapore, and the Gulf states for firms running cross-border mandates. A pitchbook and information memorandum auto-draft feature ships, with the same deterministic-compiler-plus-bounded-AI architecture that the briefing memo uses.

**Across professions.** The architecture's design supports adding new professions without re-engineering the engine. Law (M&A legal, regulatory advisory), management consulting (strategy engagements, due diligence consulting), and audit and risk advisory are the highest-priority adjacencies. Each requires a new profession base and a new mandate set; the engine, the schema, and the user interface do not change. The first profession expansion targets a single named firm partnership, not a horizontal launch.

**Long run.** The vision is that Querro becomes the operating system for every professional engagement. The engagement record, structured well at the source, drives every output the engagement requires across its full lifecycle. Software handles modeling, drafting, due diligence management, and information synthesis. Humans handle relationships, judgment, and accountability.

## What this roadmap commits to and what it does not

This document commits to the architectural shape of the platform, the development sprint dates through June 2026, the customer segment focus through 2026, and the long-term professional-services-OS vision.

It does not commit to specific feature dates beyond the v2.0 milestone, to specific funding amounts, to specific named pilot customers, or to specific product features in the 2028-and-beyond horizon. Those commitments are made in private with the parties who will execute against them.
