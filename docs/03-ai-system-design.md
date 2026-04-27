# AI System Design

## The principle

Querro uses AI deliberately, in narrow places, with auditable boundaries. This document describes where AI is invoked, where it is explicitly not invoked, and the reasoning behind each choice.

The guiding principle is that the cost of an incorrect AI-generated number, citation, or claim in a deal document is significantly higher than the cost of writing a deterministic compiler. A wrong figure in a briefing memo for a $400 million transaction is not a usability problem; it is a reputational and legal problem for the firm using the tool. The architecture is built around this asymmetry.

This puts Querro in a different posture from chat-first AI products. The platform's value comes from structure first and AI second. Removing every AI feature from Querro tomorrow would degrade the product but would not break it. Removing the structured engagement record, the composition engine, or the deterministic document compiler would break it entirely.

## Where AI is used

There are exactly four places in the production system where a language model is invoked. Each is described below with the rationale for using AI rather than a deterministic alternative.

### 1. Adaptive question suggestions

When a user is filling out the structured questionnaire and provides an answer that opens new lines of inquiry — for example, a target company that is described as having recently completed a major acquisition — the system can surface follow-up questions that were not part of the base questionnaire.

**Why AI here.** The space of possible follow-up questions is too large and too context-dependent to enumerate in advance. A regex over answer text is brittle; a hand-authored decision tree would require thousands of branches. Language models are good at this kind of contextual extension.

**Constraint.** Adaptive questions are surfaced as suggestions, not silently appended. The user accepts, edits, or dismisses each one. The user is always in the loop. Suggestions are tagged in the database so that good ones can be promoted into the permanent question library through review.

**Failure mode.** A bad suggestion costs the user a few seconds of dismissal. There is no downstream consequence because rejected suggestions never enter the engagement record.

### 2. Briefing memo executive summary

The platform compiles a professional briefing memo from the structured engagement record. The bulk of this memo is assembled deterministically: company facts come from labeled fields, the risk register comes from flagged answers, the deal structure comes from typed inputs. AI is invoked for one section: the executive summary.

**Why AI here.** Executive summaries require natural-language synthesis of facts that are scattered across many fields and need to be presented in coherent prose with appropriate emphasis. This is exactly what language models are good at.

**Constraint.** The executive summary is generated from a fixed budget of input tokens drawn from labeled engagement fields. The model does not have free access to the user's documents or unbounded context. Output is bounded to roughly six hundred tokens. The user reviews and can regenerate, edit, or replace.

**Failure mode.** A weak or generic summary is visible immediately on review and can be regenerated or rewritten. The summary is the only AI-touched section of the memo, so review attention is concentrated where it matters.

### 3. Briefing memo consolidated risk section

The same memo includes a consolidated risk section that synthesizes risks flagged across the operational, financial, legal, and HR sections of the questionnaire into a coherent narrative.

**Why AI here.** Individual flagged risks are captured deterministically as structured fields. But weaving them into a prose narrative — connecting a customer concentration risk to a working-capital risk to a key-person-dependency risk — is a synthesis task. Language models do this well.

**Constraint.** The model receives only the structured risk fields, not the underlying free-text answers. It cannot invent risks; it can only articulate the ones the structured data has already flagged. Output is bounded to roughly eight hundred tokens.

**Failure mode.** A weak narrative is visible on review. A hallucinated risk would be detectable because it would not correspond to any flagged structured field; the user can audit which structured field generated which sentence.

### 4. Document tagging and pre-fill (in development)

The Documents section of the platform, in active development, accepts uploaded source materials — pitchbooks, financials, prior board decks, regulatory filings — and uses AI to extract structured information from them, mapped to the question schema for the engagement.

**Why AI here.** Document parsing across heterogeneous formats (scanned PDFs, native PDFs, slide decks, Excel files) and extracting the right fields into the right slots is a task that language models with vision capabilities now do reliably enough to be useful, where rule-based parsers cannot generalize.

**Constraint.** Documents are stored page-by-page. Each extracted answer is tagged with a citation pointing to the specific page (and where possible the specific region) it came from. The user reviews each pre-filled answer before it is committed to the engagement record. No answer enters the record without explicit user confirmation.

