# HI-282 increment 2 — stage backdrop candidates

Staging only — Viper's playtest pick decides any swap; the live set at
`public/assets/backgrounds/` is never touched by this lane.

- **A/B sheet:** `python3 -m http.server 8793 --bind 0.0.0.0` run from
  `public/assets/`, then open
  `http://10.0.40.202:8793/backgrounds-candidates/sheet.html`
  (OLD reads the live set via `/backgrounds/<scene>.jpg` — serve the
  parent `assets/` dir, not this one, or the originals 404).
- **Generate candidates:** `python3 scripts/backdrop-candidates-gen.py`
  (route auto: ComfyUI z-image → codex; `--wait-comfy 90` polls a down box;
  `--list` prints the prompt pack without spending anything).
- **Gate candidates:** `python3 scripts/backdrop-candidates-check.py`
  (painterly-family bars vs the five originals; `--selftest` proves the
  bars offline, `--baseline` re-measures the originals).

**2026-09-15 fill (the court has its cells):** ComfyUI moved — the Olares
box died; the Windows/RTX-4090 replacement answers at `10.0.10.33:8188`
(`COMFY_URL` overrides). Its only image checkpoint is DreamShaper8_LCM,
so the `comfy-ds` route carried the fill (the z-image wiring resolves
nowhere on the new box). Nine candidates staged, all past the
painterly-family gate: four scenes × A/B at 8 steps cfg 1.8 (the
best-looking in-family schedule), plus **zone-1/B at 16 steps cfg 2.5**
(`DS_LCM_STEPS`/`DS_LCM_CFG`) — the volcanic calm-stone brief is
structurally smooth on this model: its A variant measured flat-run
0.43-0.71 across 12 seeds at 8-16 steps and is honestly NOT staged (see
`candidates.json` `notes`); the original rides zone-1's A side. Seeds and
sampler params are recorded per run in `candidates.json`; the manifest
merges by (scene, variant), so a `--scene X --seed-offset N` re-roll
never clobbers the other scenes' staged cells.
