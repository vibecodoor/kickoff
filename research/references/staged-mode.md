# Staged Execution

## Goal

Run a **full, autonomous research process** as a sequence of **macro-stages**. The Lead Researcher progresses through the stages itself, dispatching specialist agents/tracks per stage, and runs an internal Stage Review between stages to decide what to do next. It produces a finished report without pausing for the user.

This file defines *how* to pace the work. It does not replace the rigor in `workflow.md`, `source-policy.md`, and `output-contract.md` — every stage still obeys those rules. Staging only sets the order of passes, where specialist agents are launched, and what each internal checkpoint records.

## Core principle: macro-stage, not micro-step

- **One stage = one large semantic pass**, not one bullet point.
- A stage may contain several related sub-steps. Do them together.
- The **Stage Review is an internal checkpoint**, run after a full macro-stage — not a hand-off to the user and not a hard stop.
- Move straight into the next stage based on the review's decision (continue / narrow / broaden / synthesize).

Reviewing after every small item makes the model administer the process instead of researching. Macro-stages keep the checkpoints meaningful.

## Autonomy

- The skill runs all stages to completion on its own. It does **not** wait for a "continue" between stages.
- It launches specialist agents/tracks within a stage when they add information gain (see `orchestration.md`), runs independent tracks in parallel when real workers are available, and merges their ledger deltas before that stage's review.
- Run stages as separate user-facing turns **only** if the user explicitly asks for an interactive stage-by-stage process. That is the exception, not the default.

## Mode → stage count

| Mode | Stages | Use |
|---|---|---|
| **Standard staged** | 3 | Ordinary topics. Compress the passes. |
| **Deep staged** | 5 | High-stakes, broad, contested, or recommendation-heavy. |
| **Exhaustive** | 5 + specialist agents | As Deep, plus dispatch specialist tracks/agents where they add information gain (see `orchestration.md`). |

The stages below are the **5-stage map**. The 3-stage map at the end is a compression of the same passes — not a different method.

---

## 5-stage map (Deep / Exhaustive)

Each stage lists the sub-steps it covers and the `workflow.md` steps it maps to. End every stage with a Stage Review (template below), then proceed to the next stage per the review's decision.

### Stage 0 — Frame + Research Plan
Maps to workflow Steps 1–2.

Produce:
- main research question;
- research type;
- fixed constraints / flexible assumptions / excluded scope (kept separate);
- evaluation criteria;
- risk level;
- depth: Quick / Standard / Deep / Exhaustive;
- which source buckets are needed;
- the stop condition (when "good enough");
- expected deliverable + downstream consumer if obvious.

**Stage Review:** what is fixed; assumptions taken; source buckets needed; what the next stage will verify. Then continue to the next stage.

### Stage 1 — Ground + Source Quality + Initial Evidence Ledger
Maps to workflow Steps 3–4 + `source-policy.md`.

Collect the primary base in preference order (primary/official → primary-adjacent → secondary → community): official sites, docs, pricing, release notes, help centers, repositories, studies, guidelines, regulatory docs where applicable. For library/framework/API topics, start with official docs (Context7 MCP when available), not broad search.

Rate each source immediately: primary/official · secondary · community · freshness · relevance · likely bias.

Start the evidence ledger:

| Claim | Evidence | Source type | Confidence | Caveat |
|---|---|---|---|---|

**Stage Review:** what primary sources confirmed; which claims are weak; what is missing; what to expand next. Then continue to the next stage.

### Stage 2 — Expand + Alternatives + Snowball
Maps to workflow Steps 4–4A.

Widen the map: alternatives, competitors, analogues, other solution classes, "X vs Y" comparisons, expert reviews, and links/mentions snowballed from strong sources. Check whether the task is framed too narrowly — the best option may sit in a different class than the original choice. Update the ledger with any new load-bearing claims.

**Stage Review:** which alternatives appeared; did the frame change; which options got stronger/weaker; what criteria to add; what to reality-check next. Then continue to the next stage.

### Stage 3 — Reality-check + Negative Signals
Maps to workflow Step 6 (community-signal portion) + `source-policy.md` community rules.

