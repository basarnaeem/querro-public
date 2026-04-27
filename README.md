# Querro

**Structured intelligence for professional services deals.**

Querro captures, organizes, and transforms client information into every professional output a deal requires — from the first kickoff meeting through closing. Briefing memos, financial models, due diligence trackers, country and sector research, risk registers, and pitchbooks all flow from the same structured data layer captured at the start of an engagement.

Live at **[querro.app](https://querro.app)** · Built solo · In active development

---

## The problem

Every investment banking engagement begins the same way: a kickoff meeting between the deal team and the client. The information captured in that meeting determines the quality of everything downstream.

In practice, that meeting is run from a generic checklist or from the senior banker's memory. Critical questions are missed. Industry-specific nuances are skipped. Special situations — distress, carve-outs, family-owned businesses, Shariah-compliant capital structures — get treated as edge cases when they should drive the entire question set.

The AI tools shipping into this space — Rogo, Hebbia, Maywood, Model ML — assume the structured client information already exists somewhere. They analyze it, format it, summarize it. None of them build the tool that captures it in the first place.

Querro owns that first mile.

---

## What's in this repository

This is a public documentation repository. **No source code, prompts, schemas, or proprietary implementation details are published here.** It exists to give external readers — investors, prospective customers, researchers, and engineering candidates — a clear view of what Querro is, how it is designed, and what it implies for the economics of professional services work.

Read in order:

| #   | Document                                        | What it covers                                                          |
| --- | ----------------------------------------------- | ----------------------------------------------------------------------- |
| 1   | [Overview](docs/01-overview.md)                 | What Querro is, the problem it solves, the whitespace, why now          |
| 2   | [Who It's For](docs/02-who-its-for.md)          | Target customer segment, why this segment, expansion path               |
| 3   | [Platform Design](docs/03-platform-design.md)   | The contextual architecture and content library that power the platform |
| 4   | [AI Philosophy](docs/04-ai-philosophy.md)       | Where AI is used, where it isn't, and how outputs are validated         |
| 5   | [Production State](docs/05-production-state.md) | What is live in production today, with screenshots                      |
| 6   | [Roadmap](docs/06-roadmap.md)                   | What is being built next, and on what timeline                          |
| 7   | [Economic Impact](docs/07-economic-impact.md)   | What Querro implies for the analyst-class labor market                  |

---

## Status snapshot

**Live in production at [querro.app](https://querro.app):**

- Email/password authentication and per-firm data isolation
- Engagement dashboard with multi-project, multi-jurisdiction support
- A 191-question structured intake covering general, operational, financial, legal, and HR dimensions
- Adaptive question suggestions powered by Claude
- Three-state source attribution (AI Research, Primary Research, AI Research Edited) on every answer
- Auto-saved responses, sensitivity flagging, and concentration-risk surfacing
- One-click generation of a professional briefing memo as a PDF (deterministic compiler + two bounded AI sections)
- AI-generated risk register with auto-flags from flagged questionnaire fields
- Document upload with page-by-page text extraction and tag-based organization
- Sector research with AI-generated content and inline source citations

**In active development (ends May 5, 2026):**

- Dynamic question tailoring — replacing the static questionnaire with a contextually tailored question set per engagement, derived from the mandate type, target's business model and industry, applicable jurisdictions, and any special situations

**Coming in Phase 2 (May 6 to June 8, 2026):**

- Document pre-fill with AI tagging — extracting structured answers from uploaded documents, mapped to questionnaire fields with page citations
- Country research generation with citation grounding
- Information gap detection — structured checklist of unanswered or weakly-answered questions
- Financial model templates — spreadsheet-format, tailored to the engagement's mandate and industry

See the [Roadmap](docs/06-roadmap.md) for detail.

---

## Design philosophy

Three principles run through every decision in this product.

**Structure beats freeform.** Generative AI is most useful when constrained by a strong information schema. Querro's central bet is that the right primitive for professional work is not a chat window or a document but a structured engagement record that any output can be compiled from.

**Determinism where it matters; AI where it adds value.** The briefing memo is assembled by a deterministic compiler. AI is invoked only for the sections where natural-language synthesis genuinely helps. Every other section is rendered from structured fields. The cost of an incorrect AI-generated number in a deal document is higher than the cost of writing a compiler.

**The content library is the moat.** The platform's intelligence lives in a versioned content library — questions, regulatory context, industry terminology, and special-situation logic — that grows with every completed engagement. Software engineering builds the engine; domain expertise compounds in the library.

---

## About the founder

Querro is built by **Basar Naeem Qureshi**, a Master of Financial Engineering candidate at UCLA Anderson and former investment banking associate. He has passed all three levels of the CFA Program (private markets pathway) and is targeting US middle-market boutique investment banks as the platform's first customer segment.

Contact: **basar@querro.app**

---

## Repository

Public documentation only. The product itself, including all source code, prompts, schemas, and implementation details, is closed source.

License: [CC BY-NC-ND 4.0](LICENSE) for documentation and written content. The Querro product and trademark are not licensed by this repository.

For inquiries — partnership, fellowship, advisory, customer pilot — see [CONTRIBUTING.md](CONTRIBUTING.md).
