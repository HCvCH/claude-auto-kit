---
name: motion-styles
description: Catalog of code-rendered motion graphic looks — glass mosaic, pixel explainer, paper-cut, CGI product, watercolour, retro terminal/HUD, Galton board and other physics, isometric worlds, 3D data charts, map routes, 3D teardowns, split-flap, git-commit graphs, holograms, synthwave, atom models and more — each with look rules, motion rules and the render tech that gets it right. Use when picking or executing the visual style of a Claude-made video, explainer or animated hero, so the result looks designed instead of default.
---

# Motion Styles

Default Claude animation is flat shapes sliding in with ease-out. Pro results come from committing to one style and following its rules for palette, texture, motion and tech. Use this catalog when `video-pipeline` has picked the format and the user picks the look (offer three fitting styles, like the Phase 1 directions in `project-pipeline`). Timing and storyboard still come from the motion graphics skill; motion code quality from `animate` and `animation-performance`.

## How to use a style

1. Pick **one** style per video. Mixing two looks reads as a template collage.
2. Write a 5-line style sheet before any code: palette (3–5 hex), texture, type, camera, motion rule.
3. Use the listed tech. A style faked in the wrong tech (3D in CSS, physics by hand-keyed frames) is the main reason results look cheap.
4. Render a 3-second test of the hardest shot first and check it at full size before building the rest.

## Catalog

| Style | Look | Motion | Tech |
|---|---|---|---|
| Glass mosaic | Frosted tiles, soft refraction, bright edges on dark ground | Tiles assemble or ripple into the image, light sweeps across | Three.js with transmission material, or Canvas with blurred tile layers |
| Aurora / glassmorphism | Blurred colour blobs behind frosted cards | Slow drifting gradients, cards float in with depth | CSS/Canvas, `backdrop-filter` only in browser renders |
| Pixel explainer | Low-res grid (e.g. 320x180 scaled up), limited palette, pixel font | Stepped motion at 8–12 fps, no sub-pixel easing | Canvas with `imageSmoothingEnabled = false`, integer positions |
| Paper-cut | Layered paper with drop shadows, visible fibre texture, warm light | Layers slide on parallax planes, slight wobble, stop-motion feel | DOM/Canvas layers with real shadow offsets, or Three.js planes; paper texture image |
| Collage / cut-out | Photo scraps, torn edges, tape, halftone | Jumpy, 12 fps placement, pieces slap in | Canvas/DOM with masks; CC0 photos only |
| Watercolour | Soft bleeding edges, paper grain, granulation | Washes spread outward, ink lines draw on | Canvas/p5.js with noise-displaced shapes and multiply blending |
| Line art / line boil | Single-weight lines on plain ground | Lines draw on (stroke-dashoffset); hand-drawn jitter re-randomised every 2–3 frames | SVG paths |
| Flat vector | Bold flat shapes, 3–4 colours, no gradients | Squash-and-stretch, overshoot, snappy timing | SVG or Lottie-style shapes in Remotion |
| Shape morph | One shape that becomes every next object | Continuous morphs, never a hard cut | SVG path interpolation (same point count) |
| Sticker explainer | Objects as die-cut stickers with white border and shadow | Peel-on, pop and wiggle | SVG/DOM with stroke outline |
| CGI product | Studio-lit hero object, soft reflections, gradient backdrop | Slow orbit or turntable, light sweeps, exploded parts | Three.js / React Three Fiber, HDRI lighting, PBR materials |
| 3D teardown | Object splits into labelled layers | Parts lift apart on one axis, callout lines draw to labels | Three.js with grouped meshes; `img2threejs` for a model from a photo |
| Isometric world / flow | 30° isometric miniature, soft shadows, tilt-shift | Pieces build up from the ground, packets travel along paths | Three.js orthographic camera, or SVG isometric grid |
| 3D data chart | Bars or stacks as real objects (e.g. cash stacks) | Bars grow from the floor in sequence, camera dolly, numbers count up | Three.js with instanced meshes; data from JSON |
| Data story (2D) | Clean chart, one highlight colour | One chart per scene, counted numbers | Remotion + SVG; no 3D unless the style is 3D data chart |
| Map route | Muted base map, bright route line, pins | Line draws along the route, camera follows, landmarks pop up | MapLibre/Natural Earth data or SVG map; route as GeoJSON |
| Split-flap | Airport board, mechanical flaps, mono font | Characters flip through letters before settling, staggered | DOM/CSS 3D flaps or Canvas; click SFX per flip |
| Git commit graph | Branch lines and commit dots, terminal colours | Commits appear in order, branches split and merge | SVG with data from `git log --graph` style JSON |
| Retro terminal / HUD | Dark ground, phosphor green or cyan, scanlines, glow | Typing text, blinking cursor, scanning brackets lock on | Canvas/SVG with glow filter; monospace font |
| Hologram | Cyan wireframe, scanlines, flicker, additive blending | Rotating wireframe, glitch flickers, data rings | Three.js wireframe + additive blending + bloom |
| Synthwave / VHS | Neon grid floor, sunset gradient, chromatic aberration, VHS noise | Grid scrolls toward camera, logo chrome shine | Three.js or Canvas; noise overlay |
| Bauhaus geometric | Primary colours, circles/squares/triangles, grid | Shapes slide and rotate on beats | SVG, timing from a beat list |
| Liquid motion | Blobby metaballs, glossy highlights | Drops merge and split, wobble | Canvas metaballs or SVG goo filter |
| Physics: Galton board / dominoes | Clean objects, visible physics | Real simulation: balls bounce into a bell curve, dominoes fall in chains | matter.js (2D) or a 3D physics engine; record frames deterministically with a fixed seed |
| Atom / science model | Glowing nucleus, orbit rings, particle trails | Electrons orbit, energy levels pulse, interactive hover in web version | Three.js with bloom; particles as instanced points |
| Variety captions (9:16) | Big bold words, emoji, colour per speaker | Word-by-word pop synced to voice | Remotion captions; `ffmpeg-media` for burn-in |

## Quality rules for every style

- Texture carries the style: paper grain, pixel grid, scanlines, film noise. Without it most styles fall back to "default vector".
- Real light for 3D: HDRI or three-point lighting, soft shadows; never flat ambient only.
- Physics and particle styles must be simulated, not keyed by hand, and seeded so the render is repeatable.
- Respect the frame: 9:16 safe areas for captions, nothing important in the bottom 15 %.
- Sound: pair the style with matching SFX (`sound-effects`): clicks for split-flap, paper rustle for paper-cut, synth hits for synthwave.

## Open references

For ready prompts and full demo films of many of these looks: https://github.com/Vincentwei1021/mg-styles-15 (15 styles, MIT) and https://github.com/lemomo-ai/lemo-opuscar. Read and adapt; do not run their code without the user's go.

---
Written for this repo; no third-party text copied. Style names are generic design terms.
License: CC-BY-NC-SA-4.0 — © HCvCH, https://github.com/HCvCH/claude-auto-kit (see NOTICE.md)