If the topic is practical, check real-world experience: Reddit, GitHub issues, Hacker News, forums, X, YouTube comments, reviews, long-term reviews, complaints, user cases. Separate: repeated complaints · one-off stories · stale complaints · regional issues · serious edge cases · repeated positive signals.

Reality signal shows practical pain but does not prove official facts — keep it labeled as community signal.

**Stage Review:** repeated problems found; what looks like noise; what contradicts official sources; which risks rose; which claims to attack next. Then continue to the next stage.

### Stage 4 — Attack + Claim-Source Audit + Context Check
Maps to workflow Steps 5, 6A, 6B.

Deliberately try to break the preliminary conclusion. Search: limitations, complaints, bad reviews, failure cases, alternatives, "vs", "not working", deprecated, pricing change, security issue, lawsuit, regulation, adverse effects, benchmark dispute, methodology criticism.

Audit load-bearing claims: does the source actually support the claim (not just same topic)? Is the claim stronger than the evidence? Is the source fresh? Are there contradicting sources? Should confidence drop?

Revision log:

| Claim tested | Why it might be wrong | Counter-check | Result | Revision |
|---|---|---|---|---|

Revision ∈ {kept, narrowed, downgraded, reversed}.

Then run the context-loss check: are the user's constraints, region, budget, excluded scope, and original question still intact?

**Stage Review:** which claims survived; which were weakened; what changed after counter-search; ready for synthesis or need one more narrow stage. Then continue to the next stage.

### Stage 5 — Synthesis + Stop/Continue + Micro-validation
Maps to workflow Steps 7–8 + `output-contract.md`.

Deliver the final result: executive summary; key findings; comparison/ranking if applicable; recommendation; confidence; biggest tradeoff; risks; contradictions; unresolved gaps; what changed after counter-research.

Choose a status:
- **Stop** — enough to act.
- **Continue narrowly** — one specific gap to close.
- **Continue broadly** — research needs widening.
- **Do not conclude yet** — evidence insufficient.

Propose micro-validation: what to test, how, what result confirms the recommendation, what result kills it, what to do after the test.

Do not add sources for volume. Continue only if new data could change the decision, reduce a material uncertainty, or resolve a contradiction.

---

## 3-stage map (Standard staged)

Same passes, compressed into three macro-stages:

| Stage | Covers | Maps to |
|---|---|---|
| **Stage 0 — Frame + Plan** | Same as 5-stage Stage 0 | Steps 1–2 |
| **Stage 1 — Research Pass** | Ground + Source Quality + Expand + Alternatives + Reality-check | Steps 3–4, 4A, 6 (community) |
| **Stage 2 — Attack + Verify + Synthesize** | Attack + Claim-Source Audit + Context Check + Synthesis + Stop/Continue + Micro-validation | Steps 5, 6A, 6B, 7–8 |

Keep the evidence ledger from Stage 1 and the revision log from Stage 2 even in the compressed mode. End each stage with a Stage Review, then continue.

---

## Stage Review template

Each stage closes with the same compact internal checkpoint, then the Lead Researcher acts on the decision and moves on:

```md
### Stage Review — Stage N: <name>
- Locked in: <what is now established>
- Weak / unverified: <claims still soft>
- Missing: <gaps>
- Uncovered by ALL passes/tracks so far: <angle no pass has touched, or "none identified">
- Decision: continue / narrow / broaden / synthesize
- Next stage will: <what the next pass does>
```

This is a working checkpoint, not a stopping point. Carry the ledger, revision log, and preserved constraints forward into the next stage. Surface the review to the user mid-run only if running an explicitly interactive stage-by-stage session.

## Exhaustive add-on

In Exhaustive mode, run the 5-stage map and, where a specialist track has real information gain, dispatch it per `orchestration.md` (primary sources, alternatives, reality signal, counter-evidence, freshness, regional, technical docs, legal/regulatory, medical, benchmark methodology). Merge each track's ledger deltas before the relevant Stage Review; when multiple tracks ran in parallel, run the anonymized cross-review from `adversarial-review.md` before merging. Do not spawn a track that cannot change the recommendation. When real parallel workers are unavailable, run the same tracks directly and do not present simulated roles as independent validation.
