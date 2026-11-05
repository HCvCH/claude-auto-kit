---
name: workflow-stacks
description: Ready-made tool stacks and automation ideas with free replacements for paid parts — content system for short videos, an "AI team" of 42 add-ons, 10 Claude systems, and free open-source alternatives to paid software. Use when the user asks how to automate content, build a system or workflow, or replace a paid tool.
---

# Workflow Stacks

Always prefer the free option. Name the cost of every paid part before suggesting it.

## 1. Content system (short-form video)

| Job | Tool | Cost | Free replacement |
|---|---|---|---|
| Orchestrates everything | Claude Code | existing plan | — |
| Animation | Remotion, HyperFrames | free | — |
| "Watch" footage, edit | video-use (browser-use) | free (uses ElevenLabs for transcripts) | Whisper local transcripts |
| "Hear" audio | Whisper | free | — |
| Edit by JSON | Editly | free | ffmpeg (`ffmpeg-media`) |
| Captions on phone | IG Edits app | free | Whisper + burned-in captions |
| B-roll / footage | Higgsfield | paid | ComfyUI + Flux schnell locally, Pexels/Pixabay free stock |
| Research transcripts | Apify | free credits | yt-dlp + Whisper |
| Download references | yt-dlp | free | — |
| Landing pages | Claude Design / `project-pipeline` | free | — |
| Content calendar | Notion | free | Todoist (already used) |
| Email / lead list | Resend | free tier | — |

Flow: idea → research (yt-dlp/Apify) → script → `video-pipeline` → render → captions → post → log in calendar.

## 2. "AI team" map (42 add-ons, by department)

- **Build & test:** superpowers, gstack, graphify, GitHub CLI, Vercel, Playwright, Codex, Claude HUD
- **Design & animate:** Figma, ui-ux-pro-max, impeccable, taste-skill, HyperFrames, Remotion, ffmpeg, Higgsfield (paid → ComfyUI)
- **Research & sell:** Perplexity (paid API), Claude in Chrome, Firecrawl, Apify, Gemini, humanizer, Metricool (paid)
- **Make the posts:** GPT Image / Nano Banana (paid APIs → ComfyUI), ElevenLabs (free tier), Puppeteer (→ Playwright), Google Drive, Granola, Whisper, Python
- **Run the office:** Notion, Gmail, Google Calendar, Slack, Zapier, caveman, find-skills, Node.js, Ollama

## 3. Ten Claude systems — what they need and the free version

| System | Original setup | Paid parts | Free version |
|---|---|---|---|
| WhatsApp agent (replies, bookings) | GoHighLevel + WhatsApp | GoHighLevel, WhatsApp Business API fees | WhatsApp Business app auto-replies; self-hosted gateways are unofficial and risk bans |
| Listing video maker | Higgsfield + master prompt | Higgsfield | `video-pipeline` "Photo tour" format in Remotion |
| Excel dashboard | Google Sheets connector | — | CSV/Sheets → HTML dashboard built by Claude |
| AI voice agent (calls) | receptionist skill + Fish Audio | Fish Audio, phone number/telephony | none fully free (calls always cost) |
| Website from Maps link | Claude Code + Netlify | — | `maps-to-website` + Netlify/Vercel free tier |
| Carousel machine | carousel skill + Blotato | Blotato | Claude renders slides (HTML → PNG with Playwright), post manually; ideas from topcarousels.com free plan |
| Facebook ads engine | Ads Library + Higgsfield | Higgsfield | Ads Library (free) + ComfyUI for visuals |
| Personal assistant / morning brief | Gmail + Calendar + skills | — | calendar + task connectors + a scheduled morning brief |
| AI second brain | Claude Code + Obsidian | — | Obsidian vault (free) or mymind |
| Cold email machine | Cowork + Instantly + 5 inboxes | Instantly, inboxes | not recommended in Germany: unsolicited B2B emails need prior consent (UWG §7) |

## 4. Free open-source alternatives to paid tools

| Paid | Free alternative |
|---|---|
| Higgsfield (AI image/video studio) | Open Higgsfield |
| ElevenLabs (voice cloning) | VoiceStudio (local) |
| Semrush | OpenSEO |
| Notion | AppFlowy |
| Wispr Flow (dictation) | OpenWhispr |
| Asana | OpenProject |
| Calendly | Cal.diy |
| Intercom | Chatwoot |
| Loom | Cap |

Look up the current repository and license before installing any of them.

---
Written for this repo from saved workflow references; no third-party text copied.
License: CC-BY-NC-SA-4.0 — © HCvCH, https://github.com/HCvCH/claude-auto-kit (see NOTICE.md)
