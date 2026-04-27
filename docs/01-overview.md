# Overview

## What Querro is

Querro is a structured intelligence platform for professional services deals. The product begins where every deal begins — at the kickoff meeting between the deal team and the client — and produces every downstream artifact the engagement requires: briefing memos, financial models, country and sector research, due diligence trackers, risk registers, and information memoranda.

The thesis is that every professional services output is, in the end, a transformation of the same underlying client information. A pitchbook, an information memorandum, a credit memo, a valuation opinion, and a due diligence report are not five different documents. They are five different views of the same structured engagement record. Capture that record well at the source, tag every field precisely, and any of those views can be compiled on demand.

This shifts the unit of value in professional services software from "AI that drafts documents" to "structure that documents are drafted from." It is a more durable position because the structure does not get cheaper as language models get cheaper.

## The problem

Every investment banking, consulting, legal, and audit engagement begins the same way: a kickoff meeting between the deal team and the client. The information captured in that meeting determines the quality of everything downstream — the briefing memo, the financial model, the pitchbook, the diligence plan, the risk register.

In practice, that meeting is run from a generic checklist or from the senior banker's memory. Critical questions are missed. Industry-specific nuances are skipped. Jurisdictional regulatory context is filled in retroactively, often by a junior analyst working late. Special situations — distress, carve-outs, family-owned businesses, Shariah-compliant capital structures — get treated as edge cases when they should drive the entire question set.

The downstream cost is significant: missed information becomes missed risk; missed risk becomes botched valuations, mispriced deals, and rework cycles that consume the analyst's first years of career.

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

**Boutique firms have run out of margin.** Mid-market deal economics tightened through 2024 and 2025. The traditional answer to a complex engagement — staff another two analysts — is harder to justify when fee compression bites. Software that recovers analyst hours directly drops to the bottom line.

## What this repository is

This is a public documentation repository for external readers — investors, prospective customers, researchers, and engineering candidates. **No source code, prompts, schemas, or proprietary implementation details are published here.**

Read the docs in order: [Who It's For](02-who-its-for.md) → [Platform Design](03-platform-design.md) → [AI Philosophy](04-ai-philosophy.md) → [Production State](05-production-state.md) → [Roadmap](06-roadmap.md). Readers focused on labor-market implications should continue to [Economic Impact](07-economic-impact.md).
