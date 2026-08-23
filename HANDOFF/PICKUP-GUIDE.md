# PICKUP-GUIDE — where to start

*Three entry ramps, a recommended first hour, and a short list of ways to waste your time.*

---

## The first hour

**1. Get `preview.html` open in a real browser.** Double-click it — no server, no build step, it runs from `file://`. Load `?piece=069`, then `?piece=066`. Drag the fold sliders. Switch to Cluster mode and load `065,066,067`. This is the beating heart of the project and you cannot reason about the work without having watched it move. *(Do not start an HTTP server to do this — see below.)*

**2. Read one authored SVG as text.** Open `work/pieces/066/066.svg` and find the `panels`, `folds-valley`, `folds-mountain`, `attach-points` and `marks` layers. Trace one fold id — `fold-tabaa-pane7` is the interesting one — back to the two panels it names. Thirty minutes of real markup teaches the authoring grammar better than `LAYER-CONVENTIONS.md` does.

**3. Regenerate the connection graph.** `python3.12 claude-work/scripts/build_assembly_graph.py` from the repo root. It reproduces the committed `claude-work/state/connection-graph.{json,md}` — verified at the freeze. If it ever stops doing that, that discrepancy is your first task.

**4. Read `claude-work/DECISIONS.md` end to end.** Fourteen decisions, each with a reopen trigger. It is short, and it will save you from relitigating things that took real work to settle.

You do **not** need to spend the first hour hunting for stale claims. That was done at the freeze; `HANDOFF/RECONCILIATION.md` records what changed.

---

## Ramp A — Close the anchor cluster

**Best if:** you want to understand the whole system before changing any of it, and Alan has bench time.
**Size:** one or two sessions. **Needs Alan:** yes, briefly.

The anchor cluster (065–069) is the furthest-advanced subassembly and the only place where every tool gets exercised end to end: Affinity → SVG → parser → face graph → preview → bridge server → sidecar → connection graph.

1. Load `065,066,067` in Cluster mode and check whether 066's computed translation `[-23.9, -70.8, 0]` actually lands the pivot box centred on the anchor pivot. That number was derived by hand — seven pane heights resolving to a cyclic-polygon circumradius of 31.2 mm, closure gap 0.53 mm at the saved fold angles — and **was never verified in a browser**. Correct with TransformControls if it is off, and save.
2. Test the ring-lock event delegation fix in Bench mode on 066. Drag one pane fold with the lock on; the other five should redistribute to hold Σ constant while the closure fold stays put. It shipped and was never exercised.
3. Capture 068's pose sidecar. It is the only anchor-cluster member without one, and its fold bug is fixed — `fold-c2-pane3` bridges the slot cluster into the main pane chain.
4. Decide the Z-depth question. 066's walls span roughly −10 mm to +10 mm; 065 and 067 are both saved at Z = 0, so the face plates pass through the mid-wall instead of sitting flush at the open ends. Either push them to ±10 mm or accept the approximation and write that down.
5. Decide what a pivot cluster means. `pivot_clusters.anchor` is `[067, 069]` because only those two declare `pivot-anchor`. If the cluster means "pieces sharing this physical axle," author the marker on 065, 066 and 068. If it means "pieces that pivot on it," two is already right. Do not expect regeneration to change it — see `RECONCILIATION.md`.

---

## Ramp B — Debt paydown and pipeline reshape

**Best if:** you are an agent working alone, or Alan is unavailable.
**Size:** several focused sessions. **Needs Alan:** barely.

The documentation debt is paid. What remains is mechanical and blocks everything downstream.

**The pipeline reshape — tasks M0.5.6 through M0.5.9.** `01-crop.py` sliced whole plates into pieces; chunk-and-crop made that obsolete in April 2026 and nobody removed it. Archive it, repoint `02-trace.py` at `source/pieces/`, update the Makefile, re-run trace and layer-split on plate D's eleven pieces (4, 10, 18, 19, 26, 29, 30, 31, 32, 91, 92) against the good gen-2 scans, open one result in Inkscape to confirm the silhouettes come out rectilinear, and close M0.5.

This matters more than it looks. The pipeline is the only path to authoring ninety-odd remaining pieces at anything faster than fully manual speed, and it currently points at a scan generation that was deleted.

**The sidecars.** Four exist. The old roadmap called the per-piece JSON sidecars the highest-leverage batch task in the project and estimated four hours for all 123; that estimate is worthless — see the freeze header on `SPEC-3D-VIEWER.md` — but the underlying observation holds. Most sidecar content is mechanical and derivable from the transcriptions.

---

## Ramp C — The gear train

**Best if:** Alan has real bench appetite. **Size:** the largest authoring block in the project, ~50 pieces. **Needs Alan:** constantly. **An agent cannot move this alone.**

A full planning brief exists at `claude-work/to-alan/gear-train/README.md`: kinematic chain, shared axles, five sub-stack maps, recommended order. It was written 2026-05-09 and never started.

Recommended order: motor wheel (33–49) → middle wheel (50–57) → escape wheel (58–64) → reduction gear (81–87) → hands assembly (73–80, 088–092a, 108, 109).

Two things make this more attractive than it first looks. **Twenty-one of these pieces already have Affinity sources started** in the 033–049 range — the motor wheel is partly underway, it just has no SVG exports. And **the escape wheel forces a decision deferred all project**: 058+059 is where the first `function` block gets authored, which locks the mechanism-geometry schema that has been a draft since April. Zero `function` blocks exist anywhere. Expect to revise the draft schema on contact.

Once the escape wheel exists alongside the finished anchor, the first real mechanism demo becomes possible — a two-subassembly scene with a tick.

---

## Recommendation

**Ramp A first, then B.** A is small, it is the natural resumption point, and it teaches you the system by making you use all of it. B then unblocks everything downstream. C is the biggest prize but it is gated on human bench time, and starting there without having done A means authoring fifty pieces against conventions you have not personally stress-tested.

---

## Ways to waste your time

- **Do not start an HTTP server to test `preview.html`.** It is a single file designed for `file://`. Worse, terminal agents run inside a git worktree, so a server started there serves the *main* repo's copy of the file rather than your edited one — you will verify the wrong thing and conclude your change failed. Static checks gate the commit; browser checks gate the merge and belong to a human. "Browser verification blocked" is a valid session outcome.
- **Do not rebuild the parser.** Cut-line-first was built, refined through three increasingly clever algorithms, and deliberately retired in DECISIONS #6. Panels-first is authoritative and the parser is not supposed to outsmart the author. If it cannot resolve something, the SVG is missing an id.
- **Do not build the production viewer yet.** DECISIONS #4 settled it: fresh TypeScript at `claude-work/viewer/` when M3 is imminent, no code shared with `preview.html`, and M3 is not close. `work/viewer/` is an empty stub that will never be populated.
- **Do not fan out parallel asks to Alan.** The charter is explicit — the queue stays at three to five items, because the constraint is one person's bench time and a long queue defeats the iteration discipline that made each piece teach something.
- **Do not invent piece numbers or label notation.** They come from `source/transcriptions/embedded-labels.md`. If it is not there, it does not exist.
- **Do not republish the book.**
