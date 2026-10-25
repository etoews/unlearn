# Unlearn with AI Evals

A conference presentation for [CloudNative.AI](https://www.cloudnative.ai/), Melbourne.

## Abstract

Models change under us constantly and every release quietly shifts the line between what still works and what needs to be unlearned. The prompt scaffolding and workarounds you perfected for the last model are still in your fingers, your memory files, and your agent's system prompt. When the model changes, some of those won't work as well anymore, but nothing tells you which ones. AI evaluations (evals) can help draw that line.

We start with what it means to unlearn in the context of the AI era. Then we increase our understanding with an introduction to evals (ground truth, metrics, LLM-as-judge, etc). Followed by a walk-through of a real setup that tests new models against the prompts that matter to you. You'll leave knowing how to measure what changed, unlearn what no longer holds, and pick up what's improved.

## Presentation

The slides are a [reveal.js](https://revealjs.com/) deck in [presentation/](presentation/). There is nothing to install or build.

- **Present locally, offline:** open `presentation/index.html` in a browser. reveal.js 6.0.2 is vendored in `presentation/vendor/reveal.js/`, so the deck needs no network connection.
- **Online:** GitHub Pages publishes the `main` branch at <https://etoews.github.io/unlearn/presentation/>.

Keys: arrows to move, `S` for the speaker view (notes go in `<aside class="notes">`), `F` for full screen, `Esc` for the overview, `Ctrl+Shift+F` to search.

To upgrade reveal.js, replace the files in `presentation/vendor/reveal.js/` with the same files from the new release's `dist/` and update `VERSION`.
