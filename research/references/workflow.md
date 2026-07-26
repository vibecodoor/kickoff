# Workflow: researcher

## Goal

Run a rigorous research workflow that produces trustworthy, reusable outputs by combining evidence collection with an explicit self-critique and revision pass.

## Step 1 — Clarify the Task

- Restate the research objective in one sentence.
- Identify the research type:
  - technical
  - market
  - competitor
  - OSS landscape
  - verification
- If scope is ambiguous, ask only the smallest clarifying question needed.
- If asking is not necessary, continue with explicit assumptions.
- Preserve:
  - fixed constraints
  - flexible assumptions
  - excluded scope

## Step 2 — Define the Research Plan

Before heavy browsing, write a short plan that includes:
- target question
- decision needed
- evaluation criteria
- sub-questions
- inclusion / exclusion rules
- likely source buckets
- risk level
- stop condition
- expected deliverable
- downstream consumer if one is obvious

Do not skip this step for deep research.

For Deep research, read `orchestration.md` and select only the tracks that can change the decision. Parallelize independent tracks when real workers are available.

## Step 3 — Gather Sources

Collect sources in explicit buckets:
- primary / official
- primary-adjacent
- secondary analysis
- community signal

Start with the smallest high-signal set. Expand only if needed.

For broad topics, it is acceptable to split research by dimension:
- stack
- architecture
- pitfalls
- alternatives

Then synthesize later.

## Step 4 — Extract Evidence

For each important claim, capture:
- claim
- evidence
- source
- source type
- date if relevant
- confidence / caveat
- whether it drives the recommendation

Prefer a claim table during intermediate work over freeform prose.

For large or multi-worker research, assign stable IDs to claims and sources so evidence can be merged without repeating the full context.

## Step 4A — Compare Competing Hypotheses

When framing or recommendation is uncertain, maintain a compact live set:
- H1: the initial hypothesis is correct
- H2: an alternative option or explanation is better
- H3: the problem is framed incorrectly
- H4: evidence is insufficient

Map decision-relevant evidence against these hypotheses. Eliminate or narrow hypotheses as evidence accumulates. Skip this artifact for straightforward factual verification where it adds no discrimination.

## Step 5 — Run the Self-Critique Loop

Use this loop before final synthesis whenever:
- the mode is deep research or verification pass
- the answer contains a strong recommendation
- the key conclusion depends on a small number of sources
- the topic is contested, fast-changing, or high-impact

For standard research, keep the loop compact. For deep research and verification, make it visible in the final report.

### 5A. Select Load-Bearing Claims

Pick the claims that would materially change the answer if wrong:
- recommendation drivers
- factual claims about current state, pricing, features, legality, benchmarks, adoption, or safety
- comparisons that rank one option above another
- assumptions imported from secondary sources

Do not waste the loop on background facts that do not affect the decision.

### 5B. Generate Critique Questions

For each selected claim, ask:
- What would make this false?
- What would make this only partly true?
- What source would be authoritative enough to settle it?
- What alternative, analogue, or edge case would change the recommendation?
- Is there a recency risk?
- Is this actually evidence, or interpretation stacked on top of evidence?

### 5C. Run Targeted Counter-Search

Search against the draft, not for it. Use targeted queries such as:
- "[claim keywords] limitations"
- "[tool/company/topic] failure cases"
- "[tool/company/topic] alternatives"
- "[benchmark/topic] dispute"
- "[feature/pricing/API] changelog release notes"
- "[tool/company/topic] security issue"
- "[tool/company/topic] customer complaints"
- "[claim keywords] site:official-domain"

For technical questions, re-check official docs, release notes, issue trackers, and benchmark repos. For market questions, check current official pages, filings, credible market reports, and operator/community signal separately.

### 5D. Record the Revision Log

Use this compact structure:

| Claim tested | Why it might be wrong | Counter-check | Result | Revision |
|---|---|---|---|---|
| [claim] | [risk] | [query/source] | [counterevidence or none] | kept / narrowed / downgraded / reversed |

If a claim survives, state what was checked. If it fails or weakens, update the main synthesis and confidence level.

### 5E. Stop Condition

Stop after one good loop when:
- the load-bearing claims have primary or high-quality support
- counter-search found no material refutation
- remaining uncertainty is named explicitly

Run another narrow loop only when the first loop reveals a new important contradiction or a materially better framing.

## Step 6 — Check Contradictions and Gaps

Actively look for:
- direct disagreement between sources
- missing evidence for key claims
- outdated information
- claims supported only by derivative summaries

If contradictions remain unresolved, report them explicitly.

## Step 6A — Audit Claim-Source Alignment

Audit every load-bearing claim before final synthesis:
- direct support versus inference
- claim strength versus evidence strength
- freshness
- applicability to the user's context
- primary, secondary, community, or inferred support
- contradictory evidence

Classify each claim:
- supported
- partially supported
- weakly supported
- unsupported

Keep, narrow, downgrade, replace the source, or remove the claim. An unsupported claim must not drive the recommendation.

## Step 6B — Check Context Preservation

Re-check:
- original question and decision
- fixed constraints
- flexible assumptions
- excluded scope
- region and budget
- time window and freshness needs
- risk level
- requested output
- assumptions changed during research

Correct any drift before synthesis.

## Step 7 — Synthesize

Separate output into:
- facts
- interpretation
- recommendation
- open questions

Do not let recommendation sections pretend certainty that the evidence does not support.

## Step 8 — Deliver

Return the final report with:
- executive summary
- findings
- recommendation
- contradiction / uncertainty section
- revision log
- evidence table
- sources
- next-step handoff note when useful
- explicit stop / continue decision
- micro-validation when the recommendation can be tested

Use one stop status:
- **Stop** — evidence is sufficient to act; more research is unlikely to change the decision.
- **Continue narrowly** — one or two concrete gaps could change the decision.
- **Continue broadly** — framing, alternatives, or source coverage remain materially weak.
- **Do not conclude yet** — evidence is too weak, stale, contradictory, or unsupported.

For micro-validation, state what to test, how to test it, success signal, failure signal, and the decision after the test.

## Step 9 — Follow-up Surface

If research quality is not strong enough, do not over-polish the answer.

Return one of:
- evidence gap report
- contradiction report
- follow-up research plan
- narrowed next-step recommendation

## Operating Rules

- Prefer official sources over commentary.
- Prefer recent sources when freshness matters.
- Prefer explicit assumptions over hidden assumptions.
- Prefer bounded iteration over open-ended wandering.
- Prefer falsification and counter-search over internal-only self-critique.
- Prefer adaptive tracks over a fixed agent waterfall.
- Prefer real parallel workers for independent tracks; do not treat simulated roles as independent validation.
- Prefer reusable artifacts over long verbal summaries.
- Prefer outputs that the next workflow step can consume directly.
