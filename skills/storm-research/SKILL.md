---
name: storm-research
description: Multi-perspective, cited research on a topic using Stanford's STORM method (discover perspectives, ground each in real web search with follow-ups, synthesize with citations and disagreements left in). Use when asked to research a topic thoroughly, write a brief/report on something, or compare/evaluate options where a single-pass answer would just average everything into mush.
---

# STORM research

Adapted from the method in Stanford OVAL's STORM paper (NAACL 2024, arXiv:2402.14207); this is a prompt-level adaptation, not the knowledge-storm code, and it adds a human edit of the perspective list and keeps disagreements visible. The idea: the trick isn't researching harder, it's researching like a panel. A one-shot answer collapses every angle into an averaged paste. This runs the topic through several grounded, adversarial perspectives and keeps the disagreements between them instead of smoothing them out — the disagreement is where the real insight lives.

## Step 1 — Discover perspectives, then let the human edit them

Propose 4-6 distinct expert perspectives relevant to the topic (not a generic "pros and cons" split — pick roles that would actually ask different questions: practitioner, skeptic, economist/cost angle, historian ("we've been sold this before"), end user, regulator/compliance, whichever fit the topic). For each, write the ONE question that perspective cares about most.

**Stop here and show the list before searching anything.** The user's edit (cut a perspective, add the one you missed) is where most of the value enters — don't skip this by proceeding straight to research.

## Step 2 — Interview each perspective, grounded

For each surviving perspective: ask its 2-3 sharpest questions, answer each with real web search (not from training knowledge), ask one follow-up per answer to resolve anything thin, and cite every claim. Explicitly flag where sources disagree with each other — don't resolve the disagreement here, just surface it.

## Step 3 — Synthesize without flattening

Build a non-redundant outline from all the interviews, for a smart reader who knows nothing about the topic yet. Write it up with citations. Mark any claim that rests on a single source. Keep genuine disagreements between perspectives visible in the final writeup rather than averaging them into a mushy consensus sentence.

## What this does not do

It won't tell you which question was worth asking, or which finding matters for the decision in front of you — that's the user's judgment, not automatable. It also doesn't critique its own perspective list; if the topic itself was the wrong one, this will produce a well-cited answer to the wrong question. Flag that risk rather than hiding it if the topic seems mis-scoped.
