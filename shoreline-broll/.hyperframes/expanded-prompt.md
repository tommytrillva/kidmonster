# Expanded Production Spec — "Endless Summers" Tutorial B-Roll

Source of truth for all scene sub-compositions. Design tokens come from `frame.md` — use those exact
hex values. Total runtime 311s (5:11), 1920×1080, 12 scenes. NO readable text anywhere (glyph bars only),
NO logos, NO audio (music added in DaVinci Resolve).

## Rhythm declaration

`doubt-hold → DREAM-bloom → dissolve-REBUILD → map-pulse → SNAP-montage → wipe-organize →
glitch-PURGE → lab-drift → freeze-REORDER → feel-assemble → MEMORY-pour → unify-RESOLVE`

Energy peaks: s03 (icons→AI network rebuild), s05 (beat-snap montage), s11 (VHS memory pour).
Longest holds: s02 (shoreline breathe), s10 (moodboard), s12 (final glowing system).

## Global rules (every scene)

- Canvas-filling `.scene-content` (flex column, padding ~90px, width/height 100%, box-sizing border-box).
  Absolute positioning ONLY for decoratives and free-floating canvas items.
- 8–12 visual elements per scene: BG (2–4 decoratives w/ ambient motion), MG (the content), FG (accents).
- Background: `#050a06` base + radial accent glows at 15–25% + hairline horizon/grid lines in `#3e8e0e`.
  NEVER full-screen linear gradients on the dark bg. NEVER `transparent` keyword in gradients.
- Every decorative has a slow finite-repeat ambient tween ON THE SCENE TIMELINE (breathe/drift/pulse).
- Entrances staggered, ≥3 distinct eases per scene, first tween at local t≥0.3 (root crossfades the scene
  in during local 0–1s). NO exit animations (root transition is the exit) — EXCEPT scene 12 which resolves
  to a fade-out ending.
- Deterministic only: mulberry32 PRNG, no Math.random/Date.now. No `repeat:-1` — compute finite repeats.
- One transform tween per element (or split wrapper/child). Prefer `tl.fromTo` with explicit both-ends state.
- Grain/scanlines/vignette are GLOBAL (root overlay) — scenes must not add their own.

## Scene map (root timing — scene files are LOCAL time, 0 = clip start)

| # | file | root start | local duration | beat |
|---|------|-----------|----------------|------|
| 01 | s01-almost-closed.html | 0 | 16 | doubt → curiosity |
| 02 | s02-shoreline.html | 15 | 15 | waveform becomes shoreline |
| 03 | s03-old-vs-ai.html | 29 | 25 | film gear dissolves → AI network |
| 04 | s04-workflow-map.html | 53 | 16 | 7-node pipeline map |
| 05 | s05-edit-timeline.html | 68 | 22 | clips snap on beat → montage wall |
| 06 | s06-process.html | 89 | 36 | buzzword fog → organized pipeline |
| 07 | s07-why.html | 124 | 25 | client chaos → personal canvas |
| 08 | s08-lab.html | 148 | 37 | creator's lab, experiments |
| 09 | s09-planning.html | 184 | 39 | chaos path → storyboard GPS route |
| 10 | s10-feelings.html | 222 | 34 | moodboard assembles |
| 11 | s11-vhs-scanner.html | 255 | 31 | cassette → memories spill out |
| 12 | s12-one-shot.html | 285 | 26 | full pipeline in one motion, resolve |

---

## Scene 01 — "I almost closed it out" (16s)

**Concept.** A dark desktop workspace floats alone in a void. A music file opens into a waveform so dense
and alive it overwhelms the panel — intimidating power. A cursor drifts toward the close control… hesitates…
pulls back. The waveform then exhales and reorganizes into a calm AI video timeline. Doubt becoming curiosity.

**Mood.** 2001-Kubrick stillness meets a midnight DAW session. The interface is beautiful but slightly
too powerful for comfort.

**Depth layers.** BG: faint green grid (8% opacity) drifting, two radial accent glows breathing, sparse
sea-spray dots. MG: a large frosted glass window (rounded 24px, traffic-light dots as 3 plain circles —
no glyphs) holding a dense waveform of ~90 bars; a small file chip with abstract music icon. FG: cursor,
a circular "close" control top-right of the window, hairline baseline under the waveform.

