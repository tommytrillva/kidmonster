# Scene Sub-Composition Contract (READ FULLY BEFORE WRITING CODE)

Every scene file in `compositions/` MUST follow this exact structure and these rules.
The design spec is `../frame.md` (exact hex values, components, hard "What NOT to do" rules).
The creative brief for each scene is in `.hyperframes/expanded-prompt.md`.

## File template (replace SID with your scene id, e.g. `s03`)

```html
<template id="SID-template">
  <div data-composition-id="SID" data-width="1920" data-height="1080">
    <!-- content: plain divs/SVG. NO nested data-start clips. NO <br>. NO text characters anywhere. -->
    <style>
      /* EVERY selector scoped with the [data-composition-id="SID"] prefix */
      [data-composition-id="SID"] {
        position: absolute;
        inset: 0;
        width: 1920px;
        height: 1080px;
        background: #050a06;
        overflow: hidden;
      }
      [data-composition-id="SID"] .my-thing { /* ... */ }
    </style>
    <script src="https://cdn.jsdelivr.net/npm/gsap@3.14.2/dist/gsap.min.js"></script>
    <script>
      (() => {
        window.__timelines = window.__timelines || {};
        const tl = gsap.timeline({ paused: true });
        const S = '[data-composition-id="SID"] ';
        // tweens use S + ".selector" so they never hit other scenes
        // ...
        window.__timelines["SID"] = tl;
      })();
    </script>
  </div>
</template>
```

## Hard rules (violating ANY of these ships a broken video)

1. **Local time.** Your timeline runs 0 → your scene's local duration (see scene map). t=0 is when the
   root starts crossfading you IN over the previous scene (~1s). Schedule your first entrance at t≥0.3.
   Your scene must look COMPLETE and alive at its final frame — the next scene crossfades over you.
   **NO exit animations at scene end** (except s12, which is the finale and fades out).
2. **`tl.fromTo()` for every entrance/appearance** — explicit both-end states. Elements that appear
   mid-scene: their CSS is the visible hero state; the `fromTo` "from" hides them (GSAP holds the from
   state before the tween's start time).
3. **One transform tween per element.** Entrance + ambient on the same element = split into wrapper
   (entrance) + child (ambient), or combine into a single `fromTo`. NEVER stack two transform tweens
   on one element.
4. **All motion on `tl`.** Never bare `gsap.to()` / `gsap.set()` outside the timeline — it won't render.
5. **No `repeat: -1`.** Finite repeats: `repeat: Math.ceil(remaining / cycle) - 1`.
6. **Deterministic.** No `Math.random()` / `Date.now()`. Use mulberry32:
   ```js
   const rng = (seed => () => ((seed = (seed * 1664525 + 1013904223) >>> 0) / 4294967296))(42);
   ```
   (or proper mulberry32 — any seeded PRNG). Generated layouts (particles, bars) are built by JS
   creating DOM nodes synchronously at script top, before tweens reference them.
7. **Synchronous script.** No async/await/setTimeout/Promises/fetch. No images, no videos, no fonts.
8. **NO TEXT.** Zero readable or random characters anywhere — no letters, numbers, punctuation glyphs.
   "Labels" are glyph bars (rounded pills, see frame.md). Icons are pure CSS/SVG geometry. No logos.
9. **Colors only from frame.md.** bg #050a06, fg #eaf5e2, accent #8fe000, accent-bright #c6ff4d,
   accent-deep #3e8e0e, sunset-orange #ff8a3d, sunset-gold #ffc65c, sunset-rose #ff6473,
   ocean-teal #35d0ba, glass fills/strokes as specified. Tints = rgba() of these. Never #000/#fff,
   never cyan/purple/blue.
10. **Gradients:** never the `transparent` keyword (use the color at 0 alpha); no full-screen linear
    gradients over the dark bg (radial or solid + localized glow instead).
11. **No grain/scanlines/vignette** in scenes — the root overlay provides them globally.
12. **Density:** 8–12 visual elements; 2–4 BG decoratives, all with slow finite ambient motion on `tl`;
    ≥3 different eases among entrances; durations mixed (some 0.25s, some 0.7s+, ambient 3–6s cycles).
13. **Sizes for video:** strokes 2px+, decorative opacity 12–25%, glyph bars 6–12px tall, icons 36px+.
    Elements intentionally animating across edges get `data-layout-allow-overflow`; pure decoratives
    that should never be layout-audited get `data-layout-ignore`.
14. **SVG:** fine for cables/paths. Stroke-draw via `stroke-dasharray`/`stroke-dashoffset` animated ON `tl`
    (set dasharray in attribute/CSS, tween `strokeDashoffset` with gsap `attr` or css). Give every SVG
    explicit `width`/`height`/`viewBox`.
15. **Filters sparingly:** `filter: blur()` tweens only on small/medium elements (not full-frame layers).
16. Mid-scene morphs/dissolves (e.g. chaos board draining away at a scripted beat INSIDE the scene) are
    allowed and choreographed in the brief — those are content, not scene exits. After any mid-scene
    fade-out, hard-kill: `tl.set(el, { opacity: 0, visibility: "hidden" }, tEnd)`.

## Quality bar

This is premium B-roll: Apple-keynote polish over a Y2K Xbox-green palette. Glassmorphism per frame.md
component recipes (glass-fill bg, 2px glass-stroke border, top sheen, soft outer green glow). Movement is
cinematic: slow camera-style drifts on wrapper containers, eased entrances, breathing glows, traveling
cable pulses. Nothing static, nothing cluttered, nothing texty.
