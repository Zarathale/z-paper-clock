---
date: 2026-08-23
start_time: "not recorded"
end_time: "14:16"
mode: code
participant: Zarathale (Alan)
target: anchor-cluster-depth
---

## Goal

Resume the GPT line from the freeze and close the next safe anchor-cluster decision: place the two face pieces at the physical ends of piece 066 rather than leaving all three at Z=0.

## What was done

- Read the required handoff, project state, layer conventions, decision record, status, queue, latest session, and relevant viewer implementation.
- Reviewed pieces 065-069 from the repository and presented the actual SVGs in chat for Alan's decision.
- Alan confirmed the physical stack under the repository convention that +Z is toward the viewer:
  - 065 anchor-arm face: Z=+10 mm
  - 066 bearing box: Z=0
  - 067 rear plate: Z=-10 mm
- Created `gpt/anchor-cluster-depth` from `main-gpt`.
- Updated 065 and 067 sidecars with the agreed translations and explicit provenance.
- Kept the derived-pivot convention unchanged: authored pivot markers seed a cluster; pieces 065, 066 and 068 inherit membership through the connection graph rather than receiving invented pivot markers.
- Initialized the GPT line identity and recorded the decisions in `HANDOFF/DIVERGENCE-LOG.md`.

## Verification

### Depth

Piece 066's seven body panels are approximately 2001 SVG units wide. At the sidecar/viewer scale of 0.01016 mm/unit, the bearing box depth is about 20.3 mm, so its end planes are approximately Z=+10.2 and Z=-10.2 around the Z=0 mid-plane. The selected +/-10 mm plate offsets are therefore the correct precision for the current sidecars.

### Inherited 066 XY transform

The inherited transform `[-23.9, -70.8, 0]` was not promoted to verified.

A deterministic reproduction of `preview.html`'s panels-first transform chain found that the 2026-05-10 derivation held `pane1` fixed. The live viewer instead selects `pane2`: it has maximum hinge degree and wins the alphabetical tie-break. The folded ring itself is coherent (approximately 31.24 mm radius in the reproduction), but its center is root-dependent in scene coordinates. The old translation therefore cannot be considered verified against the live renderer.

The numeric transform was preserved to avoid replacing one unverified pose with another. Its sidecar note and provenance now label XY as provisional while retaining Z=0 as verified.

### Static checks

- All edited sidecars remain valid JSON.
- No SVG artifact-truth was changed.
- No pivot markers or piece identities were invented.
- No HTTP server was started.

## Open items

- Re-derive 066's complete pose against the live `pane2` root, including the currently zero-valued face-flap folds and the front/rear handedness implied by the authored b-h glue relationships.
- Piece 068 still has no pose sidecar. Its SVG fold bug is fixed, so it is the next capture after 066 is made trustworthy.
- Ring-lock event delegation remains unexercised in a real browser.

## Branch / commits

- Branch: `gpt/anchor-cluster-depth`
- Base: `main-gpt` at `6fb127c1afc8f1383cc45ed67fead61df5c16d59`
- Pull request: pending at session-note write

## Next-session handoff

Finish 066 before authoring 068. Use the authored 065↔066 b-h glue surfaces to settle bearing-box handedness and rotation, then record a root-aware 066 transform. Once that reloads coherently, capture 068 and align its g/h/i connections to 069.
