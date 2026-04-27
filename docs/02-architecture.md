# Architecture

## The problem the architecture solves

Every professional services deal sits at the intersection of several independent contextual axes. A sell-side M&A engagement for a Texas regional bank with a Shariah-compliant capital structure and a public listing is not a generic deal. The questions a banker should ask, the regulatory frameworks that apply, the financial model that makes sense, and the risk register that matters all change with each axis.

If a software platform tries to handle this with hand-crafted templates, the combinatorial explosion is fatal. With eight mandate types, forty-nine business models, one hundred sixty-three sub-industries, twelve priority jurisdictions, and twelve special-situation modes, the number of possible context combinations is on the order of **eighty million**. No content team, regardless of size, can author and maintain eighty million tailored questionnaires.

If the platform instead handles this with a single generic template and lets users edit it, the result is the status quo: a Word document checklist that captures nothing useful and degrades engagement quality across the firm.

The architectural problem is therefore: how do we deliver a questionnaire — and downstream, a financial model template, a risk register, a research brief — that feels hand-crafted for the specific deal, while authoring and maintaining only a small, finite number of artifacts?

## The five-dimensional context model

Querro defines every engagement segment as a point in a five-dimensional context space. Each dimension is locked: there are five and there will only ever be five. Options grow within dimensions; the dimension list never grows.

| # | Dimension | What it captures | Cardinality | Initial scale |
|---|-----------|------------------|-------------|---------------|
| 1 | Mandate | The deal type — what is being executed | One per engagement | 8 in production for investment banking, expanding to ~40 across professions |
| 2 | Business model | The economic structure of the target — how it makes money | One per segment | 49 categories |
| 3 | Sub-industry | The terminology, peer set, and specific competitive dynamics | One per segment | 163, aligned with GICS sub-industry classification |
| 4 | Jurisdiction | The regulatory and legal environment, captured at country granularity | Multi-valued per segment | 12 priority countries, expanding to all major markets |
| 5 | State modes | Special situations that override or augment the default question set — distress, carve-out, family-owned, employee-owned, Shariah-compliant, public listed, pre-revenue, acquisition vehicle, greenfield, state-owned, joint venture, privatization | Multi-valued per segment | 12 modes |

The five-dimension lock is a deliberate constraint, not an accident of incomplete design. Every requirement that initially appears to need a sixth dimension — geography sub-regions, deal size tiers, client type, transaction structure — has been examined and resolved into one of the existing five. The discipline is what keeps the system tractable.

A real engagement may contain multiple segments. A holding company with a banking subsidiary, an asset management subsidiary, and a real estate subsidiary is one mandate but three segments, each with its own business model, sub-industry, jurisdictions, and active state modes. The composition runs once per segment and the results are unioned for the engagement.

## The modular library

The platform's intelligence does not live in code. It lives in a versioned content library of small, independent artifacts. Each artifact owns exactly one concern.

There are six artifact types in the library, and there will only ever be six.

1. **Profession-level base content** — the universal questions, terminology, and structure for an entire profession (investment banking, law, audit, consulting). One per profession.

2. **Mandate-specific content** — questions, financial model inputs, and section structure that change with the mandate type. Eight in production for investment banking.

3. **Business model content** — questions and economic-structure logic that change with how the target firm makes money. Forty-nine in scope.

4. **Sub-industry content** — terminology variables, peer firm sets, and regulator names that change with the sub-industry. One hundred sixty-three in scope, aligned to a public industry classification standard.

5. **Jurisdiction content** — regulatory frameworks, accounting standards, tax regimes, and country-specific questions. Twelve priority countries to start.

6. **State-mode content** — contextual question blocks and modifications that activate when special situations apply.

The combinatorial math:

> 1 base + 8 mandates + 49 business models + 163 sub-industries + 12 jurisdictions + 12 state modes = **245 artifacts** that compose at runtime into approximately 80 million possible engagement variants.

