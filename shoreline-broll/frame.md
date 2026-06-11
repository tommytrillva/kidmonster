# Endless Summers — Design Spec (frame.md)

Premium cinematic motion-graphics B-roll for the "Shoreline / Endless Summers" AI music-video tutorial.
Mood: high-end SaaS product demo × nostalgic VHS summer memory. Y2K original-Xbox acid green on near-black,
glassmorphism, warm sunset bleed, ocean particles, film grain.

```yaml
name: Endless Summers
canvas: 1920x1080 (16:9)
colors:
  bg: "#050a06"            # near-black, green-tinted. NEVER pure #000.
  bg-raise: "#0a140b"      # raised panel base
  fg: "#eaf5e2"            # green-tinted off-white (rare, glyphs/strokes only)
  accent: "#8fe000"        # Y2K Xbox acid green — primary UI / cable / glow color
  accent-bright: "#c6ff4d" # hot green core for glow centers, pulses
  accent-deep: "#3e8e0e"   # dim green for idle UI strokes, grid lines
  sunset-orange: "#ff8a3d" # warm bleed, horizon glow
  sunset-gold: "#ffc65c"   # highlights, light leaks
  sunset-rose: "#ff6473"   # dusk pink, halation edges
  ocean-teal: "#35d0ba"    # sea-spray particles, secondary data color
  glass-fill: "rgba(150, 230, 120, 0.07)"   # frosted panel fill
  glass-stroke: "rgba(143, 224, 0, 0.30)"   # panel border 2px
  glass-highlight: "rgba(234, 245, 226, 0.12)" # top-edge sheen
typography:
  # THIS VIDEO CONTAINS NO READABLE TEXT. No letters, no numbers, no words, no logos.
  # All "labels" are abstract glyph bars: rounded rects 6-10px tall in fg/accent at 35-70% opacity.
  # All "icons" are abstract geometry (CSS/SVG shapes), never brand marks.
rounded:
  chip: 8px
  node: 18px
  panel: 24px
  pill: 999px
spacing:
  pad-frame: 90px
  gap-md: 28px
  gap-lg: 56px
motion:
  energy: moderate-cinematic
  easing:
    entry: "expo.out"         # UI elements snapping/gliding in
    drift: "sine.inOut"       # ambient float / breathe / parallax
    camera: "power2.inOut"    # slow zooms, pans on scene wrappers
    impact: "power3.out"      # beat hits, node pulses
  duration:
    entrance: 0.5-0.9
    ambient-cycle: 3-6
    transition: 0.8-1.2
  atmosphere:
    - film-grain (global overlay)
    - vhs-scanlines (global overlay, very subtle)
    - radial accent glows (per scene, 15-25% opacity)
    - drifting particle fields (green spray / teal ocean dust)
    - hairline grid / horizon lines (accent-deep)
  transition: blur-crossfade primary; scanline wipe + soft glitch as accents
```

## Components

- **Glass node**: rounded 18px, `glass-fill` background, 2px `glass-stroke` border, inner top sheen
  (1px `glass-highlight` line or subtle linear overlay), soft outer glow `0 0 40px rgba(143,224,0,0.18)`,
  backdrop-blur look faked with layered translucency (no `backdrop-filter` — unreliable in capture).
  Inside: an abstract icon shape + 2-3 glyph bars.
- **Cable**: SVG path, 3px stroke `accent-deep`, with an animated bright dash/pulse in `accent-bright`
  (animate `stroke-dashoffset` on the timeline, finite repeats). Cables curve (bezier), never right angles.
- **Glyph bar** (fake text): rounded-pill div, height 6-12px, widths varied 40-220px, fg or accent at 30-70%.
  Group 2-4 bars with 8-10px gaps to suggest a paragraph/label. NEVER use real characters.
- **Waveform**: row of thin vertical bars (3-5px wide, 2px gap) or SVG polyline; accent color with bright core.
- **Frame card** (AI output "footage"): 16:9 rounded 12px card filled with a cinematic CSS gradient scene
  (sunset sky, ocean horizon, neon dusk) + grain, 2px glass stroke, slight perspective tilt.
- **Cursor**: 22px arrow (CSS triangle/SVG) in fg with soft drop shadow; moves with `power2.inOut`, never teleports.

## Cinematic gradient recipes (for frame cards / horizons)

- Sunset sky: vertical `#1a0f14 → #5a2233 → #b8503a → #ff8a3d → #ffc65c` with a `sunset-gold` radial sun glow.
- Ocean dusk: vertical `#04121a → #0d3340 → #35d0ba(30%)` + horizontal horizon hairline in `fg` 25%.
- Neon boardwalk: `#0a0612 → #2a1140` base + `sunset-rose`/`ocean-teal` radial neon pools.
- Use radial gradients or solid + localized glows for large backgrounds — avoid full-screen linear
  gradients on the dark bg (H.264 banding). Gradients on dark bg: alpha colors, never `transparent` keyword.

## What NOT to do (hard rules from the client brief)

1. NO readable text, letters, numbers, words, captions, or scrambled-character effects. Zero glyphs.
2. NO real or fake brand logos. Tools are abstract glass nodes with geometric icons only.
3. NO low-poly 3D look, NO clutter, NO random UI junk. Every element earns its place.
4. NO pure #000 / #fff. Tint toward green (dark) or warm (light highlights).
5. NO cyan/purple "AI slop" palette. Greens, warm sunset tones, one teal — nothing else.
6. NO static decoratives — everything breathes, drifts, or pulses (on the timeline, finite repeats).
7. NO hard jump cuts between scenes; transitions are handled by the root composition.

## Recurring motifs (thread through all scenes)

- The **shoreline line**: a horizontal glowing line that reads as both waveform baseline and ocean horizon.
- **Green pulse traveling along cables** — data flowing through the pipeline.
- **Warm sunset bleed** entering from a corner whenever emotion/memory wins over the cold interface.
- **Sea-spray particles**: 1-3px dots in accent/ocean-teal drifting slowly up-right.
- **Film grain + faint scanlines** (global overlay layer, applied once at root — scenes must NOT add their own).
