# Kickoff

A pipeline for starting a new project. Four stages run in order: an interview to pin down the idea, deep research, a council of advisors arguing about the result, then file generation.

```text
Stage 1  Clarify   interview until the brief is solid
Stage 2  Research  parallel web tracks, sources tagged by confidence
Stage 3  Council   5 advisors, peer review, a verdict, and a gate
Stage 4  Generate  devkit/ files you can build from
```

You get asked two things. The Stage 1 questions, and the Stage 3 gate if the council disagrees with the research. The rest runs unattended.

Each stage writes to disk before the next one starts, so a `/compact` in the middle doesn't lose the work.

## Why the extra stages

Research alone tells you what exists. It doesn't tell you whether your read of it is any good.

That's Stage 3. Five advisors take the researched plan, argue from different angles, review each other anonymously, and a chairman rules on whether this is the right thing to build, at the right scope, on the right stack.

If the verdict is "don't build this" or "reframe it entirely", the pipeline stops and asks you. Smaller adjustments get applied and the run continues.

## What lands in your project

A `devkit/` folder:

- `devkit/RESEARCH.md` holds the brief, the research report (competitors, stack with confidence tags, architecture patterns, things not to hand-roll, risks), and the council verdict. It grows stage by stage.
- `devkit/PROJECT.md` is the control plane. Vision, scope, architecture, invariants, build plan, plus a protocol telling any agent how to keep the kit current.
- `devkit/STATE.md` is the cursor. Current task, next steps, blockers.

Templates for `DECISIONS.md`, `JOURNAL.md` and per-feature specs come with `creator`. They get created when something triggers them, not upfront as empty files.

## What's in this repo

Two skills, both original work here:

| Folder | Job |
|---|---|
| `kickoff/` | The orchestrator. Sequencing, handoffs, the Stage 3 gate. Thin by design. |
| `research/` | Stage 2. Parallel tracks, source policy, confidence tags, a self-critique loop. |

Three more skills do the actual work at Stages 1, 3 and 4. They live in their own repos and this one doesn't copy them:

| Skill | Used at | Source |
|---|---|---|
| `grill-me` | Stage 1 interview | [mattpocock/skills](https://github.com/mattpocock/skills) by Matt Pocock |
| `llm-council` | Stage 3 council | [aiwithremy/claude-skills-llm-council](https://github.com/aiwithremy/claude-skills-llm-council) by Ole Lehmann, adapting [Andrej Karpathy's LLM Council](https://github.com/karpathy/llm-council) |
| `creator` | Stage 1 checklist, Stage 4 generation | [vibecodoor/creator](https://github.com/vibecodoor/creator) |

Installing from source means you get their updates and their authors keep their credit.

## Install

Paste this into Claude Code, or whatever agent you use:

```
Install the kickoff pipeline for me. It's five skills that go in my skills
directory (~/.claude/skills/ for Claude Code, one folder each).

Two come from https://github.com/vibecodoor/kickoff. Copy its `kickoff/` and
`research/` folders.

Three come from their own repos:
  grill-me    https://github.com/mattpocock/skills (skills/productivity/grill-me)
  llm-council https://github.com/aiwithremy/claude-skills-llm-council
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
npx degit aiwithremy/claude-skills-llm-council ~/.claude/skills/llm-council
```

Then open a project and say `kickoff: <your idea>`.

## How each stage behaves

Stage 1 asks one question at a time, each with a recommended answer, working down the dependency order of the decisions. It stops once the four things are settled: what and for whom, what problem, MVP scope, constraints. There's a question ceiling so it can't stall the pipeline. In an existing repo it reads the code instead of asking about it.

Stage 2 runs at least 3 web tracks in parallel: competitors and market, stack and architecture, pitfalls and what not to hand-roll. Genuinely separate concerns get their own track, up to 7. Stack claims get checked against current docs. Every claim carries a HIGH, MEDIUM or LOW tag.

Stage 3 is the council, described above.

Stage 4 hands everything to `creator`, which synthesizes it into `devkit/` and points at the first concrete build step. Council rulings override research on scope. `creator` skips its own research fan-out, since Stage 2 already covered it.

## Using less of it

For research without the council, run `creator` on its own. It has a research step built in.

`llm-council` works standalone too, on any decision, not just a new project.

The knobs live in the skill files. Stage 1's question ceiling is one line in `kickoff/SKILL.md`. The 3-track floor and 7-track ceiling are in `research/SKILL.md`. Advisor count and the chairman prompt are in `llm-council/SKILL.md`.

## Credits

Stage 3 exists because of [Andrej Karpathy's LLM Council](https://github.com/karpathy/llm-council) and [Ole Lehmann's](https://x.com/itsolelehmann) skill adaptation of it. Stage 1's interview method is [Matt Pocock's](https://github.com/mattpocock/skills) `grill-me`. File issues about those skills on their repos, not here.