**Choreography.** Window GLIDES up into place (expo.out, 0.9s, t≈0.5). File chip POPS (back.out, t≈1.6).
Waveform bars GROW staggered from baseline (0.02s stagger, power3.out, t≈2.2) then PULSE ambient — too tall,
some bars OVERSHOOT past the window edge (data-layout-allow-overflow). Window glow INTENSIFIES (t≈5).
Cursor SLIDES toward close control (power2.inOut, t≈7–9); close control GLOWS warning-warm (sunset-rose tint).
Cursor HESITATES (micro back-and-forth), PULLS BACK (t≈10.5). At t≈12 the waveform bars MORPH: scaleY settles,
bars re-tint toward accent-deep, a horizontal track structure (3 rounded track lanes + clip blocks) FADES UP
over the waveform area — the chaos LOCKS IN to an editable timeline. Camera (scene wrapper) does one slow
3% push-in across the whole scene.

**Transition out.** Root: slow blur-crossfade into s02 (the timeline's baseline becomes the horizon).

## Scene 02 — "You got to feel / shoreline" (15s)

**Concept.** Pure poetry beat. The audio baseline stretches into an ocean horizon made of light. Sea spray
of green particles, warm sunset bleeding into the dark UI from above the horizon. The shoreline line pulses
like a heartbeat. The most organic, least UI scene.

**Mood.** Vaporwave dusk without the kitsch — Apple ad restraint over a Kodak sunset.

**Depth layers.** BG: deep ocean dusk panel (radial glows: sunset-orange low on frame, rose halation),
slow-drifting teal particle field (~26 dots, mulberry32-placed). MG: the glowing horizon line (full-width,
2-3px, accent-bright core with wide soft glow), beneath it a "water" band of faint horizontal shimmer lines;
above it a soft sun disc (radial gold glow) rising very slowly. FG: a few waveform bars at far left fading
to dashes — the last trace of the UI — plus 2 thin hairline elevation lines.

**Choreography.** Horizon DRAWS across the frame (scaleX 0→1, power2.inOut, 1.4s, t≈0.6). Sun glow BLOOMS
(opacity+scale, sine.inOut 3s). Particles DRIFT up-right for the whole scene (single long linear tweens with
varied distance). Shimmer lines BREATHE (staggered opacity, sine). Horizon HEARTBEAT: scaleY/glow pulse every
~1.7s (finite repeats). Sunset wash FADES UP from 0 to 22% over 8s — warmth invading the interface. Waveform
remnant bars FLATTEN one by one into the horizon line.

**Transition out.** Root: blur-crossfade.

## Scene 03 — "This entire music video was made with AI" (25s)

**Concept.** The old way appears as ghost equipment — camera, drone, clapper, location pin, permit sheet,
crew chairs — frozen pale holograms on a planning grid. One by one they BURST into green particles; the
particles stream toward center and RECONNECT as a neural node network, which then outputs cinematic frame
cards: beach, car at sunset, boardwalk neon, VHS memory.

**Mood.** A production binder evaporating into pure capability. Awe, not menace.

**Depth layers.** BG: blueprint-style grid (accent-deep 10%), two breathing glows. MG: 6 ghost icon plates
(glass chips with abstract CSS/SVG icons, desaturated fg 35%) arranged in a loose arc; later the node network
(5–7 glass discs + bezier cables) center-left and 4 frame cards (cinematic gradient recipes from frame.md)
sliding out right. FG: particle bursts, cable pulses, tiny corner registration ticks (pure lines).

**Choreography.** Ghost plates MATERIALIZE staggered (blur+opacity fromTo, 0.6s each, t≈0.8–3.5), HOVER gently.
From t≈5, every ~1.6s one plate SHATTERS into 8–12 particle dots that STREAM (bezier-ish via x/y tweens) toward
center. Network nodes IGNITE as particles arrive (scale 0→1 back.out + glow pulse). Cables DRAW (stroke-dashoffset)
between nodes t≈13–16. Then pulses RACE along cables and frame cards DEAL out to the right one per pulse
(x+rotationY entrance, expo.out) t≈17–23. Cards get slow Ken Burns on a child layer.

**Transition out.** Root: scanline wipe into s04.

## Scene 04 — "Today I'm breaking down the tools" (16s)

**Concept.** A premium workflow map on an infinite dark canvas: seven glass nodes connect left→right in
pipeline order (Reference Board → Image Gen → Character Consistency → Image Animation → Upscale → Project
Org → Final Edit), each identified ONLY by an abstract icon. Green light flows through the cables, lighting
each node in sequence. This is the table of contents of the tutorial.

**Mood.** Figma-meets-mission-control. Calm mastery. The cleanest scene in the video.

**Depth layers.** BG: dot-grid (accent-deep dots 12%) with slow parallax pan, one large breathing glow under
the node row. MG: 7 glass nodes (≈150×120) in a gentle S-curve across the frame, connected by bezier cables;
each node holds a distinct geometric icon (grid of squares / aperture blades / twin silhouettes circles /
play-triangle in rings / up-arrow chevrons / folder shape / razor-split bar) + one glyph bar underneath.
FG: cable pulse dots, small index ticks (plain short lines) above each node.

**Choreography.** Canvas wrapper PANS slowly right→left 2% the whole scene (camera move). Nodes LAND in
sequence left to right (y-drop + scale, varied eases: expo.out / back.out(1.4) / power3.out, 0.45s apart,
t≈0.8–4). Cables DRAW behind them just-in-time. From t≈6: a bright pulse TRAVELS the full pipeline (dash
offset animation ~4s), each node FLARES + lifts 6px as the pulse passes (sine.inOut). Second pulse pass
t≈11–15. Icons each have a tiny idle motion (rotate/blink/bob — all different).

**Transition out.** Root: soft glitch into s05.

## Scene 05 — "Throw the footage into the timeline" (22s)

**Concept.** An abstract brandless NLE: track header column, 4 stacked timeline lanes, a playhead. AI clips
(mini cinematic gradient thumbnails) FLY in and SNAP onto lanes on the beat. Color wheels and a waveform lane
glide by. The timeline then zooms back and becomes a glowing montage wall of frames.

**Mood.** Editor flow-state. Precise, rhythmic, percussive — the most kinetic scene.

**Depth layers.** BG: faint lane ruler ticks, one glow. MG: timeline panel (full-width glass), 4 lanes,
12–14 clip blocks (sunset/ocean/neon gradient fills), playhead (vertical accent line) sweeping; secondary
floating panels: 3 color wheels (CSS conic rings — alpha-safe), an audio lane of small bars. FG: snap-flash
rectangles, beat tick marks that blink.

**Choreography.** Panel RISES (power3.out t≈0.5). Lanes EXTEND (scaleX staggered). Clips FLY in from right
and SNAP (x overshoot back.out(2), landing flash 0.12s) on a strict 0.75s beat grid t≈2.5–11. Playhead SWEEPS
continuously (linear, lane-length repeats). Color wheels SPIN slowly. At t≈15 the whole panel (wrapper) ZOOMS
OUT (scale 1→0.62, power2.inOut 2s) while a 4×3 montage wall of frame cards FADES UP behind, each card with
staggered glow; timeline panel settles bottom-center as one tile of the system.

**Transition out.** Root: blur-crossfade.

## Scene 06 — "Not just the tools, but the process" (36s)

**Concept.** A fog of meaningless "buzzword" blobs (amorphous glass pills WITHOUT text — smeared, unfocused)
clutters the frame. A clean storyboard interface WIPES it away like a squeegee. Then the real workflow
assembles itself in stages: moodboard thumbnails → shot cards → animation nodes → project folders →
timeline layers — each group filing into its own labeled-by-icon column. Theory replaced by practice.

**Mood.** Decluttering satisfaction — Marie Kondo for an AI pipeline. From noise to order.

**Depth layers.** BG: grid fading from blurry to crisp as scene progresses, two glows. MG: ~10 fog pills
(blurred 8–14px, fg 12–20%) drifting aimlessly; then a 5-column board (glass columns with header icons),
populated by: 4 mini moodboard cards, 4 shot cards (16:9 minis with corner tick), 3 node chips with cable
stubs, 3 folder shapes, 3 layer bars. FG: a vertical "squeegee" light bar that performs the wipe, column
underline draws, sea-spray dots.

**Choreography.** Fog pills WANDER (slow drifting fromTo tweens, blur, 0–8s). At t≈8 the light bar SWEEPS
left→right (power3.inOut 1.6s); pills it passes get WIPED (clip-path or opacity+x exit synced to bar position
— allowed here because it's mid-scene choreography, not a scene exit). Board columns RISE behind the bar
staggered. From t≈12: each column POPULATES in its own rhythm and style — moodboard cards FLIP in (rotationY),
shot cards DEAL (x slide), nodes CLICK (scale snap), folders STACK (y drop), layer bars EXTEND (scaleX).
t≈26–34: one green pulse THREADS through all five columns connecting them; columns BREATHE.

**Transition out.** Root: soft glitch into s07.

## Scene 07 — "Why did I make Endless Summers?" (25s)

**Concept.** A nightmare client revision board: dozens of tiny unreadable note bubbles, criss-crossing arrows,
red-ish markers, overlapping pins — visual claustrophobia. It GLITCHES, destabilizes, and DISSOLVES downward
like static draining away. Beneath it: a vast empty personal canvas with ONE glowing world-building node —
a sun-and-wave icon. Space. Silence. Ownership.

**Mood.** From inbox panic to first-day-of-summer freedom. The emotional pivot of the video.

**Depth layers.** Chaos phase — BG: dim grid; MG: ~22 note bubbles (glyph-bar filled, varied sizes, slightly
rotated), 8 arrow connectors, 5 sunset-rose alert dots pulsing anxiously; FG: jitter flickers. Calm phase —
BG: huge slow-breathing green glow + warm horizon hint at bottom; MG: one glass node (180px) center with
sun/wave geometric icon, 3 faint orbit rings; FG: 4 spawning cable stubs hinting future growth.

**Choreography.** Bubbles PILE ON in accelerating stagger (0.25s→0.08s intervals, t≈0.5–6) until the frame
feels overfull; arrows SCRIBBLE between them (scaleX draws at angles); alert dots PULSE fast (anxiety tempo
0.4s). t≈8–10: full-board GLITCH (x-jitter steps + slice-y clip flickers on a wrapper), then the chaos layer
DRAINS (y +60, opacity→0, masked stagger bottom-up) — mid-scene morph, allowed. t≈11: black beat (only glows).
t≈12: the personal node BLOOMS (scale 0→1 elastic.out(1,0.6) 1.2s), rings RIPPLE outward, orbit rings ROTATE
slowly, warm bleed RISES from bottom edge. Node heartbeat-PULSES till scene end; cable stubs GROW out at t≈20.

**Transition out.** Root: blur-crossfade.

## Scene 08 — "Personal projects are where you experiment" (37s)

**Concept.** A creator's laboratory: floating screens at varied depths hold experiments — weird generations,
broken frames (corrupt-glitch cards), rejected takes (dimmed with a slash line), interesting accidents.
They hover like specimens. The best four get PICKED (cursor selects each), glide forward, and line up into
a clean storyboard sequence strip. Failure as raw material.

**Mood.** Mad-scientist midnight energy with affection — every failure is lit like it matters.

**Depth layers.** BG: depth fog (two dim glows), faint lab grid, particle dust. MG: 9 floating screen cards
in 3 depth tiers (scale/blur-graded: far=small+blurred, near=large+crisp), mix of: cinematic gradient frames,
corrupted frames (RGB-split bars, displaced slices), over-noisy frames (heavy dotted overlay), a melted-gradient
failure. A storyboard strip dock (4 empty slots, glass) along the bottom, initially dim. FG: cursor, selection
ring, slot glow flashes, tiny status dots per card (green=keep, rose=reject) — dots only, no text.

**Choreography.** Cards FLOAT in from depth (z-feel: scale 0.7→1 + blur clear, staggered t≈0.6–5), then each
gets a personal idle DRIFT (different amplitude/period — parallax). Broken cards TWITCH occasionally (2-frame
x-glitch every ~4s, finite). t≈10: cursor GLIDES card to card; rejected ones DIM + slash line DRAWS (power1.in);
keepers get a selection ring that LOCKS (scale-in, accent flash). t≈18–30: the four keepers DETACH and GLIDE
(power2.inOut, 1.2s each) into dock slots; each slot FLARES on arrival; remaining cards RECEDE into depth
(scale down, blur up, dim — mid-scene, allowed). t≈30–36: dock strip LEVELS UP — slots connect with a drawn
underline, sequence pulses left→right like a film strip coming alive.

**Transition out.** Root: scanline wipe.

## Scene 09 — "Planning doesn't kill creativity" (39s)

**Concept.** A camera path drawn as a jittery scribble jumps chaotically between location markers scattered
on a dark map plane — run-and-gun chaos. The chaos FREEZES mid-jump. A storyboard grid slides in and the
markers REORGANIZE into a deliberate visual route; a glowing path CONNECTS each shot card like a GPS itinerary.
Same ingredients, opposite energy: intention.

**Mood.** From caffeine jitter to architect's drafting table. The longest exhale in the video.

**Depth layers.** BG: topographic-ish contour lines (2–3 SVG curves, accent-deep 12%) drifting, one glow.
MG: 7 location pins (teardrop shapes) scattered; a chaos path (SVG polyline, sharp angles) that draws and
redraws erratically; then a 3×2 storyboard grid of shot cards (cinematic gradients, corner ticks) and a smooth
bezier route with a traveling pulse dot. FG: freeze-frame flash, grid frame lines, route waypoint rings.

**Choreography.** Pins DROP (bounce, staggered t≈0.6–3). Chaos path SCRIBBLES pin-to-pin (fast dashoffset
draws 0.3s each with overshooting wiggle, t≈3–12) while a small camera dot DARTS along it (steps-like jerky
tweens); pins FLASH stressed-rose when visited. t≈13: FREEZE — everything stops, frame desaturates one beat
(dim overlay fades in 0.3s). t≈14.5: storyboard grid SLIDES in from right (power3.out), pins LIFT and FLY
each to its grid cell (1s each, overlapping, power2.inOut, t≈16–24), morph-flash into shot cards. t≈25–33:
smooth route DRAWS through the cards in order (3.5s, sine.inOut), waypoint rings RIPPLE as it passes; pulse
dot CRUISES the route (calm, constant). t≈33–38: grid wrapper slow push-in 3%; cards breathe.

**Transition out.** Root: warm light-leak crossfade into s10 (gold flash, 0.9s).

## Scene 10 — "I start with feelings" (34s)

**Concept.** A premium glass moodboard assembles itself from emotional artifacts: VHS-texture swatch,
film-strip fragment, sunset-sky card, beach-night card, headlight-streak card, soft silhouette card,
warm-grain swatch. Each floats in, finds its place, and threads connect them to a growing emotional color
palette column — feelings literally becoming a spec.

**Mood.** Scrapbook intimacy with Apple keynote polish. The warmest scene; green UI takes the back seat.

**Depth layers.** BG: warm radial bleed (sunset-orange 18%) + green glow balancing opposite corner, slow
particle drift. MG: glass board frame (rounded 24px, subtle) holding a 4×2 masonry of artifact cards — each
an abstract CSS rendering (VHS: scanline texture block; film strip: sprocket-holed dark strip with 3 gradient
cells; headlights: dark card with two gold glow streaks; silhouettes: dusk gradient with 2-3 soft dark figures
(simple rounded shapes); etc.). Right column: emotional palette — 5 swatch pills that FILL with colors sampled
from the cards. FG: connecting threads (1.5px lines) from cards to swatches, corner ticks, a slow cursor pass.

**Choreography.** Board frame BREATHES in (opacity+scale 0.97→1, 1.2s sine). Cards ARRIVE one per ~1.4s
(t≈1.5–12), each with its OWN entrance verb: VHS swatch SLIDES, film strip UNROLLS (scaleX from left),
sunset card BLOOMS (blur clear), night card FADES from dark, headlights STREAK in (x with motion-feel),
silhouettes DRIFT up, grain swatch SETTLES (tiny rotation). Each card lands with a soft glow ring. t≈14–24:
threads DRAW from each card to the palette column; swatch pills FILL (scaleX) with sunset-gold / orange /
rose / teal / deep-green in sequence; palette pulses softly. t≈25–33: whole board does a gentle parallax
tilt sweep (rotationY -2°→2° over 8s, sine.inOut), cards micro-float at different depths.

**Transition out.** Root: VHS tracking wipe into s11.

## Scene 11 — "Visual language / best summer that never happened" (31s)

**Concept.** A chunky VHS cassette (built from CSS shapes: shell, twin reels, label stripe WITHOUT text)
slides into a futuristic glass scanner slot. The tape de-materializes into light particles inside the scanner,
and MEMORIES pour out: cinematic frames fly up and outward — orange skies, shoreline waves, sunset drive,
boardwalk neon, night friends — each frame trailed by halation glow. A home movie from a timeline that never
existed.

**Mood.** The emotional climax. Spielberg-glow nostalgia processed through a clean machine.

**Depth layers.** BG: deep dusk glows (rose+gold low, green rim high), drifting particles. MG: the cassette
(≈420px wide) with rotating reels; the scanner — a glass arch/slot with an animated scan beam; 6 memory frame
cards (gradient recipes + heavy halation box-shadows) that erupt and settle into a loose constellation arc.
FG: light streams (thin glowing lines) from slot to frames, scan beam flicker, sprocket dots.

**Choreography.** Cassette ENTERS from left (power2.inOut 1.4s, t≈0.8), reels SPIN (rotation, finite repeats,
ease none). Scanner POWERS UP (glow ramp + beam sweep, t≈2.5). Cassette SLIDES into slot (t≈4–5.5), its body
DISSOLVES into ~20 particles that funnel into the slot (staggered curved tweens, t≈5.5–8). Beat of dark
(t≈8.5). Then frames ERUPT one per ~1.6s (t≈9–19): each LAUNCHES up-out from the slot (scale 0.3→1, y -300
varying, slight rotation, expo.out) and SETTLES into its arc position, then KEN BURNS on child layer + a
halation pulse. Light streams CONNECT slot→frames as each lands. t≈20–30: constellation BREATHES, slow camera
drift across it (wrapper x pan), warm bleed maxes at 25%.

**Transition out.** Root: blur-crossfade.

## Scene 12 — "Build one shot" — finale (26s)

**Concept.** The entire methodology in one continuous motion graphic, left to right: reference thumbnails
flow into a prompt card (glass card with glyph bars) → card CONDENSES into one cinematic still → still enters
an animation node (ring spins, still gains motion lines) → enhanced (sharpen flare, card grows crisper +
larger) → lands on a mini timeline at far right. Then the camera pulls back: every stage glows, cables join
them, and the whole pipeline pulses as ONE connected living system. Resolve to calm; end on the shoreline
motif and fade down.

**Mood.** Mastery and closure. The cold open's overwhelming waveform is now a tamed, humming machine.

**Depth layers.** BG: dot grid + dual glows + horizon line low in frame (the shoreline motif returns).
MG: 5 pipeline stations in a row (refs cluster / prompt card / still frame / anim node / enhance node) +
mini timeline; cables linking all. FG: traveling pulse, stage flare rings, particle dust.

**Choreography.** 3 reference thumbs DRIFT in and STACK (t≈0.5–3). They STREAM (shrink+fly) into the prompt
card which ASSEMBLES (glyph bars type-on via scaleX staggers, t≈3–6). Card FLASHES → still frame DEVELOPS
(blur 12→0 + brightness settle, t≈6.5–9). Still GLIDES into animation node ring (t≈10–12); ring SPINS UP,
motion streak lines SWEEP across the still (t≈12–15). Enhance stage: card SCALES UP 12% + crisp flare
(t≈15–17). Card DROPS onto mini timeline lane, SNAP flash (t≈17.5). t≈18–22: wrapper ZOOMS OUT (scale 1→0.8
power2.inOut 2.5s) revealing all stations; cables DRAW joining everything; one grand pulse RUNS the full
pipeline; every station FLARES in sequence. t≈22–26: FINAL RESOLVE — pipeline glow softens, the horizon line
brightens one last heartbeat, then ALL elements fade gently to the dark bg (the ONLY allowed exit fade,
power1.inOut 2s) ending on near-black with the faint horizon — ready for the editor's end card.

---

## Negative prompt (all scenes)

No text/letters/numbers/captions/scrambled glyphs. No brand or fake logos. No low-poly. No cyan/purple AI-slop
palette. No pure #000/#fff. No full-screen linear gradients on dark bg. No `transparent` keyword in gradients.
No static decoratives. No `repeat:-1`. No Math.random/Date.now. No exit animations before transitions
(except s12 finale and explicitly-allowed mid-scene morphs). No element overlap that isn't intentional depth.