**Failure mode.** A misextracted answer is rejected by the user at the review stage. A hallucinated answer that is not anchored to a real page citation is detectable because the citation will not resolve.

## Where AI is explicitly not used

The following parts of the system are entirely deterministic by design.

### The composition of the questionnaire

Given an engagement's configuration across the five context dimensions and a frozen library version, the questionnaire is fully reproducible. The same input always produces the same output. There is no language model involved in deciding which questions to ask.

This is a hard requirement. Two different deal teams running kickoffs on similar engagements need to receive comparable questionnaires so that the resulting structured records can be compared, benchmarked, and used to improve the library. Stochastic question generation breaks this comparison.

### The body of the briefing memo

Sections of the briefing memo other than the executive summary and the consolidated risk narrative are rendered from structured fields by a deterministic compiler. Numbers come from typed numeric inputs, not from text generation. Tables are assembled from labeled rows. Section headings are fixed. Formatting is template-driven.

A user who reads a Querro briefing memo can trust that every number in it corresponds to a structured field they or their team entered. There is no number in the memo that was hallucinated by a model.

### Financial model values

The financial model templates produced by the platform — projections, valuations, sensitivity tables, capital structures — are populated from the structured engagement record by deterministic mapping into spreadsheet templates. AI does not generate forecasts. AI does not generate assumptions. The user enters the assumptions; the template does the math.

This is the most important boundary in the system. Generating financial model values with a language model is a category of error that no current model is reliable enough to ship into a regulated workflow.

### Routing of structured fields to outputs

Which question feeds which section of which output is a deterministic mapping defined in the content library. AI is not used to decide where an answer to question seventeen should appear in a credit memo. The mapping is authored, versioned, and reviewable.

## Model selection

All production AI calls use a current frontier model from Anthropic's Claude Sonnet family, accessed through the Anthropic API with no training on user data per Anthropic's commercial terms. Sonnet was selected for the four use cases above because the latency and cost profile is appropriate for production-volume calls and because the quality is sufficient at the bounded output sizes the platform requires. Larger Anthropic models are reserved for separate use cases — internal content authoring, evaluation runs — that do not run on the production hot path.

The choice of one provider for all production AI calls is deliberate. Multi-provider routing would add operational complexity that does not pay off until volume is significantly higher than current.

## Why this design rather than a more agentic one

Industry framing in 2025 and 2026 has converged heavily on **agent** and **multi-agent** architectures, where multiple language model calls coordinate to perform a task. Querro is deliberately not built this way. Three reasons.

**Reasoning length is not the bottleneck.** The bottleneck in deal advisory is not "the AI did not think long enough." It is "the right structured information was never captured in the first place." Adding agentic reasoning on top of incomplete data does not help. Capturing the data well does help.

**Auditability degrades with each additional call.** A workflow with one bounded AI call and structured inputs is auditable. A workflow with five AI calls passing intermediate results to each other is not. In a regulated workflow, this matters.

**Cost compounds non-linearly.** Multi-agent systems trade exponentially more tokens for marginal quality improvements on tasks that are not actually language-bound. The economic argument does not work for this product at this stage.

This is a position, not a permanent commitment. If a specific feature emerges in the future where multi-call coordination is genuinely the right tool — for example, deep research over many documents with cross-referencing — it will be built. But the default architecture is one structured input, one bounded model call, one auditable output.

## What an AI feature must clear to ship

Every proposed AI feature in Querro must answer four questions before being built. This is the internal review checklist.

1. **What is the deterministic alternative?** If structured fields and a compiler can produce the output, that is the default. AI is invoked only when natural-language synthesis genuinely outperforms the deterministic alternative on quality.

2. **What is the failure mode?** What happens when the model produces a wrong, irrelevant, or hallucinated output? If the answer involves a number landing in a deal document or a citation pointing at a real page that does not exist, the feature does not ship until the failure is mitigated.

3. **Where is the human in the loop?** Every AI output that affects the engagement record passes through a human review step. There are no silent AI writes to engagement state.

4. **How is the output bounded?** Token budgets, structured output formats, and field-level constraints reduce the space the model can produce something wrong in. Free-form generation into important fields is avoided.

A feature that cannot clear all four does not ship.
