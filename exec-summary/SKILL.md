---
name: exec-summary
description: Write a short, evidence-backed executive summary of an analysis, investigation, incident, or decision. Use when the user asks for an executive summary, TLDR, short wrap-up, or brief for a decision-maker.
---

# Executive summary

Turn detailed work into a one-screen summary for a reader who did not follow it. Give the answer, the supporting evidence, and the next decision.

## Before writing

- Identify the reader and the decision or response they need.
- Check the original evidence for the required questions. An earlier AI summary is not an independent source.
- If a missing answer could change the decision, label the summary `INTERIM`. State the impact and the next evidence check. A short summary does not make unfinished analysis complete.

## Writing rules

1. Lead with the result or recommendation and its business implication. Distinguish a proposed action from an approved decision.
2. Keep prose to about six lines before the diagram. Cut the investigation timeline, generic introductions, and repeated conclusions. Link to detail when needed.
3. Put a source and measurement period beside each key number. Include the denominator or cohort needed to interpret a rate. Label estimates with their basis.
4. Separate confirmed findings, signals, and hypotheses. Claim causality only when supported. Preserve source disagreements that affect the decision.
5. Include a compact ASCII chain showing evidence -> supported conclusion -> proposed or approved decision. Keep sources next to the prose they support. No other skill is required.
6. Close with a specific ask when action is needed. Use known owners and dates. If they are unknown, ask to agree them instead of inventing commitments.
7. Match the user's language and the reader's familiarity with the topic. Use plain text, without bold formatting or semicolons.

For a shareable document, use `[DRAFT]` until its human owner approves it. Human approval and analytical completeness are separate: a decision-changing evidence gap still requires `INTERIM`.

## Template

```text
# [DRAFT] Executive summary: <topic>

<Result or recommendation and business implication.>
<Key evidence with source, period, and denominator where relevant.>
<Decision-changing limitation or disagreement, if any.>

<Evidence> -> <Supported conclusion> -> <Proposed / approved decision>
                                      ^
                         <Decision-changing caveat, if any>

<Specific ask, known owner, and known deadline or next checkpoint.>
```

A direct chat response does not need a document title. Omit empty template lines. The diagram shows the evidence-to-decision rationale, not a transcript of internal reasoning.
