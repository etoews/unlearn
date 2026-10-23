# Unlearn with AI Evals

A conference presentation for [CloudNative.AI](https://www.cloudnative.ai/), Melbourne.

## Abstract

Models change under us constantly and every release quietly shifts the line between what still works and what needs to be unlearned. The prompt scaffolding and workarounds you perfected for the last model are still in your fingers, your memory files, and your agent's system prompt. When the model changes, some of those won't work as well anymore, but nothing tells you which ones. AI evaluations (evals) can help draw that line.

We start with what it means to unlearn in the context of the AI era. Then we increase our understanding with an introduction to evals (ground truth, metrics, LLM-as-judge, etc). Followed by a walk-through of a real setup that tests new models against the prompts that matter to you. You'll leave knowing how to measure what changed, unlearn what no longer holds, and pick up what's improved.

## Research

[docs/research.html](docs/research.html) collects the evidence behind the talk, with citations: what unlearning means, why old workarounds stick (from Kahneman's *Thinking, Fast and Slow*), vendor guidance on removing scaffolding written for older models, counter-evidence, an evals primer, and how the [ai-eval](https://github.com/etoews/skills/tree/main/skills/ai-eval) skill fits. Open it in a browser.
