# Economic Impact

## What this document is for

This document examines the labor-market and productivity implications of platforms like Querro for the analyst-class workforce in professional services. It is written for readers — researchers, fellowship reviewers, policy analysts — who care less about whether a particular product succeeds commercially and more about what its trajectory implies for the economics of professional work.

The framing is honest about uncertainty. The empirical questions raised here cannot be answered from inside one company building one product. They can only be answered from outside, with longitudinal data across many firms over multiple years. What this document offers is a structured account of the mechanism by which a platform of this design changes the unit economics of a deal team, which tasks within that deal team are substituted or complemented, and the distributional effects that follow.

The author is the founder of the company being described. The document is written to invite scrutiny rather than to advocate. Where the founder's interest and the empirical question diverge, the document attempts to flag the divergence rather than paper over it.

## The labor structure of investment banking, briefly

A US middle-market investment banking deal team is typically organized in a four-tier hierarchy: analyst, associate, vice president, and managing director. Total compensation in 2025 base-plus-bonus terms ranges from approximately $130,000 to $180,000 fully loaded for first-year analysts, scaling to $400,000 to $700,000 for vice presidents and into seven figures for managing directors at top boutiques. Public Bureau of Labor Statistics data understates these figures because they aggregate across the broader securities industry; the more accurate references are the annual compensation surveys published by industry trade outlets and recruiting firms.

The hours structure is well-documented and largely unchanged in two decades. Junior bankers work eighty to one hundred hours per week. Roughly half of those hours are spent on tasks that have a clear template structure — pitchbook formatting, comparable-company spreads, basic financial-model maintenance, slide editing, due diligence checklist management, briefing memo drafting. The remainder is spent on judgment-bearing work, client interaction, and senior-banker support that is harder to template.

The empirical question that motivates Querro is whether platforms that capture, structure, and route deal information from the kickoff meeting through closing alter this labor mix, and if so, in which direction.

## A task-level decomposition of a kickoff workflow

Consider a single concrete workflow: the kickoff meeting and the briefing memo it produces. This is a small but representative slice of an analyst's job.

The current workflow, in the absence of structured intake software:

1. **Pre-meeting preparation.** A senior banker reviews available information about the client and writes a list of questions. Typical time: 30 to 90 minutes of senior banker time.
2. **Meeting itself.** The deal team meets with the client. Notes are taken in a Word document or by hand. Typical duration: 60 to 120 minutes of full team time, often four to six people.
3. **Post-meeting reconstruction.** An analyst converts notes into a structured internal document. Typical time: 4 to 8 hours of analyst time.
4. **Gap identification.** A senior banker reviews the document, identifies missing information, and assigns the analyst follow-up questions to send to the client. Typical time: 30 to 60 minutes of senior banker time, plus several hours of analyst time spent emailing the client and updating the document.
5. **Briefing memo drafting.** An analyst converts the structured document into a formal briefing memo, formatted to firm standards. Typical time: 6 to 12 hours of analyst time, often spread across two days as the document goes through internal review.

The total analyst time consumed by this single workflow is approximately 12 to 24 hours. Across a deal team running concurrent engagements, this aggregates rapidly: an analyst at a firm running three concurrent deals may spend a meaningful fraction of their workweek on kickoff-cycle tasks alone.

The same workflow on a platform of Querro's design:

1. **Pre-meeting preparation.** The senior banker selects the engagement's mandate and segment dimensions. The platform produces a tailored question set automatically. Typical time: 5 to 15 minutes of senior banker time.
2. **Meeting itself.** The deal team enters answers into the platform during the meeting itself. Notes are structured by construction; there is no separate transcription step. Duration is comparable to the current workflow.
3. **Post-meeting reconstruction.** None. The structured record is complete at the meeting's end.
4. **Gap identification.** The platform identifies unanswered or weakly-answered questions automatically and surfaces them as a follow-up checklist. Typical time: 10 to 20 minutes of analyst time to refine and send.
5. **Briefing memo drafting.** The platform generates a complete branded briefing memo from the structured record in under fifteen seconds. The analyst reviews and refines. Typical time: 1 to 2 hours of analyst time.

The total analyst time consumed by the same workflow drops to approximately 1.5 to 3 hours, a reduction of roughly 80 to 90 percent on this slice. The reduction is not uniform across all of the analyst's tasks — many other tasks remain unchanged — but on the specific kickoff-and-briefing slice, the change is large.

## Where the freed time goes

The interesting question is not whether the time is freed. The interesting question is what happens to it.

There are three possibilities, each with different distributional consequences.

**Possibility A — The time is reabsorbed into more deals.** A boutique that was running three concurrent deals per banker now runs four or five. Analyst headcount stays constant; throughput rises. The labor demand for analysts is preserved or increases; the productivity of each analyst rises; the firm captures more revenue per banker. This is the outcome that aligns most closely with the founder's commercial interest and is the outcome that historical productivity-shock literature tends to predict for industries with elastic demand for the underlying service.

**Possibility B — The time is reabsorbed into higher-judgment tasks.** Analyst headcount stays constant; the work shifts toward client interaction, deal structuring, and senior-banker support that previously the analyst had no bandwidth for. The job at the analyst level changes substantively: less templating, more judgment. Career progression accelerates because earlier exposure to judgment-bearing work compresses the time-to-vice-president.

