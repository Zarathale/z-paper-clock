# RECONCILIATION — what changed at the freeze, and why

*2026-08-22. Every change made to the repository between commit `5a6b49b` and the freeze commit. Nothing here is code; the working tree of the project itself is untouched apart from `work/pieces.csv` and the regenerated connection graph.*

---

## Why this pass happened

The repository went dormant on 2026-05-10 and sat for three and a half months. Its summary surfaces had drifted about a day behind its git log at the moment work stopped. The last working session's own note ends by describing an architecture decision as "still pending" that had closed three days earlier.

A fork multiplies that problem — two caretakers would each independently trust the same wrong documents. So the repository was reconciled against itself before branching.

**Two classes of document, two treatments.** Decision records describe what we believed at the time; editing them to be currently-true would falsify the record, so they got a dated freeze header naming what in them is no longer accurate, and nothing else. Live surfaces claim to be true right now, so they were corrected in place. One exception is noted below.

---

## Part 1 — Four factual questions, settled

These had been open in `pieces.csv` and the annotated instructions since May. All four were resolved on 2026-08-22 against the scans, the printed instructions, and the figure plates, and confirmed by Alan from his own build.

**Piece 103 is the weight-cylinder bottom, not a reduction gear.** It was filed under `reduction-gear` and described as "small reduction gear with central spiral pattern." What reads as gear teeth are trapezoidal glue tabs that fold up and glue against the inside of tube 101. §II.E: *"Form a tube from piece 101… Glue in the bottom, piece 103."* Its diameter matches the lid discs 104 and 106; compare piece 081, which has real pointed gear teeth, or 087, a plain reduction-gear disc with an axle cross and no teeth at all. → `section: weight`.

**Piece 074 is the rim strip of the minute-hand wheel, not an anchor-pendulum piece.** §II.D: *"Assemble pieces 73, 74, 75, and 76 to produce the wheel of the minute hand."* The neighbours label it directly — 073 carries `b74` three times around its rim and 075 carries `74` with a pointer. The strip zigzags because it wraps the twelve-point star profile of both wheels, structurally the same idea as 105 in the weight lid. → `section: hands`.

**The 093 brace geometry, from Figure 10.** The book calls for *"the six pieces designated 93… to form three separate braces."* Plate B prints them as **three identical pairs**, with two "93" labels and arrows fanning to all six shapes. Each pair is one **trough** — two long fold lines, pointed ends — and one **fin**, a vertical fold plus an L-shaped foot with a chamfered corner. Fig. 10 draws the fin dropping into the trough and the two glued into a single standing brace.

So `093a` (trough) + `093b` (fin) = one brace; three braces; six printed pieces. The 2026-05-05 split into two shapes was correct. What was wrong was the note claiming the brace template is "instantiated 6 times in piece 94" — it is three braces of two pieces each, glued inside 094 at the middle and five inches above and below. Alan's bench order, now recorded: cut all three troughs first, then the fins. Also noted: `source/pieces/093.png` captured one of the three printed pairs. The shapes repeat, so nothing is lost.

**A typo in the book, at §II.C.** The printed text reads *"…hold the pendulum bob in place on the pendulum rod, piece 94."* The same paragraph uses 94 twice as the bob casing. Fig. 13 settles it: **070** labels the long vertical rod running the height of the movement, **094** and **095** label the bob at the bottom. The sentence means piece 070. The transcription stays verbatim as printed; the annotated instructions now carry a `[GAP]` flag rather than silently asserting both readings.

---

## Part 2 — Live surfaces corrected

### `claude-work/STATUS.md`

Its `next_action` for the preview track told you to ship a prompt that had shipped as PR #29, and to capture a sidecar that already existed. Its "what's shipped" list stopped at PR B and omitted **seven merged ships** — marks-lookup, the bridge button, Cluster mode, snap, bridge save, the guided stepper, grouped fold sliders — leaving anyone who read only that list badly underestimating the tool. Its newest log entry said "066 + 068 still missing entirely" when 066's sidecar existed, and called 068 "blocked by two-component fold bug" when `QUEUE.md` recorded that bug fixed **in the same commit**. Its footer said two PRs still needed merging and described PR C as an unshipped draft at repo root; all were merged. Graph counts read 24/24 in two tracks and 30 in two others.

