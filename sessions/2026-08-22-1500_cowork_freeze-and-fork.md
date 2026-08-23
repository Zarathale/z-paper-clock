---
date: 2026-08-22
start_time: "15:00"
end_time: "17:40"
mode: cowork
participant: Zarathale (Alan)
---

## Goal

Freeze the repository, reconcile it against itself so the frozen state is coherent, and branch it into two independently-driven lines that are not intended to merge.

## What was done

### Framing

Alan opened by asking for a branch plus a handoff package. The first attempt produced a `HANDOFF/` folder that *catalogued* the repository's contradictions and left them in place. He reframed: the handoff package should *be* the fix — reconcile the repo within itself, make it as accurate as we can, and freeze that. Editing and rewriting fully open; we decide together what the frozen package is.

That reframe changed the proportions. Reconciliation became most of the work, and the handoff docs shrank because they no longer had to warn anyone about the repo they sit in. Two docs from the first attempt (`PROJECT-BRIEF.md`, `OPERATING-MODEL.md`) were dropped entirely as duplicating `PROJECT-STATE.md` and `CHARTER.md` + `CLAUDE.md`; a third (`STATE-OF-PLAY.md`) dissolved into the corrections themselves plus `RECONCILIATION.md`.

### The two-class principle

Settled early and it shaped everything after. **Decision records** describe what we believed at the time; editing them to be currently-true would falsify the record, so they take a dated freeze header naming what in them is no longer accurate, and nothing else. **Live surfaces** claim to be true right now, so they get corrected in place. The repo already had the idiom — `CLAUDE.md` prescribes exactly this header form for shipped CODE_PROMPTs — so we reused it rather than inventing one.

One approved exception: `SPEC-3D-VIEWER.md`'s assembly-group table carries inline bracketed corrections, because it omitted 059 from the escape wheel it forms half of and omitted 087 entirely. A frozen document is a record; a frozen document that would misdirect M4 is a trap.

### Four piece questions, settled

All four resolved against the scans, the printed instructions and the figure plates, then confirmed by Alan from his own build. Presented to him as a published visual page — pieces shown side by side with the relevant instruction text — which is what made them quick to answer.

- **103** → `weight`. What read as gear teeth are glue tabs that fold inside tube 101.
- **074** → `hands`. It is the rim strip of the minute-hand wheel; 073 and 075 both label it (`b74` ×3, `74`).
- **093** — Fig. 10 and plate B settle it. Three printed pairs, each a trough (093a) plus a fin (093b), glued into three braces. The split was right; the note claiming "instantiated 6 times" was wrong. Bench order recorded from Alan: **troughs first, then fins.**
- **094** — a typo in the book. The passage means piece 070. Transcription stays verbatim; the annotated instructions now flag it.

### Reconciliation

Eighteen files corrected. Full record in `HANDOFF/RECONCILIATION.md`. The headline items:

- `STATUS.md` — next-action a day and six merged PRs behind; "what's shipped" omitted seven ships; 066's sidecar reported missing when it existed; 068 reported blocked by a bug that `QUEUE.md` recorded fixed in the same commit. A `site` track was missing entirely and has been added — it should have existed since 2026-05-09.
- `QUEUE.md` — closed out. **One entry was wrong on the merits rather than merely stale:** it said to regenerate the connection graph so `pivot_clusters.anchor` reflects all five anchor members. Regeneration cannot do that — `pivot_clusters` derives from `pivot-<name>` markers in `attach-points`, and only 067 and 069 declare one. Verified by regenerating: byte-identical, cluster unchanged. Getting five members is bench work, and it is worth deciding first what a pivot cluster is supposed to mean.
- `ROADMAP.md` — caught up with seventeen missing ships (rows 0.6.15–0.6.31, one per merged PR #13–#29), then frozen.
- `DECISIONS.md` — gained #14, the freeze and fork.
- `CHARTER.md` — gained amendment A4, closing the charter with an honest scorecard against its seven ship commitments. Three met, two partly, three not reached — and the three not reached are the three that would have produced a clock.

### Verification discipline

Facts were rebuilt from primary sources rather than from the summary surfaces, which is how the QUEUE error surfaced and how an earlier claim of my own — that `pivot_clusters` was stale and needed regenerating — was caught and corrected before it reached a document. The connection graph was regenerated and diffed; it reproduces what was committed.

## Open questions

- 066's computed translation `[-23.9, -70.8, 0]` is still unverified in a browser, and the ring-lock event delegation fix was never exercised. Both are recorded as open, not assumed correct.
- 068 has no pose sidecar. Nothing blocks it.
- What a pivot cluster means — "shares this axle" or "pivots on it" — is genuinely undecided.
- The `function`-block JSON schema has never met a real piece. It locks on first contact, most likely on 058/059.

## Next-session handoff

There is no next session under this charter. `HANDOFF/PICKUP-GUIDE.md` carries three entry ramps for whichever line resumes first; Ramp A (close the anchor cluster) is the recommended opener.

## Note on tooling

Git could not be driven from the Cowork sandbox — the mount cannot finalize git objects, so `git add` fails partway and leaves orphaned temp files. Everything else (file writes, running Python, regenerating the graph) worked normally. The commit, tag, branch and push sequence was handed to Alan to run in his own terminal. Debris from the attempts was quarantined into `.git/_lock-quarantine/`, which is safe to delete.