**Possibility C — The time is recovered as labor cost reduction.** A boutique that was hiring four analysts per year hires three, or hires the same four but extends their time-to-promotion to compensate for slower revenue growth. This is the outcome the labor-displacement literature focuses on; it is also the outcome that platform vendors typically downplay in their sales materials.

The honest answer is that all three happen, in different mixes at different firms, depending on the firm's growth posture, capital allocation, and culture. The empirical question — what the actual mix is, longitudinally, across firms adopting platforms of this design — cannot be answered from a single product's deployment data. It requires the kind of cross-firm panel analysis that economists working in this space are positioned to conduct.

## What is substituted, what is complemented

A useful framing borrowed from the recent labor-AI literature is to ask, at task level, which tasks the platform substitutes for human labor and which tasks it complements human labor on.

Tasks Querro substitutes for:

- Generating, customizing, and maintaining kickoff question lists. This was previously a senior banker task.
- Transcribing meeting notes into structured form. This was previously an analyst task.
- Drafting the body of standard professional documents like briefing memos and risk registers, where the content is a transformation of structured fields. This was previously an analyst task.
- Cross-referencing answers across sections to surface concentration risks and information gaps. This was previously an analyst task done imperfectly under time pressure.

Tasks Querro complements:

- Reviewing AI-generated executive summaries and risk narratives. The reviewer must be expert enough to catch errors; the platform raises the leverage of that expertise rather than replacing it.
- Conducting the kickoff meeting itself. The platform structures the conversation but does not run it. The senior banker's relationship with the client and judgment about which non-templated questions to ask remain primary.
- Synthesizing the briefing memo into a recommendation. The memo presents structured facts; the recommendation that follows is human judgment that the platform makes more efficient but does not produce.
- Building the financial model. The platform produces a tailored template; the assumptions and the final valuation judgment are human.

The pattern is consistent with a broader hypothesis in recent task-level AI labor research: AI substitutes most reliably for tasks that have a clear structural template and complements most reliably for tasks that require judgment, relationships, or accountability. Querro is, in a sense, an attempt to push as much of an analyst's workflow into the substitutable category as possible, while leaving the complementary tasks intact and making them more leveraged.

## Distributional effects

Within the analyst-to-managing-director hierarchy, the productivity gain is not distributed evenly.

**Junior analysts** absorb the largest task substitution. Tasks that previously consumed half of their week are largely automated. The junior role survives but changes substantively, and the marginal value of the junior hire becomes more sensitive to their judgment quality than to their template-execution quality. Hiring filters at boutique firms may shift toward candidates who demonstrate judgment earlier; this could be a leveling force (less reliance on which university the candidate attended for templating tasks) or a sorting force (more reliance on judgment which is harder to interview for and may correlate with social class). Which direction dominates is an empirical question.

**Associates and vice presidents** see less direct substitution because their work is already weighted toward judgment. They benefit primarily through the leverage effect — the same VP can supervise more concurrent engagements because the analyst review burden per engagement falls. Their compensation should rise faster than analyst compensation under platforms of this design.

**Managing directors** are the largest beneficiaries in absolute terms. Their work is already almost entirely judgment and relationships; platforms like Querro do not substitute for any of it but make every junior person on their teams more productive. The implicit revenue per managing director rises.

The distributional implication, taken honestly, is that platforms like Querro plausibly widen the within-firm compensation distribution. The bottom of the analyst tier gains in capability but is more easily substituted; the top of the firm captures most of the productivity surplus. This is not a unique pattern in the broader AI-labor literature, but it is worth naming explicitly rather than letting the platform vendor narrative — "we just save analysts time so they can do better work" — quietly elide it.

## What the founder believes, separately from what the data will show

The founder's prior, stated separately from the empirical claims above, is that Possibility A — time is reabsorbed into more deals — dominates in the US middle-market segment over the first three to five years of platform adoption, because the segment has been throughput-constrained for over a decade and would readily absorb capacity. Possibility C — labor cost reduction — becomes more visible in later years and in adjacent segments where deal volume is less elastic, particularly in legal advisory and audit.

The founder also believes — and this is opinion, not analysis — that the more interesting effect of platforms like Querro is not on the headline employment numbers but on the apprenticeship structure of professional services. The traditional career path in investment banking, law, and consulting trades two-to-four years of templating work for a structured exposure to deal flow that produces senior judgment. If templating disappears, the apprenticeship has to be redesigned; if it is not redesigned, the supply of senior judgment a decade out is jeopardized. This is a question worth research attention regardless of where any individual platform's commercial trajectory lands.

## What this document does not claim

It does not claim that Querro will, in fact, be widely adopted. Adoption depends on a long list of commercial factors that the architecture and the labor analysis do not determine.

It does not claim that the productivity gains described here generalize to professions outside investment banking. The architecture is portable; whether the labor effects replicate in law, audit, or consulting is an empirical question that requires its own evidence base.

It does not claim that platforms of this design are net welfare-improving. Welfare depends on the distribution of the gains, the externalities to client outcomes, and the second-order effects on the apprenticeship pipeline. The case can be made; it has not yet been demonstrated.

The document's purpose is to set up the empirical questions cleanly enough that a researcher external to the company can engage with them. The questions matter beyond Querro. The answers, when they arrive, will not come from Querro alone.
