# Adversarial review (council-style)

Independent critique of the draft conclusion by sub-agents who did not build it. Adapted from Karpathy's LLM Council: independent stances + anonymized review + a chairman who can side with the dissenter. This replaces same-agent reflection as the critique mechanism — the agent that formed a conclusion is structurally bad at falsifying it.

## When to run

- **Deep research** — run the review board before final synthesis when the report makes a strong or contested recommendation.
- **Exhaustive research** — review board, plus anonymized cross-review of specialist tracks before merging.
- **Standard research / verification pass** — skip; the regular self-critique loop applies.
- **No real sub-agent workers available** — do not simulate the board. Fall back to the standard self-critique loop and label it as same-agent critique in the revision log.

Cost gate: the board is +3 sub-agents, cross-review is +N. Run it when the recommendation is contested, high-stakes, or hangs on one or two sources. Skip it when the answer is factual verification with converging primary evidence.

## The review board

After the draft report exists, spawn three stance-based reviewers **in parallel**. Each gets a different input slice — that asymmetry is deliberate.

1. **Contrarian** — input: the draft recommendation + the evidence ledger only (not the prose). Task: does the evidence actually force this conclusion? Name the weakest load-bearing claim, the strongest alternative reading of the same evidence, and what single finding would reverse the recommendation.
2. **Outsider** — input: the final report only, zero research context. Task: does the report stand alone? Flag claims that require prior knowledge, undefined terms, and any jump from findings to recommendation that a cold reader cannot follow.
3. **Executor** — input: the report + handoff note. Task: can the next agent or operator act on this without re-deriving the work? Flag missing next steps, untestable recommendations, and vague success/failure criteria in the micro-validation.

Each reviewer: under 200 words, direct, no hedging, no balance-seeking. Their job is to attack from their angle; synthesis happens later.

## Cross-review of specialist tracks (Exhaustive only)

Before merging specialist track outputs:

1. Anonymize track outputs as Response A..N, randomized order (prevents deference to a "senior" track).
2. Spawn one reviewer per track. Each sees all anonymized outputs and answers:
   - Which output has the strongest evidence, and why?
   - Which output has the biggest blind spot or weakest sourcing?
   - What did **all** outputs miss that the research should cover?
3. Feed the answers into the Stage Review. The "what did all outputs miss" answers are the highest-value signal — they surface structural blind spots no single track could see.

## Chairman merge rules

The Lead Researcher acts as chairman:

- Integrate review findings into the main answer — never as appended caveats that contradict the recommendation.
- **The dissenter can win.** If a minority reviewer, track, or source has the strongest reasoning, side with it explicitly and say why the majority reading loses.
- Record each board finding in the revision log: reviewer stance, finding, conclusion change (kept / narrowed / downgraded / reversed), final confidence.
- If the board changes nothing, state what was attacked and why the conclusion survived — silence is not evidence of robustness.
