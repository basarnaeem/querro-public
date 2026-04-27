# AI Philosophy

## The principle

Querro uses AI deliberately, in narrow places, with auditable boundaries. This document describes where AI is invoked, where it is explicitly not invoked, how the system validates AI outputs, and the reasoning behind each choice.

The guiding principle is that the cost of an incorrect AI-generated number, citation, or claim in a deal document is significantly higher than the cost of writing a deterministic compiler. A wrong figure in a briefing memo for a $400 million transaction is not a usability problem; it is a reputational and legal problem for the firm using the tool. The architecture is built around this asymmetry.

This puts Querro in a different posture from chat-first AI products. The platform's value comes from structure first and AI second. Removing every AI feature from Querro tomorrow would degrade the product but would not break it. Removing the structured engagement record, the dynamic question engine, or the deterministic document compiler would break it entirely.

## Where AI is used

There are exactly four places in the production system where a language model is invoked. Each is described below with the rationale for using AI rather than a deterministic alternative.

### 1. Adaptive question suggestions

When a user is filling out the structured questionnaire and provides an answer that opens new lines of inquiry — for example, a target company described as having recently completed a major acquisition — the system surfaces follow-up questions that were not part of the base questionnaire.

**Why AI here.** The space of possible follow-up questions is too large and too context-dependent to enumerate in advance. Language models are good at this kind of contextual extension.

**Constraint.** Adaptive questions are surfaced as suggestions, not silently appended. The user accepts, edits, or dismisses each one. Suggestions are tagged in the database so that good ones can be promoted into the permanent question library through review.

**Failure mode.** A bad suggestion costs the user a few seconds of dismissal. There is no downstream consequence because rejected suggestions never enter the engagement record.

### 2. Briefing memo executive summary

The platform compiles a professional briefing memo from the structured engagement record. The bulk of this memo is assembled deterministically: company facts come from labeled fields, the risk register comes from flagged answers, the deal structure comes from typed inputs. AI is invoked for one section: the executive summary.

**Why AI here.** Executive summaries require natural-language synthesis of facts that are scattered across many fields and need to be presented in coherent prose with appropriate emphasis.

**Constraint.** The executive summary is generated from a fixed budget of input tokens drawn from labeled engagement fields. The model does not have free access to the user's documents or unbounded context. Output is bounded to roughly six hundred tokens. The user reviews and can regenerate, edit, or replace.

**Failure mode.** A weak or generic summary is visible immediately on review and can be regenerated or rewritten. The summary is the only AI-touched section of the memo, so review attention is concentrated where it matters.

### 3. Briefing memo consolidated risk section

The same memo includes a consolidated risk section that synthesizes risks flagged across the operational, financial, legal, and HR sections of the questionnaire into a coherent narrative.

**Why AI here.** Individual flagged risks are captured deterministically as structured fields. But weaving them into a prose narrative — connecting a customer concentration risk to a working-capital risk to a key-person-dependency risk — is a synthesis task.

**Constraint.** The model receives only the structured risk fields, not the underlying free-text answers. It cannot invent risks; it can only articulate the ones the structured data has already flagged. Output is bounded to roughly eight hundred tokens.

**Failure mode.** A weak narrative is visible on review. A hallucinated risk would be detectable because it would not correspond to any flagged structured field.

### 4. Document tagging and pre-fill

The Documents section of the platform accepts uploaded source materials — pitchbooks, financials, prior board decks, regulatory filings — and uses AI to extract structured information from them, mapped to the question schema for the engagement.

**Why AI here.** Document parsing across heterogeneous formats (scanned PDFs, native PDFs, slide decks) and extracting the right fields into the right slots is a task that language models now do reliably enough to be useful, where rule-based parsers cannot generalize.

**Constraint.** Documents are stored page-by-page. Each extracted answer is tagged with a citation pointing to the specific page it came from. The user reviews each pre-filled answer before it is committed to the engagement record. No answer enters the record without explicit user confirmation.

**Failure mode.** A misextracted answer is rejected by the user at the review stage. A hallucinated answer that is not anchored to a real page citation is detectable because the citation will not resolve.

## Where AI is explicitly not used

The following parts of the system are entirely deterministic by design.

**The composition of the questionnaire.** Given an engagement's configuration across the five context dimensions and a frozen library version, the questionnaire is fully reproducible. There is no language model involved in deciding which questions to ask. Two deal teams running kickoffs on similar engagements receive comparable questionnaires so that the resulting structured records can be compared, benchmarked, and used to improve the library. Stochastic question generation breaks this.

