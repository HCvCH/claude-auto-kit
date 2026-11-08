---
name: sound-effects
description: Find, choose and place sound effects for code-rendered or edited videos — search free openly licensed SFX through the Openverse API, pick by length and licence, keep an attribution list, and lay hits on exact frames with ffmpeg. Use when a Remotion/HyperFrames render or an edit needs whooshes, clicks, pops, impacts or ambience, or when generic or badly timed SFX should be fixed.
---

# Sound Effects

Generic SFX in the wrong place make a good edit feel cheap. This skill covers three things: where the sounds come from, which one fits, and where exactly it lands. Mechanical mixing goes through `ffmpeg-media`; format and pacing decisions stay in `video-pipeline`.

## 1. Source order

Use the first source that has a fitting sound:

1. **Local SFX folder** the user named (ask once for the path, then reuse it).
2. **Installed SFX tools**, if present: `earshot` (MCP/CLI — can listen to the render, audition candidates and render code-based effects) or the `real-sfx` skill (recorded UI sounds placed on frames). Check `/mcp` and the skill list; never install them yourself.
3. **Openverse API** — millions of openly licensed audio clips, no key needed for normal searches.
4. **Generate** only when nothing above fits (synth in code, or a generator the user has).

Never use sounds ripped from films, games, TV or other creators' videos.

## 2. Openverse search

Endpoint: `GET https://api.openverse.org/v1/audio/`

| Param | Use |
|---|---|
| `q` | what it sounds like: `whoosh`, `ui click`, `paper slide`, `bass hit` |
| `category` | `sound_effect` (others: music, podcast, audiobook, news, pronunciation) |
| `length` | `shortest` or `short` for hits; `medium`/`long` for ambience |
| `license` | `cc0` first; `by` only if attribution goes into the description |
| `license_type` | `commercial` when the video is monetized |
| `extension` | `wav` or `mp3` |
| `page_size` | 10–20 is enough to choose from |

Example: `https://api.openverse.org/v1/audio/?q=whoosh&category=sound_effect&length=shortest&license=cc0&page_size=15`

From each result keep `title`, `creator`, `url` (file), `foreign_landing_url`, `license`, `license_version`, `license_url` and `attribution`. Download into `./sfx/` with a short descriptive name (`whoosh-01.wav`). Write every non-CC0 sound's `attribution` line into `./sfx/CREDITS.md` and remind the user to paste it into the video description.

Anonymous requests are rate-limited: batch the searches for one video, don't loop per frame.

## 3. Choosing

- Short and dry beats long and reverby for UI and motion graphics; trim silence at the start so the transient sits on the frame.
- One sound family per video (same click, same whoosh) — variety reads as noise.
- Match energy: soft pop for a fade-in, sharp tick for a counter, low thump for a big reveal.
- Less is more: a sound on every cut gets tiring. Mark the 5–10 moments that matter (scene change, key number, logo, punchline) and leave the rest silent.

## 4. Placing on exact frames

1. List the moments from the storyboard or the Remotion/HyperFrames composition as frame numbers. Convert with `seconds = frame / fps`.
2. Offset whooshes so their peak lands on the cut (start ~0.1–0.3 s before it); clicks and hits start on the frame.
3. Build the SFX track with ffmpeg (`adelay` per sound in milliseconds, then `amix`), keep it 6–12 dB under the voice, and duck music under hits if needed — exact commands in `ffmpeg-media`.
4. Export the SFX stem as its own WAV as well as the mixed MP4, so levels can be fixed later without redoing the timing.
5. Give the user a short list of the 3–5 placements to check by ear (timestamp + what plays).

In Remotion, sounds can also be placed directly with `<Audio>` inside a `<Sequence from={frame}>` — use that when the video is rendered there anyway.

## 5. Checklist before render

- [ ] Every sound is CC0, CC BY with credit in `CREDITS.md`, from the user's own folder, or generated
- [ ] Peaks land on the intended frames
- [ ] Voice stays clearly on top; no clipping (true peak ≤ −1 dBTP)
- [ ] SFX stem exported separately

---
Written for this repo; no third-party text copied. Openverse is a WordPress project (https://openverse.org); each audio file keeps its own licence.
License: CC-BY-NC-SA-4.0 — © HCvCH, https://github.com/HCvCH/claude-auto-kit (see NOTICE.md)
