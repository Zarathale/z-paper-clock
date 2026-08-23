# DIVERGENCE-LOG

*One of these lives in each line. It starts empty. Fill it as you go.*

---

## Why this file exists

`main-claude` and `main-gpt` start from the same commit and will never merge. That makes them, whether or not anyone intended it, a natural experiment: the same project, the same inherited state, two different drivers.

That experiment is only legible later if both sides write down what they chose. Six months from now, `git diff main-gpt main-claude` will show *what* differs. Only this file can show *why*.

Keep it cheap. A few lines per entry. If writing an entry feels like a chore, the entry is too long.

---

## What to record

**Record:**

- A convention you kept, changed, or abandoned — and the reason.
- A decision from `claude-work/DECISIONS.md` you reopened, and what you concluded.
- A part of the operating model (charter, lanes, prompt lifecycle, queue) you adopted, modified, or dropped.
- A direction you took that the other line probably would not have.
- Something the handoff package got wrong.

**Don't record:** ordinary task progress. That is what `sessions/` is for.

---

## Format

```
### YYYY-MM-DD — short title
**Kind:** convention | decision | process | direction | correction
**What:** one or two sentences.
**Why:** one or two sentences.
**Reversible?** yes / no / costly
```

---

## Line identity

> - **Branch:** `main-gpt`
> - **Driver:** Codex, GPT line
> - **Started:** 2026-08-23
> - **Opening stance:** Preserve the artifact-first data model and the useful parts of the inherited operating discipline, but require deterministic geometry or a human observation before promoting an assembly pose from provisional to verified. Prefer closing small physical ambiguities in sidecars over adding viewer machinery.

---

## Entries

### 2026-08-23 — Physical depth is assembly state
**Kind:** decision  
**What:** Place 065 at Z=+10 mm and 067 at Z=-10 mm around 066's Z=0 mid-plane. Keep the existing derived-pivot convention: pivot markers seed the cluster; connected members inherit membership.  
**Why:** The bearing box is about 20.3 mm deep, and Alan confirmed the anchor-arm face/front versus rear-plate ordering. Leaving both plates at Z=0 erased a real physical relationship.  
**Reversible?** yes

### 2026-08-23 — 066 XY pose downgraded
**Kind:** correction  
**What:** Keep the inherited 066 transform numerically unchanged for now, but mark its XY placement provisional.  
**Why:** Its 2026-05-10 derivation held `pane1` fixed, while the actual `preview.html` hinge-tree rule selects `pane2` (highest degree, alphabetical tie-break). A root-aware re-derivation is required before the pose can be called verified.  
**Reversible?** yes
