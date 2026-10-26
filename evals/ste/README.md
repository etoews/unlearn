# Should STE stay?

The eval behind the talk's walk-through. It tests one line from my old CLAUDE.md:

> Always use ASD-STE100 Simplified Technical English (STE) for technical documentation.

I added the line because Opus 5 wrote long, elliptical docs. Opus 5.5 claims better writing. This eval checks if the line still does any work.

## What's here

- `cases/`: three docs tasks for Tui, a fictional internal Kubernetes platform. Each task gives messy source notes and asks for a page: a procedure, a concept page and a troubleshooting entry. The ground truth is the page I want.
- `prompts/base.md`: the system prompt for every arm.
- `prompts/ste.md`: the same prompt plus the STE line.
- `judges/writing-style.yaml`: the `writing_style` metric, a binary judge for a subset of the STE writing rules. It runs beside the three built-in metrics (correctness, relevance and faithfulness).

## Arms

| Arm | Model | System prompt |
|---|---|---|
| A: baseline | Opus 5 | `ste.md` |
| B: candidate | Opus 5.5 | `ste.md` |
| C: ablation | Opus 5.5 | `base.md` |

All arms use effort `xhigh` and 3 repetitions per case. The judge is pinned to Fable 5.1.

## Run it

You need the [ai-evals skill](https://github.com/etoews/skills/tree/main/skills/ai-evals), a running Phoenix and an `ANTHROPIC_API_KEY`. See the skill's `SKILL.md` for setup. From the skill directory, with `EVAL` set to this directory:

```sh
run() {
  uv run python scripts/run_eval.py --dataset "$EVAL/cases" --dataset-name unlearn-ste \
    --effort xhigh --judge-model anthropic/claude-fable-5-1 \
    --judge-file "$EVAL/judges/writing-style.yaml" --repetitions 3 "$@"
}
run --model anthropic/claude-opus-5   --system-prompt-file "$EVAL/prompts/ste.md"  --experiment-name "A: opus-5 + STE"
run --model anthropic/claude-opus-5-5 --system-prompt-file "$EVAL/prompts/ste.md"  --experiment-name "B: opus-5.5 + STE"
run --model anthropic/claude-opus-5-5 --system-prompt-file "$EVAL/prompts/base.md" --experiment-name "C: opus-5.5, no STE"
```

Then open the `unlearn-ste` dataset in Phoenix and compare the experiments.

Three cases are enough for a demo, not for a decision. Before you delete a real rule, use 20 or more cases taken from real failures.

## Results, 26 Oct 2026

Each score is passes out of runs. Every arm has 9 runs: 3 cases × 3 repetitions. Relevance was 9/9 in every arm.

| Arm | Correctness | Faithfulness | Writing style (STE) | Task cost | Average words |
|---|---|---|---|---|---|
| A: Opus 5 + STE | 9/9 | 5/9 | 8/9 | $0.58 | 492 |
| B: Opus 5.5 + STE | 9/9 | 9/9 | 6/9 | $1.13 | 478 |
| C: Opus 5.5, no STE | 9/9 | 9/9 | 2/9 | $0.47 | 477 |

On Opus 5.5 the STE line still changes the style, but it doesn't change the facts, and it costs 2.4 times as much in extra thinking. No arm came near the ground truth's length of about 140 words, which was the original reason for the line.