All corrected, with a freeze banner at the top and a final log entry recording the two ships that post-dated the file.

**A `site` track was added.** It should have existed since 2026-05-09 — charter amendment A2 created that zone and the launch session's own open question #8 asked for a track. Nobody added one, so a day and a half of site work ran with no representation on the live surface at all. The new track records the domain, the hosting, what was built, what was never deployed, and the two `.todo-alan` blocks that only Alan can write.

### `claude-work/QUEUE.md`

Closed out with a freeze banner. Now #1 struck as shipped; Now #2 corrected to show 066 done and 068 remaining.

**One entry was wrong on the merits, not merely stale.** It instructed: *"regenerate `connection-graph.json` so `pivot_clusters.anchor` reflects all five members."* Regenerating will never do that. `pivot_clusters` is derived from `pivot-<name>` markers in the SVG's **`attach-points`** layer, and only 067 and 069 declare `pivot-anchor`. (065 carries `anchor-pivot` in its `axles` layer, which names its own axle and is a different thing.) Verified by regenerating at the freeze: byte-identical output, cluster still `[067, 069]`.

Getting five members requires **authoring** markers on 065, 066 and 068 — bench work, not a script run. And it is worth deciding first whether the cluster should mean "pieces sharing this physical axle" or "pieces that pivot on it," because if it is the latter then two is already correct and the other three are rigidly attached, which is exactly what DECISIONS #7.19's derived-pivots rule assumes.

*This one is worth dwelling on. It is the only case found where a document would have sent someone to do the wrong work rather than merely redo finished work.*

### Elsewhere

**`README.md`** — rewritten status section: real counts, the architecture decision recorded as closed, a pointer to this package.

**`PROJECT-STATE.md`** — freeze banner; "17 panels-first SVGs" corrected to 32 across 41 folders with the actual piece list; the architecture-decision paragraph corrected and the seven subsequent ships named.

**`CLAUDE.md`** — the M0.6 and panels-first rows in the status table rewritten with real figures and the full 29-PR list; the repo tree's `work/viewer/` line corrected to say it will never be populated.

**`LAYER-CONVENTIONS.md`** — the 066-cluster exemplar table had two rows labelled `panel-substring` that the marks-lookup ship moved to `marks-landing-self` and `marks-exact`, and a following sentence claiming nothing falls back to mark-anchored lookup. Both fixed. The distinction matters: mark-anchored resolution is the documented *intent* of the mark-first pattern, not a fallback.

**`claude-work/standards/ENVIRONMENT.md`** — the `node --check preview.html` instruction fails on Node 24+ with `ERR_UNKNOWN_FILE_EXTENSION`. Replaced with the extract-the-script-body method that `CLAUDE.md` has carried since 2026-05-10.

**`claude-work/INSTRUCTIONS-ANNOTATED.md`** — the claim that the connection graph is "the digital equivalent of reading all the letter labels off all 123 pieces" corrected to the real 28-of-123 coverage. The §II.C piece list corrected for the 093 split and for three authored pieces it omitted (096, 099, 100). The book typo flagged. And a total that never closed: *"15 directed (7+4+3+1) = 11 distinct physical joints"* — neither reading yields 11, so the unsupported figure is gone.

**`claude-work/to-alan/gear-train/README.md`** — marked never-started, with its four open questions answered where possible. Two were settled, one is moot, and one is handed forward: the `function`-block JSON schema has never met a real piece, and whoever authors the first one (most likely on 058/059) should expect to revise it on contact.

**`work/pieces.csv`** — rows 074, 103, 093a and 093b rewritten per Part 1.

