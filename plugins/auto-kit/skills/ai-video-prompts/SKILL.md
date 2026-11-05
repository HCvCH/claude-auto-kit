---
name: ai-video-prompts
description: Writes prompts for AI video generators (Seedance, Veo, Kling, Runway, Sora-style tools) in seven formats — motion graphics, claymation, explainer, singing story, commercial, 3D animation, cartoon. Use when the user wants a prompt or a shot list for a text-to-video or image-to-video model instead of a code-rendered video.
---

# AI Video Prompts

For code-rendered video (Remotion, HyperFrames) use `video-pipeline`. This skill is for generator models that take a text prompt.

## 1. Ask for three things (only if missing)

- Target model (prompt length and syntax differ; default: a generic prompt of 60–120 words).
- Length and aspect ratio (default 8 s clips, 9:16).
- Subject and the one feeling the clip must leave.

## 2. Prompt structure (every format)

Write the prompt in this order, one sentence each:

1. **Shot:** framing and lens (close-up, wide, 35 mm, macro, top-down).
2. **Subject:** who/what, with 2–3 concrete visual details.
3. **Action:** one clear action per clip, with a verb that moves.
4. **Setting:** place, time of day, weather.
5. **Style:** the format block below.
6. **Camera:** one camera move (slow push-in, orbit, handheld follow, static).
7. **Light and color:** key light direction, palette of 2–3 colors.
8. **Audio cue** (only for models with sound): ambience, one sound effect, music mood.

End with a short negative line where the model supports it: `no text, no watermark, no extra limbs, no flicker`.

For multi-clip videos, write a shot list first (clip number, seconds, prompt), and repeat the same character and style description word for word in every clip so the model stays consistent.

## 3. Format blocks

| Format | Style block to insert |
|---|---|
| Motion graphics | flat 2D vector shapes, bold geometric forms, smooth eased transitions, limited palette of 3 colors, clean background, kinetic shapes morphing into each other |
| Claymation | handmade plasticine characters, visible fingerprints and texture, stop-motion at 12 fps, miniature set, soft studio lighting, slight imperfections |
| Explainer | clear diagram-like visuals, one object explained per shot, simple isometric or flat illustration, labels avoided, calm pacing |
| Singing story | character performing to camera, lip movement in rhythm, expressive face, storybook background that changes with each verse, warm stage lighting |
| Commercial | hero product centered, premium studio lighting, slow dolly, shallow depth of field, reflections and texture detail, end on a clean product shot with empty space for a logo |
| 3D animation | stylized 3D characters, Pixar-like proportions, soft global illumination, rounded shapes, cinematic depth of field |
| Cartoon | 2D hand-drawn cartoon, thick outlines, squash and stretch, bright flat colors, exaggerated expressions, simple painted backgrounds |

## 4. Rules

- No real people, celebrities, brands or third-party characters (e.g. Pokémon, Disney) unless the user owns the rights.
- One action per clip; split anything longer into more clips.
- Give the user the finished prompts in a code block per clip, ready to paste.

---
Written for this repo; no third-party text copied.
License: CC-BY-NC-SA-4.0 — © HCvCH, https://github.com/HCvCH/claude-auto-kit (see NOTICE.md)
