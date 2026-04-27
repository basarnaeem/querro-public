# Querro

**Structured intelligence for professional services deals.**

Querro captures, organizes, and transforms client information into every professional output a deal requires — from the first kickoff meeting through closing. Briefing memos, financial models, due diligence trackers, country and sector research, risk registers, and pitchbooks all flow from the same structured data layer captured at the start of an engagement.

Live at **[querro.app](https://querro.app)** · Built solo · In active development

---

## The problem

Every investment banking, consulting, legal, and audit engagement begins the same way: a kickoff meeting between the deal team and the client. The information captured in that meeting determines the quality of everything downstream — the briefing memo, the financial model, the pitchbook, the diligence plan, the risk register.

In practice, that meeting is run from a generic checklist or from the senior banker's memory. Critical questions are missed. Industry-specific nuances are skipped. Jurisdictional regulatory context is filled in retroactively, often by a junior analyst Googling at 11pm. Special situations — distress, carve-outs, family-owned businesses, Shariah-compliant capital structures — get treated as edge cases when they should drive the entire question set.

The downstream cost is enormous: missed information becomes missed risk; missed risk becomes botched valuations, mispriced deals, and rework cycles that consume the analyst's first three years of career.

The AI tools shipping in this space — Rogo, Hebbia, Maywood, Model ML — assume the structured client information already exists somewhere. They analyze it, format it, summarize it. None of them build the tool that captures it in the first place.

Querro owns that first mile.

---

## What's in this repository

This is a public documentation repository. **No source code, prompts, schemas, or proprietary implementation details are published here.** It exists to give external readers — researchers, investors, prospective customers, fellowship reviewers — a clear view of what Querro is, how it is designed, and what it implies for the economics of professional services work.

| Document | What it covers |
|----------|----------------|
| [Overview](docs/01-overview.md) | What Querro is, who it's for, why it exists |
| [Architecture](docs/02-architecture.md) | The five-dimensional context model and modular content library |
| [AI System Design](docs/03-ai-system-design.md) | Where AI is used, where it isn't, and why that line is drawn carefully |
| [Evaluation](docs/04-evaluation.md) | How agent reliability and output quality are measured |
| [Current State](docs/05-current-state.md) | What is live in production today |
| [Roadmap](docs/06-roadmap.md) | What is being built next, and on what timeline |
| [Economic Impact](docs/07-economic-impact.md) | What Querro implies for the analyst-class labor market |

---

## Status snapshot

**Live in production at [querro.app](https://querro.app):**

- Email/password authentication and per-firm data isolation
- Engagement dashboard with multi-project, multi-jurisdiction support
- A 191-question structured intake covering general, operational, financial, legal, and HR dimensions of an investment banking deal
- Adaptive question suggestions powered by Claude
- Auto-saved responses, sensitivity flagging, and concentration-risk surfacing
- One-click generation of a professional briefing memo as a PDF, with AI-augmented executive summary and risk register

**In active development (April–June 2026):**

- A five-dimensional composition engine that replaces the static questionnaire with a dynamically tailored question set per engagement
- Document upload, OCR, page-by-page tagging, and tag-driven pre-fill of the questionnaire
- Country and sector research generation with citation grounding
- Information gap detection and a structured risk register
- Spreadsheet-format financial models tailored to the engagement's industry and mandate

See the [roadmap](docs/06-roadmap.md) for detail.

---

## Design philosophy

Three principles run through every decision in this product.

**1. Structure beats freeform.** Generative AI is most useful when constrained by a strong information schema. Querro's central bet is that the right primitive for professional work is not a chat window or a document but a structured engagement record that any output can be compiled from.

**2. Determinism where it matters; AI where it adds value.** The briefing memo is assembled by a deterministic compiler. AI is invoked only for the two sections — the executive summary and the consolidated risks — where natural-language synthesis genuinely helps. Every other section is rendered from structured fields. This is a deliberate choice: the cost of an incorrect AI-generated number in a deal document is higher than the cost of writing a compiler.

**3. The library is the moat.** The platform's intelligence lives in a versioned content library — questions, regulatory context, sector terminology, and special-situation overlays — that grows with every completed engagement. Software engineering builds the engine; domain expertise compounds in the library.

---

## About the founder

Querro is built solo by **Basar Naeem Qureshi**, a Master of Financial Engineering candidate at UCLA Anderson and former investment banking associate at Bridge Factor, where he led the first successful bank privatization in Pakistan in two decades. He holds the CFA charter (private markets pathway) and is targeting US middle-market boutique investment banks as the platform's first customer segment.

Contact: **basar@querro.app**

---

## Repository

Public documentation only. The product itself, including all source code, prompts, schemas, and implementation details, is closed source.

License: [CC BY-NC-ND 4.0](LICENSE) for documentation and written content. The Querro product and trademark are not licensed by this repository.

For inquiries — partnership, fellowship, advisory, customer pilot — see [CONTRIBUTING.md](CONTRIBUTING.md).