**`claude-work/state/connection-graph.{json,md}`** — regenerated. Semantically identical to what was committed: 28 pieces, 51 edges, 30 resolving, all provenance `authored`. The committed graph was current; regeneration confirmed it.

---

## Part 3 — Decision records frozen, not edited

**`work/SPEC-3D-VIEWER.md`** — a freeze header enumerating eight things in it that are no longer true: `work/viewer/` as a live target (named a dozen times), the "this decision is open" section, the claim that `preview.html` is read-only, the incomplete layer list, regions-as-derived, the auto-trace pipeline that never survived production, and the sidecar estimate of "~120 sidecars, 1–3 minutes each, ≈4 hours" against a reality of four sidecars in three weeks.

**The one approved exception to the no-edit rule:** its assembly-group table carries bracketed inline corrections. That table put **059** nowhere despite it forming half the escape wheel, omitted **087** entirely, listed 53 twice, and scattered pieces across the wrong groups. A frozen document is a record; a frozen document that would misdirect M4 authoring is a trap.

**`work/SPEC-REGIONS.md`** — a freeze header noting that its load-bearing premise, *"Regions are not authored — they are derived at load time,"* was reversed by DECISIONS #6 on 2026-05-05. It survives in code only as the legacy parser for pre-pivot pieces. Also flagged: TypeScript interfaces in a project with no TypeScript, a Shapely reference that is not in the venv, and a pointer to `WORKPLAN.md`, frozen since 2026-05-04.

**`WORKPLAN.md`** — already labelled frozen; a second banner notes the repository-wide freeze.

**`ROADMAP.md`** — **caught up before freezing.** Its M0.6 table stopped at task 0.6.14, leaving seventeen ships invisible. Rows 0.6.15 through 0.6.31 were added, one per merged PR from #13 through #29, and task 0.6.13 was flipped from `not-started` to `done` with its resolution. The milestone index above was deliberately left alone and the freeze header says its hour estimates are stale.

---

## Part 4 — The closing acts

**`claude-work/DECISIONS.md` gained #14** — the freeze and fork, in the same format as the thirteen before it, with the two-class reconciliation treatment recorded as part of the decision.

**`claude-work/CHARTER.md` gained amendment A4** — the charter closes, with an honest scorecard against its seven ship commitments plus the site track from A2. Three met, two partly met, three not reached, and the three not reached are the three that would have produced a clock. It also names what the charter got right (the role inversion, the small pull-based queue, the reopen-trigger field on decisions) and what it got wrong (hand-maintained summaries losing a race against the git log — the exact failure this pass spent its time repairing).

**A final session note** was written to `sessions/`, the ninety-fifth, per the repository's own convention.

---

## Part 5 — Structural

**`.gitattributes` added.** Every tracked text file showed as modified on the Windows checkout — 53,586 lines of pure CRLF-versus-LF, confirmed by an empty `git diff --ignore-all-space`. Left alone, an incoming agent would either panic or commit it. The file pins LF and marks binaries explicitly. The three `.rtf` files under `sessions/` are re-added byte-faithfully as a consequence; their content is unchanged in substance.

**`AGENTS.md` added at the repository root** — a vendor-neutral entrypoint, because `CLAUDE.md` is 87 KB of conventions that Claude tooling loads automatically and other agents do not.

**`HANDOFF/` added** — this file, a front door, a pickup guide, and an empty divergence log.

---

## What was deliberately not done

**No code was touched.** `preview.html`, the pipeline scripts, and `build_assembly_graph.py` are exactly as they were at `5a6b49b`.

**No SVG or sidecar was edited.** The authored corpus is Alan's lane and stays untouched.

**The unverified geometry stays unverified.** Piece 066's computed translation of `[-23.9, -70.8, 0]` was never checked in a browser, and the ring-lock event delegation fix was never exercised. Both are recorded as open rather than assumed correct.

**Nothing was retconned.** Where a document was wrong, the correction is dated and visible, and the original claim is left legible beside it. Anyone should be able to see not just what the project believed at the end, but where it had been mistaken along the way.
