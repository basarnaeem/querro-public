# Overview

## What Querro is

Querro is a structured intelligence platform for professional services deals. The product begins where every deal begins — at the kickoff meeting between a deal team and a client — and produces every downstream artifact the engagement requires: briefing memos, financial models, country and sector research, due diligence trackers, risk registers, information memoranda, and pitchbooks.

The thesis is that every professional services output is, in the end, a transformation of the same underlying client information. A pitchbook, an information memorandum, a credit memo, a valuation opinion, and a due diligence report are not five different documents. They are five different views of the same structured engagement record. Capture that record well at the source, tag every field precisely, and any of those views can be compiled on demand.

This shifts the unit of value in professional services software from "AI that drafts documents" to "structure that documents are drafted from." It is a more durable position because the structure does not get cheaper as language models get cheaper.

## Who it's for

The first customer segment is **US middle-market boutique investment banks** — firms running $50 million to $2 billion transactions across sell-side M&A, buy-side M&A, debt capital raises, restructuring, equity capital markets, private equity fund formation, and standalone advisory mandates.

This segment was chosen for four reasons.

1. **Volume.** Middle-market boutiques close 70% of US transactions by count. Per banker, throughput is high — four to twelve closed transactions per year per senior banker is normal — which means per-engagement efficiency gains compound rapidly.

2. **Pain.** The kickoff workflow is genuinely broken at this tier. Bulge-bracket banks have internal knowledge management systems and dedicated deal-prep teams; boutiques run on senior partners' memory and a generic template. The variance in question quality across kickoff meetings at a single mid-market firm is enormous, and that variance is the cost.

3. **Buying authority.** Boutique firms have decentralized technology procurement. A managing director can authorize a software pilot without a six-month committee process. The sales cycle is measured in weeks, not quarters.

4. **No internal AI engineering capacity.** Mid-market firms have neither the engineering teams to build this in-house nor the desire to. They will buy.

The named target list, in roughly descending order of fit: Houlihan Lokey, William Blair, Harris Williams, Lincoln International, Raymond James, Stifel, Piper Sandler, Robert W. Baird, Cowen, Capstone Partners, and approximately 200 to 300 firms in the next tier.

The platform extends naturally beyond investment banking into law firms (M&A legal, regulatory advisory), management consulting (strategy engagements, due diligence consulting), audit and risk advisory, and private equity diligence shops. The architecture is built to absorb these adjacent professions as additional content libraries; the engine itself does not change.

## The whitespace

The AI workflow tools shipping into investment banking today fall into one of three categories.

| Category | Companies | What they do | What they assume |
|----------|-----------|--------------|------------------|
| Document analyzers | Hebbia, Clarum | Read and synthesize existing documents | The data already exists in document form |
| Deal output generators | Maywood, Aviary, Model ML | Produce CIMs, memos, financial models | The structured client information already exists |
| Research copilots | Rogo, Samaya AI | Answer questions across a research universe | The user knows what to ask |

None of them solve the problem of **capturing structured client information in the first place**. They sit downstream of a structured intake step that, today, does not exist as a software product — it exists as an analyst, a Word document, and a senior banker's memory.

Querro is positioned at that capture layer. Every other workflow tool in the stack becomes a downstream consumer of Querro's structured engagement record.

## Why now

Three conditions converge in 2026 that did not hold five years ago.

**The cost of capturing structured information has collapsed.** Adaptive question generation, smart defaults from prior engagements, and automated tagging of uploaded documents are now feasible at production cost. Five years ago, building a useful structured intake for a middle-market deal would have required a content team of ten people maintaining hand-written question banks. Today, large language models compress that team into a versioned content library that one domain-expert founder can author and one engineer can maintain.

**The downstream output stack is being rebuilt anyway.** Every major professional services firm is in active conversation about replacing parts of its document and modeling stack with AI tooling. The window to embed at the data layer — before each firm picks a downstream tool that becomes its de facto data layer — is narrow and open now.

**Boutique firms have run out of margin.** Mid-market deal economics tightened through 2024 and 2025. The traditional answer to a complex engagement — staff another two analysts to it — is harder to justify when fee compression bites. Software that recovers analyst hours directly drops to the bottom line.

## Why solo, why now

The product is being built by one founder, currently solo, in active development since early April 2026. This is a deliberate choice rather than a constraint.

The composition architecture (described in [Architecture](02-architecture.md)) was designed specifically so that one person with deep domain expertise could author the content library while infrastructure scales linearly with engineering effort, not headcount. A larger team at this stage would build the wrong product faster.

A technical co-founder is being evaluated. The standing rule is: advisor and angel relationship first, co-founder title and equity only after sustained collaboration. The technical foundation is in place. A wrong co-founder hire is more damaging than a delayed one.

External funding will be raised once the v2.0 build is feature-complete — targeted at June 8, 2026 — and three to five customer pilots are in motion. The pre-seed plan is described in [Roadmap](06-roadmap.md).

## What this overview does not cover

This document is a high-altitude view. The dimensional architecture, the modular library structure, the AI system design, the evaluation methodology, and the production status are covered in dedicated documents in the [docs](.) folder. Readers who want to understand the technical bet should start with [Architecture](02-architecture.md) and [AI System Design](03-ai-system-design.md). Readers who want to understand the labor-economics bet should start with [Economic Impact](07-economic-impact.md).
