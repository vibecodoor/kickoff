# Adaptive Research Orchestration

## Goal

Use multiple research tracks only when they can improve the decision. The Lead Researcher controls scope, integrates evidence, and prevents duplicated or performative work.

## When to Orchestrate

Use adaptive multi-stage orchestration when one or more apply:
- the user requests deep or exhaustive research;
- the decision is high-stakes, expensive, irreversible, broad, or contested;
- several alternatives or evidence types must be compared;
- freshness, jurisdiction, methodology, or real-world reliability could change the answer;
- one pass is unlikely to establish a defensible recommendation.

For straightforward Standard research, use the bounded 3-stage map in `staged-mode.md` rather than full multi-track orchestration.

## Lead Researcher Responsibilities

The Lead Researcher:
- preserves the objective, constraints, exclusions, evaluation criteria, and stop condition;
- decomposes the question into decision-relevant tracks;
- assigns only tracks with a plausible information gain;
- runs independent tracks in parallel when real workers are available;
- merges evidence into one ledger and resolves duplicate or conflicting claims;
- chooses whether to continue narrowly, broaden, rerun a weak track, or synthesize;
- owns the final recommendation and confidence calibration.

## Track Selection

Choose from these capabilities; do not run them as a fixed waterfall:

- **Primary sources** — official facts, documentation, pricing, release notes, filings, standards, original studies.
- **Alternatives** — competing products, approaches, explanations, and comparison dimensions.
- **Reality signal** — repeated operator complaints, issue trackers, long-term reviews, and practical failure patterns.
- **Counter-evidence** — direct attacks on load-bearing claims and the current leading recommendation.
- **Freshness** — recent changes to prices, laws, APIs, availability, schedules, limits, or status.
- **Regional applicability** — jurisdiction, delivery, payments, support, language, and local availability.
- **Technical documentation** — official docs, repositories, changelogs, issues, compatibility, and architecture.
- **Legal/regulatory evidence** — current primary law and regulator guidance for the relevant jurisdiction.
- **Medical evidence** — guidelines, systematic reviews, contraindications, harms, and population applicability.
- **Benchmark methodology** — dataset, setup, metrics, reproducibility, recency, and disputes.

Spawn or run a track only when its result could change the recommendation, reduce a material uncertainty, resolve a contradiction, or verify a load-bearing claim.

Model tier per track (rule in SKILL.md "Agent model tier"):
- **`haiku`**: existence and number checks, quoting one primary source, KB lookups.
- **`sonnet`**: primary sources, alternatives, real-world signal, freshness, regional, technical documentation, benchmark methodology.
- **`opus`**: legal/regulatory, medical, and counter-evidence tracks attacking a load-bearing recommendation.

## Parallelism Rules

After framing, run independent tracks in parallel when possible. Typical parallel pairs:
- primary sources + alternatives;
- official product facts + real-world reliability;
- benchmark results + methodology audit;
- legal status + regional availability.

Keep dependent work sequential:
- claim-source audit follows evidence collection;
- targeted counter-search follows an initial hypothesis or recommendation;
- synthesis follows ledger merge and audit.

Do not use separate workers when the coordination cost exceeds the likely information gain.

## Worker Contract

Give each worker a bounded question, source priority, exclusions, freshness requirement, and output contract.

Each worker returns only:

```md
Track:
Question answered:
Sources checked:
Evidence ledger updates:
Contradictions:
Material gaps:
Confidence:
Recommended next action:
```

Use stable claim IDs (`C1`, `C2`) and source IDs (`S1`, `S2`) for large or multi-worker research. Workers should append ledger deltas rather than restating the complete research history.

## Lead Review

After merging a track, check:
- Did it answer its bounded question?
- Are the sources appropriate and current?
- What changed in the framing, ranking, confidence, or risk?
- Did it duplicate existing work?
- Which contradiction or gap remains decision-relevant?
- Would another track have enough information gain to justify its cost?

Then choose one:
- continue the planned work;
- continue narrowly on a specific gap;
- broaden because the framing or option set is weak;
- rerun a weak track with a tighter question;
- run a specialist track;
- proceed to synthesis;
- do not conclude yet.

## Anti-Failure Rules

The orchestration is failing when:
- workers repeat the same search or restart from zero;
- every possible track is run regardless of relevance;
- named roles create the appearance of depth without independent evidence;
- handoffs repeat prose instead of ledger changes and gaps;
- the Lead Researcher accepts outputs without checking source quality;
- counter-evidence or claim-source audit is skipped;
- coordination consumes more effort than the underlying research;
- work continues without a decision-relevant reason.

Stage boundaries map to the macro-stages in `staged-mode.md`: run the Stage Review checkpoint at macro-stage edges and proceed autonomously, not after every sub-step and without pausing for the user. When separate workers are unavailable, run the same decision logic directly; do not claim simulated roles provide independent validation.
