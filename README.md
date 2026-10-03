---
name: storm-research
type: tool
status: experimental
license: MIT
version: 0.1.0
summary: A Claude skill that researches a topic as a panel of perspectives you approve first, grounds each in web search with citations, and keeps the disagreements in the write-up.
updated: 2026-10-03
verified: 2026-10-03
---

# storm-research

A one-shot answer collapses every angle into an averaged paste. The trick is not to research harder. It is to research like a panel.

`storm-research` runs a topic through several grounded, adversarial perspectives and keeps the disagreements between them instead of smoothing them out. The disagreement is usually where the insight is.

Adapted from the method in the STORM paper from Stanford OVAL (NAACL 2024, [arXiv:2402.14207](https://arxiv.org/abs/2402.14207)): discover perspectives, interview each one with grounded questions, then synthesize. This is a short prompt-level adaptation for Claude. It is not their code (knowledge-storm) and does not use their system. It differs in two ways: you edit the list of perspectives before any searching, and it keeps disagreements visible in the final write-up.

## How it runs

1. **Perspectives, then you edit them.** Claude proposes 4 to 6 distinct expert perspectives for the topic, picked because they would ask different questions (a practitioner, a skeptic, someone watching cost, a historian who says "we have been sold this before", an end user, a regulator), not a generic pros-and-cons split. Each gets the one question it cares about most. **It stops and shows you the list before searching anything.** Cutting one or adding the one it missed is where most of the value enters.
2. **Interview each perspective, grounded.** For each one that survives: its 2 to 3 sharpest questions, each answered with real web search rather than from memory, one follow-up per answer to settle anything thin, and a citation for every claim. Where sources disagree with each other it flags that and does not resolve it yet.
3. **Synthesize without flattening.** A non-redundant outline from all the interviews, written for a smart reader who knows nothing about the topic. Citations throughout. Any claim that rests on a single source is marked. Real disagreements stay visible in the final write-up.

## Illustrative panel

The shape of step 1 for the topic "should a small team self-host its source control?" (invented, for illustration):

| Perspective | The one question it cares about |
|---|---|
| Operator | What does the third restore at 3 a.m. actually cost? |
| Skeptic | What does the hosted service already do that we would have to rebuild? |
| Finance | What is the total cost at 5, 20 and 100 people? |
| Historian | Which teams moved in and out of self-hosting, and why? |
| Security | What is the real exposure of each option, not the marketing one? |

## What it does not do

- It will not tell you which question was worth asking, or which finding matters for your decision. That is your judgment.
- It does not critique its own perspective list. If the topic itself was scoped wrong, you get a well-cited answer to the wrong question. It is told to flag that risk when the topic looks mis-scoped.
- It needs a web search tool in the session. Without one the grounding step has nothing to ground on.

## Install

Copy `skills/storm-research` into `~/.claude/skills/` (or a project's `.claude/skills/`). A plugin manifest is included in `.claude-plugin/plugin.json`.

Installed as a plugin the skill is namespaced, for example `/storm-research:storm-research`; copied into `skills/` it is `/storm-research`. Claude also picks it up from the description, so you do not need to type the command. Ask Claude to "research this thoroughly", "write a brief on X", or "compare these options".

## Status

Experimental. It is a procedure for Claude to follow, not a program.

## License

MIT. See [LICENSE](LICENSE).

Made at [MEDiAGATO](https://github.com/mediagato).
