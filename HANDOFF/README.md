# HANDOFF — z-paper-clock

**Freeze point:** commit `5a6b49b` (2026-05-10), tagged `pivot-2026-08-22`
**Reconciled and frozen:** 2026-08-22

---

## What this is

A personal project rebuilding the working paper clock from James Smith Rudolph's *Make Your Own Working Paper Clock* (1983) as an interactive 3D model on the web. Alan built one out of paper in the mid-1990s; it worked. This is the return, thirty years later, with an AI collaborator.

It ran hard for twelve days — 2026-04-29 to 2026-05-10, 171 commits, 94 session notes — and then stopped. It is now frozen and split into two lines that move forward independently and will not merge:

| Branch | Driver | Status |
|---|---|---|
| `main` | nobody | Frozen. Do not commit here. |
| `main-claude` | Claude | Continues under the existing charter. |
| `main-gpt` | a ChatGPT agent | Free to keep, adapt, or discard all of it. |

Per-task branches are `claude/<task>` and `gpt/<task>`.

---

## The repository tells the truth about itself

This is the important thing to know before you start reading.

When work stopped, the summary documents had drifted about a day behind the git log. They recommended shipping something that had already shipped, reported a file as missing that existed, described a settled architecture decision as open in five places, and stated the connection-graph size three different ways. That drift is normal on a fast-moving project and lethal to an incoming caretaker.

So before freezing, the repository was **reconciled against itself**. Every live surface was corrected. Every historical document got a dated freeze header naming what in it is no longer true. Four long-standing factual questions about the physical pieces were settled against the plates and the printed instructions rather than left open.

**You can trust what you read here.** Where a correction was made, it says so inline and gives the date. `HANDOFF/RECONCILIATION.md` is the complete record of what changed.

---

## Where to start

1. **`PROJECT-STATE.md`** (repo root) — what the project is, what exists, and an honest list of what does not. Reconciled. 10 minutes.
2. **`HANDOFF/PICKUP-GUIDE.md`** — three entry ramps with tradeoffs, a recommended first hour, and a list of ways to waste your time.
3. **`claude-work/CHARTER.md`** — the collaboration model, and amendment A4 at the end: an honest scorecard of what it did and did not achieve.
4. **`claude-work/DECISIONS.md`** — fourteen numbered decisions, each with rationale and an explicit reopen trigger. The most reusable artifact in the project.
5. **`LAYER-CONVENTIONS.md`** — how a paper piece is described as layered SVG. This is the project's core technical invention and the thing you most need to understand.

`HANDOFF/RECONCILIATION.md` when you want to know what we changed and why. `HANDOFF/DIVERGENCE-LOG.md` is empty and yours to fill.

---

## Where the work actually stands

**The study is finished.** All 123 pieces scanned at roughly 613 DPI, individually cropped, losslessly archived. The whole book transcribed — prose, instructions, embedded labels. This is the most reliable material in the repository and is not under active design.

**The build is roughly a quarter done.** 32 SVGs authored across 41 piece folders; 28 pieces in the connection graph; 51 declared cross-piece connections with 30 resolving. Four JSON sidecars. An 8,385-line single-file preview tool that folds pieces in three.js, co-locates subassemblies, snaps connection points, and walks a guided assembly sequence — with a local bridge server so the browser can write back into the repository.

**What does not exist:** the production viewer, the assembly engine, any mechanism simulation, any public deploy, and sidecars at scale. Each of those is real intent with a real design behind it, and each is downstream of the actual bottleneck — one person at a desk in Affinity Designer, tracing paper clock parts one at a time.

---

## If you are the ChatGPT agent

Start at **`AGENTS.md`** in the repository root. It is vendor-neutral and points at everything you need.

The operating model here is unusual and worth understanding before you discard it. A signed charter put the *agent* in the lead on direction, sequencing, architecture and the work queue, and the human in a supporting role at the bench. It produced most of what is in this repository. `claude-work/CHARTER.md` documents it, and its closing amendment says plainly what it got right and what it got wrong.

You inherit no obligation to any of it.

---

## If you are Claude

You are inheriting your own notes, now corrected.

Two things. First: three and a half months of dormancy is real, and Alan's memory of where things stood has decayed alongside yours. Do not open by asking what he wants to do next — that is precisely the failure mode the charter exists to prevent. Read, form a view, propose.

Second: the drift that made this reconciliation necessary was not carelessness. It was hand-maintained summaries losing a race against a fast git log. If you keep `STATUS.md` and `QUEUE.md` in their current form, they will drift again. Consider generating parts of them, or accept the lag and say so on their face.

---

## Housekeeping

- **`.gitattributes` pins LF.** Before it existed, a Windows checkout reported all 213 tracked text files as modified — a 53,586-line phantom diff that was purely line endings. If you ever see that again, `git reset --hard` is safe.
- **The repository is large** (~1 GB working tree, 621 MB of history) because it carries a lossless scan archive. That is intentional.
- **Never republish the book.** `source/` is personal reference. Derivative work only, everywhere, always. The book is in print; the correct answer to "can I see the source" is "buy a copy."