Each artifact is small enough to be authored and reviewed by one domain expert in a single sitting. The content library can be maintained at scale by a small team of senior practitioners, not an engineering department.

## Composition at runtime

When a user creates an engagement and configures its segments, the platform composes the questionnaire by loading the relevant artifacts and merging them according to a deterministic rule set. The output is a tailored question set with full provenance — every question is tagged with which artifact contributed it, which made it visible, and which substituted its terminology. This metadata is invisible in the user interface but available to administrators for debugging and to the audit trail for compliance.

Composition produces three concrete things, all derived from the same context vector:

- A **tailored questionnaire** for the kickoff meeting
- A **document tag schema** for the Documents section, used to route uploaded files to the questions they pre-fill
- A **financial model configuration** identifying which output schedules apply (a sell-side M&A on a regional bank produces different model outputs than an IPO on a SaaS company)

The composition is cached per engagement to keep the user interface fast. Cache invalidation occurs when the underlying library version changes or when a user edits the engagement's segment configuration.

## Library versioning and engagement freezing

The content library is versioned. When an artifact is updated — a new question added, a regulatory framework amended, a sub-industry's terminology refined — the library version increments.

In-flight engagements **do not** automatically pick up new library versions. An engagement freezes its library version at the moment it is created, ensuring that a deal team running a kickoff meeting in May 2026 does not have new questions appear underneath them in June. Users who want to refresh an in-flight engagement to the latest library version do so explicitly, with a single action that recomposes the questionnaire and surfaces any new questions for review.

This behavior is a deliberate choice borrowed from how documents-of-record systems handle revision control: in-flight work is immutable; deliberate refresh is a separate operation.

## Why this architecture, and not the alternatives

**Why not a single generic questionnaire?** Because the variance across deal types, industries, and special situations is the entire point of the product. A generic questionnaire reproduces the broken status quo.

**Why not hand-crafted per-mandate templates?** Because the combinatorial space is eighty million, and any template strategy collapses into either too few templates (and missed nuance) or too many (and unmaintainable content debt).

**Why not generate questions on demand from a language model?** Because deal-grade questionnaires need exactly the same wording across every Texas regional bank engagement to enable downstream comparison, peer benchmarking, and library improvement. Stochastic generation breaks this. Composition is deterministic; the same context vector produces the same questionnaire every time.

**Why not a graph database or rules engine?** Considered. The five-dimensional structure is a flat, well-bounded combinatorial space. A graph or rules engine adds complexity without solving any problem the simpler architecture cannot. Improvements to the system happen by editing artifacts, not by reorganizing the engine.

## What this architecture commits the company to

Three forward-looking implications follow from the architecture as designed.

**The library, not the engine, is the moat.** A competitor who replicates the engine in three months still does not have the content library, which encodes thousands of senior-practitioner hours of domain expertise. Every completed engagement informs library improvements that propagate to all future engagements in that combination. The engine is software; the library is institutional memory.

**Adding professions is content, not engineering.** Extending Querro from investment banking into law, audit, or consulting requires authoring a new profession base and the corresponding mandate set. The engine, the schema, the composition rules, and the user interface do not change. This is what enables the platform's long-run vision of becoming an operating system for every professional engagement, not just deal advisory.

**Determinism is permanent.** The composition output is fully reproducible. Given the same engagement configuration and library version, the same questionnaire, document schema, and model configuration are produced every time. This is a non-negotiable property; it is what makes the system auditable, testable, and trustworthy in regulated workflows.

## What this document does not contain

Internal artifact identifiers, the JSON schema of any artifact type, the merge precedence rules, the variable substitution syntax, the cache invalidation algorithm, and the library version format are intentionally omitted. They are proprietary implementation details. Readers who need this level of depth — investors who have signed term sheets, customers under pilot agreement, prospective senior engineering hires — can request access through the channels in [CONTRIBUTING.md](../CONTRIBUTING.md).