**The body of the briefing memo.** Sections of the briefing memo other than the executive summary and the consolidated risk narrative are rendered from structured fields by a deterministic compiler. Numbers come from typed numeric inputs, not from text generation. A user who reads a Querro briefing memo can trust that every number in it corresponds to a structured field they or their team entered.

**Financial model values.** The financial model templates produced by the platform are populated from the structured engagement record by deterministic mapping into spreadsheet templates. AI does not generate forecasts. AI does not generate assumptions. The user enters the assumptions; the template does the math.

**Routing of structured fields to outputs.** Which question feeds which section of which output is a deterministic mapping defined in the content library. AI is not used to decide where an answer should appear in a credit memo. The mapping is authored, versioned, and reviewable.

## How AI outputs are validated

Every AI feature in Querro is tested against five categories of failure, each with its own mitigation and observability signal.

**Category 1 — Factual fabrication.** The model produces a claim, number, or entity that does not appear in the inputs. This is the highest-severity category. Mitigation: every AI feature restricts the model's input to bounded structured fields. Where free-text input is necessary (the document pre-fill case), every output is tagged with a citation that must resolve to a real source. Observability: an automated post-generation validator checks every numeric and named entity against source structured fields; outputs with unsourced numbers are rejected and regenerated.

**Category 2 — Citation drift.** The model produces a claim that is technically supported by the input but cites the wrong source. Mitigation: each input field carries a stable identifier; the model is instructed to name the source identifier for each claim; a post-generation step validates that the named source actually contains the claimed information.

**Category 3 — Coverage failure.** The model omits a claim that should have been included — for example, a flagged risk that does not appear in the consolidated risk section. Mitigation: the set of flagged risks is computed deterministically and given to the model as input; a post-generation validator confirms that every input risk appears in the output narrative.

**Category 4 — Tone and register failure.** The model produces output that is factually correct but stylistically wrong for a deal document — too casual, too verbose, or formatted inconsistently with the rest of the memo. Mitigation: output style is controlled by a fixed system instruction and examples from a curated set of approved memo sections. Observability: if a user regenerates the same section more than once, the regeneration cause is logged and reviewed.

**Category 5 — Confidence calibration failure.** The model produces output that asserts something with implicit confidence that the underlying data does not support. Mitigation: confidence-bearing fields (verification flags, sensitivity flags, "to be confirmed" markers) are passed to the model as explicit signals; the output template requires their preservation.

Three evaluation methods run in parallel, in increasing order of engineering investment: universal human review on every AI output before it commits to the engagement record; automated post-generation validation of structured properties (sourced numbers, cited identifiers, coverage, uncertainty preservation); and a held-out engagement evaluation set being assembled from historical deal experience for regression testing against prompt or model changes.

## Model selection

All production AI calls use the current Claude Sonnet model from Anthropic's Claude API, with no training on user data per Anthropic's commercial terms. Sonnet was selected because the latency and cost profile is appropriate for production-volume calls and because the quality is sufficient at the bounded output sizes the platform requires.

## Why not a more agentic architecture

Industry framing in 2025 and 2026 has converged heavily on agent and multi-agent architectures. Querro is deliberately not built this way. Three reasons.

**Reasoning length is not the bottleneck.** The bottleneck in deal advisory is not "the AI did not think long enough." It is "the right structured information was never captured in the first place." Adding agentic reasoning on top of incomplete data does not help.

**Auditability degrades with each additional call.** A workflow with one bounded AI call and structured inputs is auditable. A workflow with five AI calls passing intermediate results to each other is not. In a regulated workflow, this matters.

**Cost compounds non-linearly.** Multi-agent systems trade exponentially more tokens for marginal quality improvements on tasks that are not actually language-bound.

This is a position, not a permanent commitment. If a specific feature emerges where multi-call coordination is genuinely the right tool — deep research over many documents with cross-referencing — it will be built. But the default architecture is one structured input, one bounded model call, one auditable output.

## The feature bar

Every proposed AI feature must answer four questions before being built.

1. **What is the deterministic alternative?** If structured fields and a compiler can produce the output, that is the default. AI is invoked only when natural-language synthesis genuinely outperforms the deterministic alternative on quality.

2. **What is the failure mode?** What happens when the model produces a wrong, irrelevant, or hallucinated output? If the answer involves a number landing in a deal document, the feature does not ship until the failure is mitigated.

3. **Where is the human in the loop?** Every AI output that affects the engagement record passes through a human review step. There are no silent AI writes to engagement state.

4. **How is the output bounded?** Token budgets, structured output formats, and field-level constraints reduce the space the model can produce something wrong in.

A feature that cannot clear all four does not ship.
