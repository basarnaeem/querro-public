# Current State

**As of April 26, 2026.**

This document is a literal description of what exists in production today at [querro.app](https://querro.app). The architectural and roadmap documents in this repository describe where the platform is heading; this document describes where it actually is. Everything below is verifiable by creating an account on the live site.

The platform has been in active development since early April 2026. The current production build represents approximately three weeks of solo engineering work and is best understood as a fully functional version 1, deliberately built on a static question library so that the composition architecture (described in [Architecture](02-architecture.md)) can be developed and tested against a working baseline.

## What works in production

### Authentication and account management

Email and password authentication, password reset, and session management. Per-firm data isolation enforced at the database level via row-level security. A user signing into the platform sees only their own engagements; cross-firm data leakage is structurally impossible rather than policy-enforced.

### Dashboard

A project dashboard listing all engagements the user has created, with metadata: project name, client legal name, mandate type, deal size, deal currencies, jurisdictions, timeline, and progress percentage. New engagements are created via a multi-step modal that captures the engagement metadata and provisions the project in the database. Each project card routes to that engagement's workspace.

### Structured questionnaire (version 1, static)

A 191-question questionnaire organized across five sections, modeling the kickoff information capture for a US middle-market investment banking engagement.

| Section | Questions | Coverage |
|---------|-----------|----------|
| General | 20 | Company background, contacts, mandate basics, deal scope |
| Operational | 62 | Business model, customers, competition, suppliers, geography, segments, KPIs |
| Financial | 46 | Historical performance, projections, capital structure, working capital, off-balance-sheet items |
| Legal | 39 | Corporate structure, contracts, IP, litigation, regulatory, ESG |
| HR | 23 | Headcount, key persons, compensation, turnover, labor relations |

Every question is rendered through a typed component that supports text input, long-form text, single-select, multi-select, numeric, currency-aware numeric, date, percent, and table inputs. Each question carries metadata describing whether it is required, sensitive (for example, executive compensation detail, which carries a red flag), or watch-flagged (concentrations and dependencies that auto-flag at threshold values).

Responses auto-save with an 800-millisecond debounce. A user can leave the platform mid-question, return hours later, and resume exactly where they left off. Each section displays a real-time progress percentage computed from the share of required questions answered.

The questionnaire today is statically authored. The composition architecture being built in the current sprint replaces this static layer with a dynamically composed one, retaining all existing UI components and replacing only the data source.

### Adaptive question suggestions

When a user is filling out the questionnaire, the system surfaces follow-up questions tailored to the answers already given. These suggestions appear as cards inside the relevant section, each with an accept-or-dismiss control. Accepted suggestions become part of that engagement's question set; dismissed suggestions are logged and used to improve future suggestion quality.

### Briefing memo generation

A one-click action on the engagement workspace produces a professional briefing memo as a PDF, with the firm's branding applied. The memo is structured into eight sections covering company overview, deal context, business and operations, financials, legal and compliance, human capital, key risks, and next steps.

The memo is assembled by a deterministic compiler that maps structured questionnaire fields into the memo template. Two sections — the executive summary and the consolidated key risks — are augmented with AI-generated prose, bounded to roughly 600 and 800 tokens respectively. Every other section is rendered from structured fields without language model involvement. The full reasoning for this design is in [AI System Design](03-ai-system-design.md).

The PDF is generated server-side, sanitized to handle the full set of characters that appear in international deal contexts, and delivered as a download. Generation typically completes in under fifteen seconds.

### Sensitivity and concentration flagging

Specific questions are flagged at the schema level as sensitive — for example, executive compensation breakdowns trigger a visible red border and a notice that the answer should be handled with care. Other questions are flagged as concentration risks — for example, customer concentration above a threshold automatically surfaces a warning in the operational section and propagates to the risk register in the briefing memo.

### Landing page and marketing site

The public landing page at querro.app explains the product to prospective customers without naming or describing the underlying architecture. It includes an interactive seven-frame walkthrough that demonstrates the flow from kickoff configuration through briefing memo generation. The interactive walkthrough is the strongest single artifact for understanding what the product does without creating an account.

## Technology stack

The production stack, briefly:

- **Frontend and server framework:** Next.js (App Router) on TypeScript
- **Styling:** Tailwind CSS with a custom design system (warm off-white background, deep forest green primary, terracotta accents — calibrated to feel like a Moleskine notebook rather than a Bloomberg terminal)
- **Authentication and database:** Supabase (PostgreSQL with row-level security)
- **AI:** Anthropic API, Claude Sonnet model family, no training on user data per Anthropic's commercial terms
- **PDF rendering:** server-side React PDF
- **Deployment:** Vercel with auto-deploy from the main branch
- **Domain and DNS:** Cloudflare (proxy disabled to avoid TLS conflicts with the Vercel certificate)
- **Package management:** pnpm

The full source code is closed. The above describes only the infrastructure surface that is publicly observable.

## What does not yet exist in production

Six features are described in the [Roadmap](06-roadmap.md) but are not in the current production build. They are listed here for clarity about the boundary between today and the near future.

1. **Composition engine.** The five-dimensional question composition described in [Architecture](02-architecture.md) is in active development. The current questionnaire is a static superset; the composition engine will replace it with a tailored subset per engagement.

2. **Document upload and pre-fill.** Users currently enter all data manually. Document upload, page-by-page storage, AI tagging, and tag-driven pre-fill of the questionnaire are scheduled for the next phase of development.

3. **Country and sector research generation.** A planned feature in which the platform generates structured country and sector research briefs grounded in cited sources, attached to the engagement record.

4. **Information gap detection.** A planned feature in which the platform automatically identifies unanswered or weakly-answered questions and surfaces them as a checklist for follow-up with the client.

5. **Risk register.** A structured, editable risk register synthesized from flagged questionnaire fields and editable by the deal team. Currently, risks surface only in the briefing memo's consolidated section.

6. **Financial model templates.** Spreadsheet-format financial model templates tailored to the engagement's mandate, business model, and sub-industry. The first three templates are scheduled for the eighth week of the current build phase.

## Honest assessment of maturity

Querro is, today, a working version 1 of a deal advisory platform with a static question library and a deterministic memo compiler. It is functional end-to-end: a banker can sign up, create an engagement, fill out the structured questionnaire, generate a branded PDF briefing memo, and download it.

It is not yet a finished product. The composition engine that gives the architecture its leverage is being built right now. The downstream artifacts — research, gap analysis, risk register, financial models — are the next phase of the build. Pilot customer rollout is targeted for the third quarter of 2026, after the v2.0 build is feature-complete.

A reviewer evaluating the platform should treat the live site as a credible technical demonstration, not as a finished commercial product. The architectural and economic claims in the rest of this repository are claims about where the platform is going. The live site is evidence of the building capacity, not of the destination.

---

## Visual reference

Screenshots of the production environment, in order of the workflow they represent.

### Landing page

![Querro landing page hero](../screenshots/2026-04-26-landing-hero.png)

The public-facing entry point at [querro.app](https://querro.app), with the seven-frame interactive walkthrough below the fold.

![Interactive walkthrough frame](../screenshots/2026-04-26-landing-walkthrough.png)

### Engagement dashboard

![Dashboard with engagement cards](../screenshots/2026-04-26-dashboard.png)

The post-login dashboard. Each card represents one active engagement and routes to that engagement's structured workspace.

### Structured questionnaire — General section

![General section of an engagement](../screenshots/2026-04-26-engagement-general.png)

The first section of every engagement: company background, mandate basics, deal scope. Questions G1 through G20 are universal across all investment banking engagements in the current static library.

### Structured questionnaire — Operational section

![Operational section with sensitivity flagging](../screenshots/2026-04-26-engagement-operational.png)

The Operational section uses a kanban-card layout to keep long question sets readable. Sensitive questions carry a red border; concentration-risk questions auto-flag at threshold values.

### Adaptive question suggestions

![Adaptive question suggestion card](../screenshots/2026-04-26-adaptive-suggestion.png)

Mid-questionnaire, the platform surfaces follow-up questions tailored to answers already given. Each suggestion is accepted, edited, or dismissed by the user.

### Briefing memo generation

![Generate briefing modal](../screenshots/2026-04-26-generate-modal.png)

The deterministic compiler runs server-side, augmented by two bounded language model calls (executive summary, consolidated risks). End-to-end generation completes in under fifteen seconds for a typical engagement.

## Beyond version 1: features shipping ahead of this snapshot

This document was authored against the production state of April 25, 2026. The platform is in active development; some features described elsewhere in this repository as "in active development" have shipped during the days since this document was written. The screenshot below is one example.

### Sector Research

![Sector Research view](../screenshots/2026-04-26-sector-research.png)

A 25-question structured sector analysis organized across Global, Regional, and Country tabs, populated by Claude with web search and rendered with inline source citations. Each AI-generated answer carries an "AI Research — Edited" badge indicating user-reviewed status; sources are linked underneath each answer.

The screenshot is included here, slightly out of sync with the rest of this document, to give readers a direct view of where the platform is heading week by week. The [Roadmap](06-roadmap.md) describes the broader feature set still in flight.
