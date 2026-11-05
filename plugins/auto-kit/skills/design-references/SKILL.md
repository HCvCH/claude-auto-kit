---
name: design-references
description: Curated design references for web, 3D, poster and ad work — named style catalog, font pairings, component and animation libraries, 3D and prompt resources, and rules for ads and posters that don't look AI-generated. Use when proposing style directions, picking fonts, choosing a UI/animation library, or designing a poster, ad or social graphic.
---

# Design References

A reference shelf, not a style. Nothing here is applied by default: `project-pipeline` Phase 1 picks a direction, and only the entries that fit that direction are used.

## 1. Named style catalog

Use these names when proposing the three directions in Phase 1. Each line: what defines it, and where it fits.

| Style | Defining traits | Fits |
|---|---|---|
| Claymorphism | soft inflated 3D shapes, pastel, inner + outer shadow | playful apps, kids, onboarding |
| Cybercore | dense tech graphics, acid accents, HUD fragments | gaming, music, events |
| Neo-brutalism | thick black borders, flat bright fills, hard offset shadows | indie tools, portfolios |
| Scrapbook | paper textures, tape, cut-outs, handwriting | personal brands, food, travel |
| Surrealism | impossible scenes, dreamlike compositing | art, fashion, campaigns |
| Y2K | chrome, blobs, iridescence, early-2000s UI | fashion, music, nostalgia |
| Pixel art | hard pixel grid, limited palette, 8/16-bit type | games, retro products |
| Synthwave | neon magenta/cyan, sunset grids, chrome type | music, nightlife (not for tech defaults) |
| Glassmorphism | frosted translucent panels over colorful blur | dashboards, OS-like UI |
| Neumorphism | same-color extruded surfaces, soft dual shadows | small controls, sparingly (low contrast) |
| Bento grid | modular cards of different sizes, one idea per tile | product features, portfolios |
| Editorial | big serif headlines, columns, generous margins | magazines, cafés, studios |
| Swiss | strict grid, sans-serif, asymmetry, flush-left | agencies, architecture, data |
| Minimalism | few elements, lots of space, one accent | premium products |
| Maximalism | layered color, pattern and type, controlled chaos | fashion, culture, events |
| Luxury typography | high-contrast serif, wide tracking, black/cream/gold | hotels, jewelry, wine |
| Conceptual sketch | hand-drawn lines, unfinished feel, annotations | creative studios, workshops |
| Ethereal | light gradients, soft focus, airy type | wellness, beauty |
| Bohemian | earthy tones, organic shapes, textured paper | crafts, cafés, lifestyle |
| Victorian | ornaments, frames, engraving style, serif | heritage brands, barbers, bars |
| Cyberpunk | dark city, neon signage, glitch, katakana-style accents | games, tech fiction |
| Wabi-sabi | imperfect textures, muted naturals, asymmetry, calm | ceramics, tea, interiors |

## 2. Font pairings

Pair one display face with one workhorse. Check licenses before shipping; prefer free sources (Google Fonts, Fontshare).

| Display | Body | Mood |
|---|---|---|
| Tempting (script) | Switzer (Fontshare, free) | elegant + bold contrast; cafés, beauty, events |
| Fraunces | Inter Tight | warm editorial |
| Clash Display (Fontshare) | Satoshi (Fontshare) | modern product |
| Playfair Display | Source Sans 3 | classic editorial |
| Space Grotesk | IBM Plex Sans | technical, honest |

Script faces only for one or two words (a logo line, a headline accent), never for body text or buttons.

## 3. Libraries and resources

| Need | Resource | Note |
|---|---|---|
| Smooth scrolling | Lenis (`lenis` on npm) | pair with GSAP ScrollTrigger; skip on reduced-motion |
| Scroll and timeline animation | GSAP + ScrollTrigger | see `project-pipeline` Phase 4 |
| Ready animated components (React) | React Bits (reactbits.dev) | copy the component source into the project, then restyle to the picked direction |
| Ready components with AI generation | 21st.dev (Magic MCP if installed) | same rule: restyle, never ship the demo look |
| Charts | BKlit UI | free chart components |
| Embedded 3D scenes without code | Spline (spline.design) | export the scene and embed with `@splinetool/react-spline` or the viewer; keep the file small |
| Procedural 3D from a photo | `img2threejs` | Phase 7 |
| Interaction prompt ideas for 3D sites | Getlayers prompt library (getlayers) | use as inspiration for the interaction, not as copy-paste output |
| Real app screen references | Mobbin (free browsing; the MCP needs a paid key) | study patterns, don't clone screens |
| Open-source animated UI components (copy-paste, React + Tailwind) | Magic UI (magicui.design, MIT), Animate UI (animate-ui.com, MIT), Motion Primitives (motion-primitives.com, MIT), Aceternity UI (ui.aceternity.com, free components), shadcn/ui (ui.shadcn.com, MIT) | pick ONE library per project; copy only the components the design needs and restyle them to the picked direction |
| Reference image → code | `image-to-code` skill | build a section from a generated or provided reference image |

Every JS animation library adds weight: budget roughly 150 KB of JS for animation in total and check typography and spacing first — motion doesn't fix a weak layout.

## 4. Posters, ads and social graphics

What separates a good ad from AI slop:

1. **Real product, real photo.** One sharp product shot or a clean render. No collage of generated food, flying beans or fake splashes.
2. **One message.** A headline of up to six words, one supporting line, one call to action. Delete stickers, badges and "40% OFF" bursts unless the brief demands one.
3. **Space.** At least a third of the canvas empty. Align everything to one grid; equal margins on all sides.
4. **Two typefaces at most**, one of them neutral. Type size jumps are big and deliberate.
5. **Limited palette.** Brand color + one neutral + one accent. No rainbow gradients.
6. **Campaign system.** For a series (e.g. six posters for one café), keep grid, type, logo position and photo treatment identical; vary only product, headline and one color.
7. **Check at thumbnail size.** If the message isn't readable at 200 px wide, simplify.

Run `hallmark audit` on web pages and these seven rules on every static graphic.

---
Written for this repo from saved design references; no third-party text copied.
License: CC-BY-NC-SA-4.0 — © HCvCH, https://github.com/HCvCH/claude-auto-kit (see NOTICE.md)
