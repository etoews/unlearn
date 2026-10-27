# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

A reveal.js deck for a 25-minute talk. README.md covers presenting, publishing and upgrading reveal.js.

## Constraints

- The deck runs offline from `file://` with no build step, because it is presented from a laptop without internet. Load everything by relative path from `presentation/`. That rules out CDN links, web fonts, and plugins that fetch: Markdown with external files, and Math.
- The repo is public and GitHub Pages serves `main`. Speaker notes are readable in the page source, so they never name private repos, session IDs or local paths. The research notes were removed from git history on purpose, so research material stays out of the repo.

## Slides

- Bullets are cues the speaker talks to, not text to read. Use at most six words per bullet and four bullets per slide.
- Speaker notes are memory aids, not a script. Write one full, succinct sentence for each bullet, concept or element on the slide, then `Citations:`. Every slide gets notes, including diagrams and backup screenshots. Each citation starts with the on-screen text it supports. Sources are in the research artifact: https://claude.ai/artifact/BcfgdHtDnkoWv8muvxWgEd
- Citations quote sources verbatim. Every quoted phrase must appear word for word on the cited page, because the speaker checks citations by searching the source for the exact text. Fetch the page and copy the sentence out of it; never paraphrase, elide with an ellipsis, or join two sentences into one quote. If no sentence on the page supports the claim, say so instead of inventing one.
- Diagrams are separate SVG files in `presentation/diagrams/`, loaded with `<img>`. Each file carries its own `<style>`, because page CSS and web fonts don't reach into an `<img>` SVG.

## Checking a change

Render a slide offline. The bogus proxy blocks the network, and the slide index after `#/` is zero-based:

```sh
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless=new \
  --user-data-dir=<scratch>/chrome --proxy-server=127.0.0.1:9 \
  --window-size=1280,800 --virtual-time-budget=3000 \
  --screenshot=<scratch>/slide.png "file://$PWD/presentation/index.html#/2"
```
