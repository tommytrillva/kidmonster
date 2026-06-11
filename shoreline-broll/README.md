# Shoreline / Endless Summers — Tutorial B-Roll

Premium cinematic motion-graphics B-roll for the "this music video was made with AI" YouTube tutorial.
Built with [HyperFrames](https://hyperframes.heygen.com) — the HTML is the video source.

- **Runtime:** 5:11 (311s) · 1920×1080 · 16:9 · no audio (music/VO added in DaVinci Resolve)
- **No baked-in text** — all labels are abstract glyph bars, all tools are abstract glass nodes.
  Add readable text in Resolve on top.
- **Style:** Y2K Xbox acid-green on near-black, glassmorphism, warm sunset bleed, VHS grain
  (see `frame.md` for the full design spec).

## Timecode map (matches the tutorial script)

| Time | Scene file | Beat |
|------|-----------|------|
| 0:00–0:16 | `s01-almost-closed` | overwhelming waveform, cursor hesitates at close, becomes AI timeline |
| 0:16–0:30 | `s02-shoreline` | waveform → ocean horizon of light, heartbeat pulse |
| 0:30–0:54 | `s03-old-vs-ai` | film gear dissolves into particles → AI node network outputs frames |
| 0:54–1:09 | `s04-workflow-map` | 7-node glass pipeline map, pulses run the cables |
| 1:09–1:30 | `s05-edit-timeline` | clips snap on beat → montage wall |
| 1:30–2:05 | `s06-process` | buzzword fog wiped → organized 5-column creative pipeline |
| 2:05–2:29 | `s07-why` | client revision chaos glitches away → one personal world node |
| 2:29–3:05 | `s08-lab` | floating experiment screens, best takes pulled into a storyboard |
| 3:05–3:43 | `s09-planning` | run-and-gun chaos freezes → storyboard grid + GPS route |
| 3:43–4:16 | `s10-feelings` | emotional moodboard assembles into a palette |
| 4:16–4:46 | `s11-vhs-scanner` | VHS cassette becomes light → memory frames spill out |
| 4:46–5:11 | `s12-one-shot` | full reference→shot pipeline as one glowing system, resolve + fade |

Scene boundaries overlap by ~1s; the root composition (`index.html`) owns all transitions
(blur crossfades, scanline wipes, soft glitches, a light-leak into 3:43, a VHS tracking wipe into 4:16)
plus the global film grain / scanlines / vignette overlay.

## Commands

```bash
npm install          # once
npm run dev          # studio preview (http://localhost:3002/#project/shoreline-broll)
npm run check        # lint + validate + inspect
npm run render       # MP4 at 1920x1080
npx hyperframes render --quality high --output endless-summers-broll.mp4
```

## Getting 4K

The composition is authored at 1920×1080. For the 4K master, either render at 1080p and use
DaVinci Resolve's Super Scale (2x) on import — grain/glow content upscales cleanly — or ask the
agent to produce a 2× scaled variant of the composition.

## Editing in Resolve

Each scene is also renderable in isolation if you want separate B-roll clips instead of one long file:
temporarily set `data-duration` of the root to the scene's range, or just render the full file once and
blade-cut at the timecodes above (transitions land exactly on the listed boundaries).
