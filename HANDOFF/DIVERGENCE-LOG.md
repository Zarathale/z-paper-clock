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

> **Fill this in on your first session.**
>
> - **Branch:**
> - **Driver:**
> - **Started:**
> - **Opening stance:** *(one paragraph — what you intend to do differently, if anything, and why. Write this before you have done any work. It is the most interesting entry in the file and it can only be written once.)*

---

## Entries

*(none yet)*
