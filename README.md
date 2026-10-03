# Kickoff

A pipeline for starting a new project. Three stages run in order: an interview to pin down the idea, deep research, then file generation.

```text
Stage 1  Clarify   interview until the brief is solid
Stage 2  Research  parallel web tracks, sources tagged by confidence
Stage 3  Generate  devkit/ files you can build from
```

You get asked the Stage 1 questions, and one more if research concludes the project shouldn't be built. The rest runs unattended.

Each stage writes to disk before the next one starts, so a `/compact` in the middle doesn't lose the work.

## What lands in your project

A `devkit/` folder:

- `devkit/RESEARCH.md` holds the brief, the research report (competitors, stack with confidence tags, architecture patterns, things not to hand-roll, risks). It grows stage by stage.
- `devkit/PROJECT.md` is the control plane. Vision, scope, architecture, invariants, build plan, plus a protocol telling any agent how to keep the kit current.
- `devkit/STATE.md` is the cursor. Current task, next steps, blockers.

Templates for `DECISIONS.md`, `JOURNAL.md` and per-feature specs come with `creator`. They get created when something triggers them, not upfront as empty files.

## What's in this repo

Two skills, both original work here:

| Folder | Job |
|---|---|
| `kickoff/` | The orchestrator. Sequencing, handoffs, the no-go check. Thin by design. |
| `research/` | Stage 2. Parallel tracks, source policy, confidence tags, a self-critique loop. |

Two more skills do the actual work at Stages 1 and 3. They live in their own repos and this one doesn't copy them:

| Skill | Used at | Source |
|---|---|---|
| `grill-me` | Stage 1 interview | [mattpocock/skills](https://github.com/mattpocock/skills) by Matt Pocock |
| `creator` | Stage 1 checklist, Stage 3 generation | [vibecodoor/creator](https://github.com/vibecodoor/creator) |

Installing from source means you get their updates and their authors keep their credit.

## Install

Paste this into Claude Code, or whatever agent you use:

```
Install the kickoff pipeline for me. It's four skills that go in my skills
directory (~/.claude/skills/ for Claude Code, one folder each).

Two come from https://github.com/vibecodoor/kickoff. Copy its `kickoff/` and
`research/` folders.

Two come from their own repos:
  grill-me    https://github.com/mattpocock/skills (skills/productivity/grill-me)
  creator     https://github.com/vibecodoor/creator

Skip anything I already have and tell me which ones you skipped. Then confirm
the `kickoff` skill is available.
```

If you'd rather run the commands yourself:

```bash
npx degit vibecodoor/kickoff/kickoff ~/.claude/skills/kickoff
npx degit vibecodoor/kickoff/research ~/.claude/skills/research
npx degit vibecodoor/creator ~/.claude/skills/creator
npx degit mattpocock/skills/skills/productivity/grill-me ~/.claude/skills/grill-me
```

Then open a project and say `kickoff: <your idea>`.

## How each stage behaves

Stage 1 asks one question at a time, each with a recommended answer, working down the dependency order of the decisions. It stops once the four things are settled: what and for whom, what problem, MVP scope, constraints. There's a question ceiling so it can't stall the pipeline. In an existing repo it reads the code instead of asking about it.

Stage 2 runs at least 3 web tracks in parallel: competitors and market, stack and architecture, pitfalls and what not to hand-roll. Genuinely separate concerns get their own track, up to 7. Stack claims get checked against current docs. Every claim carries a HIGH, MEDIUM or LOW tag.

Stage 3 hands everything to `creator`, which synthesizes it into `devkit/` and points at the first concrete build step. `creator` skips its own research fan-out, since Stage 2 already covered it.

## Using less of it

For a lighter run, use `creator` on its own. It has a research step built in.

The knobs live in the skill files. Stage 1's question ceiling is one line in `kickoff/SKILL.md`. The 3-track floor and 7-track ceiling are in `research/SKILL.md`.

## Credits

Stage 1's interview method is [Matt Pocock's](https://github.com/mattpocock/skills) `grill-me`. File issues about those skills on their repos, not here.
