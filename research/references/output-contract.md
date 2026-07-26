# Output Contract: researcher

## Goal

Ensure research outputs are consistent, reusable, and easy to verify.

## Default Final Structure

Every substantial research answer should contain:

1. Executive summary
2. Findings
3. Recommendation
4. Contradictions and uncertainty
5. Revision log
6. Evidence table
7. Sources
8. Next-step handoff note when a downstream consumer is obvious
9. Stop / continue decision
10. Micro-validation when the recommendation can be tested

## Section Rules

### 1. Executive summary

- Short
- High signal
- No fake certainty
- Include the main recommendation only if the evidence supports it

### 2. Findings

- Organize by question or theme
- Use concrete claims
- Prefer comparisons and specifics over generic narrative

### 3. Recommendation

- State the recommended path
- Explain why it wins
- Name the biggest tradeoff
- If evidence is weak, say "tentative recommendation"

### 4. Contradictions and uncertainty

Must include:
- unresolved disagreements
- low-confidence areas
- missing data
- assumptions that shaped the answer

### 5. Revision log

Mandatory for deep research and verification passes. Optional for lightweight standard research unless the answer makes a strong recommendation.

Use a compact table:

- claim tested
- why it might be wrong
- counter-check performed
- result
- revision

The revision must be one of:
- kept
- narrowed
- downgraded
- reversed

If the critique loop changed the conclusion, reflect that change in the executive summary and recommendation, not only in this section.

### 6. Evidence table

Use a table with columns like:
- claim
- evidence
- source type
- confidence
- note

This table is mandatory for deep research and optional for lighter passes.

### 7. Sources

- Group by priority when helpful
- Prefer official/primary first
- Include links
- Avoid source spam

### 8. Next-step handoff note

- Optional for small answers
- Recommended for substantial research
- State what the next agent or operator should do with the result
- If constraints or excluded scope matter downstream, restate them briefly

### 9. Stop / continue decision

Mandatory for substantial decision-oriented research.

Choose one:
- **Stop** — evidence is sufficient to act and more research is unlikely to change the decision.
- **Continue narrowly** — one or two concrete gaps remain and could change the decision.
- **Continue broadly** — the framing, option set, or source coverage remains materially weak.
- **Do not conclude yet** — evidence is too weak, stale, contradictory, or unsupported.

Explain the evidence-based reason and what information would change the status.

### 10. Micro-validation

When the recommendation is testable, include:
- what to test
- how to test
- success signal
- failure signal
- decision after the test

The test should be the smallest practical action that can validate or falsify the recommendation.

## Intermediate Output Contract

Before the final report, the workflow may generate:
- research plan
- source list
- claim table
- critique questions
- counter-search notes
- revision log
- contradiction log
- evidence gap list
- constraint block
- competing-hypothesis table
- claim-source audit
- stop / continue decision
- micro-validation plan
- downstream handoff note

These are good intermediate artifacts and should be preferred over hidden reasoning.

## Failure Contract

If the evidence is not sufficient, do not return a polished but overconfident final answer.

Return one of:
- "insufficient evidence"
- "contradictory sources"
- "needs narrower scope"
- "needs primary-source confirmation"

And include the next best action.

If the self-critique loop exposes a better framing, return the reframed answer and name the changed framing explicitly.

## Tone Contract

- Clear
- Direct
- Evidence-first
- Minimal fluff
- No overstated certainty
