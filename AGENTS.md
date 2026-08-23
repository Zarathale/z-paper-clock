# AGENTS.md — z-paper-clock

**Start here if you are an AI agent working on this repository.**

This file exists because the project's operating documentation was written for Claude, and `CLAUDE.md` is not a filename every agent looks for. The substance below is vendor-neutral.

---

## What this project is

A hand-built digital reconstruction of the working paper clock from James Smith Rudolph's *Make Your Own Working Paper Clock* (1983). Alan built one out of paper in the mid-1990s and it kept time. All 123 printed pieces have been scanned at roughly 613 DPI; 32 are hand-traced into layered SVG in Affinity Designer; a single-file three.js tool (`preview.html`) folds them, co-locates subassemblies and captures assembled poses; a Python script builds a graph of how pieces attach to each other. The goal is an interactive 3D model of the assembled, working clock on the public web.

**The bottleneck is human authoring time, not code.** Every capability in the preview tool exists to make bench work faster or more verifiable. An agent that forgets this will build tooling nobody is waiting for.

The repository was frozen on 2026-08-22 at commit `5a6b49b` and forked into two independent lines, `main-claude` and `main-gpt`. `main` is retired as a trunk.

---

## Read first, in this order

1. **`HANDOFF/README.md`** — what happened and where things stand.
2. **`HANDOFF/PICKUP-GUIDE.md`** — three entry ramps, a recommended first hour, and ways to waste your time.
3. **`PROJECT-STATE.md`** — what exists and, more usefully, what does not.
4. **`LAYER-CONVENTIONS.md`** — how a paper piece is described as layered SVG. **This is the project's core technical invention** and the thing you most need to understand.
5. **`claude-work/DECISIONS.md`** — fourteen numbered decisions, each with rationale and an explicit reopen trigger.
6. **`CLAUDE.md`** — 87 KB of accumulated conventions. Written for Claude; substantively useful to anyone. The sections that matter regardless of vendor: *File Naming Conventions*, *Architectural Decisions (Closed)*, *Git Workflow*, *Orchestration Prompt Format*, *Sessions Convention*.

Documents in this repository were reconciled against the git log at the freeze and corrected where they had drifted. Where a correction was applied it is marked inline with a date. Historical documents carry a freeze header naming what in them is no longer true. **You can trust what you read**, which was not the case a day before the freeze — `HANDOFF/RECONCILIATION.md` explains why.

---

## Standing rules

Not stylistic preferences. Violating these causes real damage.

**Never republish the book.** `source/` holds scans and transcriptions for personal study. Everything published must be original derivative work. The book is in print; the correct answer to "can I see the source" is "buy a copy."

**Never invent piece numbers, plate letters, or label notation.** They come from `source/transcriptions/embedded-labels.md`.

**Never start an HTTP server to test `preview.html`.** It is a single file that runs from `file://`. Terminal agents typically work inside a git worktree, so a server started there serves the *main* repo's copy rather than your edited one — you will verify the wrong file. Static checks gate the commit; browser checks gate the merge and belong to a human.

**The SVG is artifact-truth; the sidecar is overlay.** Authored SVG carries what is printed on the piece. Everything learned elsewhere — assembled poses, mechanism geometry, connections inferred from the instruction text — goes in the per-piece JSON sidecar with an explicit provenance field. Never write learned data back into the SVG.

**Always write a session note.** `sessions/YYYY-MM-DD-HHMM_mode_short-topic.md`, local Pacific time. Even for small sessions. These turned out to be the most reliable documents in the repository, precisely because they were written in the moment and never retro-edited.

**Don't reopen settled decisions casually.** Reopening is allowed; doing it by accident is not.

**Propose, don't poll.** The charter puts the agent in the lead on direction. Read the state, form a view, propose a next move rather than asking the human what they would like to do.

---

## The authoring grammar, in brief

A piece is a layered SVG. Canonical layers: `silhouette`, `cutouts`, `panels`, `folds-valley`, `folds-mountain`, `axles`, `attach-points`, `marks`.

**Panels-first** (DECISIONS #6, #7): the author names every panel as a closed polygon with a bare-alias id (`main`, `taba`, `pane3`, `bh`), and every fold names the two panels it joins — `fold-pane3-pane4`. An optional suffix gives a default angle (`fold-stem-tabA-90`); an optional ordinal prefix gives fold *order* (`2-fold-pane4-pane5`), which no amount of geometry can recover. Fold direction is encoded by which layer the path lives in, not by sign.

Cross-piece attachment is `attach-<marker><piece>`, resolved against the partner piece's own markers through an eight-step lookup ladder with shortest-match tiebreaking. Marks are the preferred target — a mark's centroid is the exact connection point, where a panel is only a region.

The parser is deliberately not clever. **If it cannot resolve something, the drawing is missing a name.**

---

## Repository map

```
source/          reference archive — scans, transcriptions. Read-only. Complete.
work/            the build
  pieces/NNN/    NNN.af (Affinity) · NNN.svg (export) · NNN.json (sidecar)
  pieces.csv     124-row master index (123 pieces; 093 split into a/b)
  pipeline/      Python trace pipeline — gen-1 era, awaiting a reshape
  SPEC-*.md      design specs, frozen — read their headers before trusting them
claude-work/     agent-led working surfaces
  CHARTER.md     the collaboration charter; amendment A4 closes it with a scorecard
  STATUS.md      per-track state, reconciled and frozen
  QUEUE.md       closed
  DECISIONS.md   fourteen decisions with reopen triggers
  scripts/       build_assembly_graph.py · preview_bridge.py · watch_and_render.py
  state/         generated — connection-graph.{json,md}
  to-alan/       rework requests and per-block briefs
site/            public-facing site — v0 drafted, never deployed
sessions/        95 session notes. The most trustworthy history here.
_archive/        33 shipped task prompts — the real decision record
preview.html     8,385-line single-file authoring + QA viewer
HANDOFF/         start here
```

---

## Tooling you would not guess at

**`claude-work/scripts/preview_bridge.py`** — a local server on port 7777. `preview.html` has a "→ Claude" button that POSTs the current parsed piece state to `/dump/preview`, landing it in `claude-work/state/` where an agent can read it; and a `/save` endpoint that merges assembled poses straight into the piece's sidecar. When it is offline the page dims the button and falls back to a copy modal. This solved a genuinely hard problem — getting state out of a sandboxed browser page and into the repository without copy-paste.

**`claude-work/scripts/watch_and_render.py`** — a trigger-file daemon. Drop a file containing a piece id into `claude-work/state/render-triggers/`; it renders that piece headlessly and writes a PNG, a log and a JSON summary. Round trip about ten seconds. This is how an agent that cannot open a browser gets to *see* its own work.

Understand both before concluding you cannot verify something.

---

## Environment

- Python 3.12 on the human's bench; scripts run from the repo root.
- The agent sandbox has **no browser and no reachable package registries**. Do not plan around installing dependencies there.
- Line endings are pinned by `.gitattributes`. If you ever see hundreds of files spuriously modified, it is line endings — `git reset --hard`.
- Work happens on `main-claude` or `main-gpt` and their per-task branches (`claude/<task>`, `gpt/<task>`). Never on `main`.
