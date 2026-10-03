---
name: kickoff
description: "Full new-project pipeline: clarify the idea → deep research → generate the Dev Memory Kit. Orchestrates the grill-me, creator, and research skills in sequence. Use when the user wants the complete kickoff flow for a new project idea: 'kickoff X', 'full pipeline for X', 'research + create project', 'run the whole pipeline on this idea', or when they describe a product idea and explicitly want it researched before files are generated. For plain project init without the separate research pass, use the creator skill directly."
---

# Kickoff — new-project pipeline

Thin orchestrator. It owns **sequencing and handoffs only** — all stage content lives in the underlying skills. Never duplicate their instructions; invoke them and apply the overrides below.

```text
Stage 1  Clarify   → project brief                     (grill-me, creator §1 checklist)
Stage 2  Research  → deep-research report              (research skill, Deep mode)
Stage 3  Generate  → devkit/ files                     (creator §4, research steps skipped)
```

Run the pipeline in one pass, pausing for the user only at Stage 1 questions.

## Global rules

- **No double research.** Creator's internal research fan-out (its steps 2–3) is replaced by Stage 2. Creator only synthesizes.
- **Persist artifacts between stages** so the pipeline survives `/compact`: each stage writes its output to `devkit/RESEARCH.md` (created at Stage 1, grown by later stages). Create `devkit/` at the project root if absent.
- **Announce the stage** in one line when entering it (e.g. "Stage 2/3 — Deep research: 3 web tracks").

## Stage 1 — Clarify

Take the coverage checklist from the **creator** skill's step-1 "Clarify the Idea" section:

- What the product does and who it's for
- What problem it solves
- MVP scope
- Constraints (timeline, budget, solo dev, tech preferences, platforms)

Run the questioning with the **grill-me** skill instead of a flat pass: one question at a time, each with your recommended answer, resolving dependent decisions in order. Two overrides on grill-me:

- **Scope:** stay on the four checklist axes above. Implementation-level design questions belong to Stage 2, not here — research hasn't run yet, so grilling on stack details is guessing.
- **Stop condition:** stop when all four axes are answered and no open question would change the research tracks. Hard ceiling ~8 questions. If the idea is already specific, confirm the gaps and move on.

grill-me's "explore the codebase instead of asking" rule still applies for existing repos. If the approach looks suboptimal or risky, say so before spending research budget.

**Output:** write the brief as the opening `## Brief` section of `devkit/RESEARCH.md` (project name, one-paragraph idea, user/problem, MVP scope, constraints).

## Stage 2 — Research

Invoke the **research** skill in **Deep mode** (5 macro-stages) with the brief as the objective. Map creator's research spec onto research tracks:

- **3 baseline web tracks** (creator's facets): competitors + market · stack + architecture + references (verify against current docs via Context7) · pitfalls + don't-hand-roll.
- **Extra tracks** only for genuinely separable concerns, per creator §2's non-overlap rule (ceiling: 7 web tracks).

The research skill's own rules govern everything else: source policy, confidence tags, evidence table, self-critique loop, output contract. If the report's go/no-go signals say don't build, stop and ask the user (askuserquestion) whether to proceed, reframe, or abort before Stage 3.

**Output:** append the full research report (research skill's output contract sections) to `devkit/RESEARCH.md`. The executive summary must state the recommended stack, MVP scope, and go/no-go signals — Stage 3 consumes it.

## Stage 3 — Generate

Invoke the **creator** skill, entering at its step 4 ("Generate the Dev Memory Kit files"). Explicit overrides:

- **Skip creator steps 2–3 entirely** — synthesis input is `devkit/RESEARCH.md` (already written).
- `devkit/RESEARCH.md` **already exists** — do not regenerate it from creator's schema; keep the pipeline's structure (Brief → research report). Reconcile only if a section required by downstream links is missing.
- Seed the inline **Decisions** digest with the 1–3 load-bearing research choices.

Everything else follows creator §4 verbatim: emit only `devkit/PROJECT.md` + `devkit/STATE.md` (RESEARCH.md exists already), never pre-create empty stubs, wire up the Dev Memory pointer block in root `CLAUDE.md` and `AGENTS.md`.

**Close-out:** summarize what was laid down, note that DECISIONS/JOURNAL/specs are deferred to their triggers, and point at `STATE.md`'s `## Now` as the first build step.
