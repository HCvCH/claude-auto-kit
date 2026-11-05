---
name: ffmpeg-media
description: Local audio and video processing with ffmpeg — cut, trim, concatenate, reframe to 9:16, burn captions, extract or replace audio, normalize loudness, remove silence, compress, make GIFs and thumbnails. Use when a video or audio file has to be edited or converted, or when a Remotion/HyperFrames render needs post-processing.
---

# ffmpeg Media

ffmpeg does the mechanical work; creative decisions stay in `video-pipeline` and Phase 8 of `project-pipeline`.

## Before running anything

1. Check that ffmpeg exists: `ffmpeg -version`. If it's missing, say so and give the install command for the user's OS (Windows: `winget install --id Gyan.FFmpeg -e`). Don't install it yourself.
2. Inspect the input first: `ffprobe -v error -show_entries format=duration:stream=codec_name,width,height,r_frame_rate -of compact INPUT`.
3. Never overwrite the input. Write to `./out/` with a descriptive name.
4. On Windows PowerShell, quote paths with spaces in double quotes and use `^`-free single-line commands.

## Recipes

| Task | Command |
|---|---|
| Trim without re-encoding (fast, cuts on keyframes) | `ffmpeg -ss 00:00:05 -to 00:00:20 -i in.mp4 -c copy out/trim.mp4` |
| Trim frame-accurate | `ffmpeg -ss 00:00:05 -to 00:00:20 -i in.mp4 -c:v libx264 -crf 18 -c:a aac out/trim.mp4` |
| Concatenate same-codec clips | write `list.txt` with `file 'a.mp4'` lines, then `ffmpeg -f concat -safe 0 -i list.txt -c copy out/joined.mp4` |
| Reframe 16:9 → 9:16 (center crop) | `ffmpeg -i in.mp4 -vf "crop=ih*9/16:ih,scale=1080:1920" -c:a copy out/vertical.mp4` |
| 9:16 with blurred background (no crop) | `ffmpeg -i in.mp4 -filter_complex "[0:v]scale=1080:1920:force_original_aspect_ratio=increase,crop=1080:1920,boxblur=20[bg];[0:v]scale=1080:-2[fg];[bg][fg]overlay=(W-w)/2:(H-h)/2" -c:a copy out/vertical-blur.mp4` |
| Burn subtitles | `ffmpeg -i in.mp4 -vf "subtitles=captions.srt:force_style='Fontsize=16,Outline=2'" out/captioned.mp4` |
| Extract audio | `ffmpeg -i in.mp4 -vn -c:a libmp3lame -q:a 2 out/audio.mp3` |
| Replace audio | `ffmpeg -i video.mp4 -i voice.wav -map 0:v -map 1:a -c:v copy -shortest out/voiced.mp4` |
| Mix music under voice (ducked) | `ffmpeg -i voice.wav -i music.mp3 -filter_complex "[1:a]volume=0.15[m];[0:a][m]amix=inputs=2:duration=first" out/mix.wav` |
| Loudness for social (−14 LUFS) | `ffmpeg -i in.mp4 -af loudnorm=I=-14:TP=-1.5:LRA=11 -c:v copy out/loud.mp4` |
| Remove silence (talking head) | `ffmpeg -i in.wav -af silenceremove=stop_periods=-1:stop_duration=0.4:stop_threshold=-40dB out/tight.wav` — for video, detect with `silencedetect` and cut the ranges instead |
| Compress for upload | `ffmpeg -i in.mp4 -c:v libx264 -crf 23 -preset slow -c:a aac -b:a 128k -movflags +faststart out/small.mp4` |
| Thumbnail at a timestamp | `ffmpeg -ss 00:00:03 -i in.mp4 -frames:v 1 out/thumb.jpg` |
| Contact sheet of stills | `ffmpeg -i in.mp4 -vf "fps=1/2,scale=270:-1,tile=5x2" -frames:v 1 out/sheet.jpg` |
| GIF (good palette) | `ffmpeg -i in.mp4 -vf "fps=12,scale=480:-1:flags=lanczos,split[a][b];[a]palettegen[p];[b][p]paletteuse" out/clip.gif` |

## Rules

- Prefer `-c copy` when no filter is needed; re-encode only when the task requires it.
- After every command, run `ffprobe` on the output and report duration, resolution and size.
- For word-level captions, transcribe first (e.g. Whisper if installed) and generate the `.srt`; never guess timings.
- Only use audio the user owns, generated audio, or royalty-free audio.

---
Written for this repo; no third-party text copied.
License: CC-BY-NC-SA-4.0 — © HCvCH, https://github.com/HCvCH/claude-auto-kit (see NOTICE.md)
