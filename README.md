# claude-auto-kit

I saved Instagram reels about Claude skills to mymind and never installed any of them. Now a weekly Claude task reads that mymind space, finds the tool or skill behind each post and adds the useful ones to this plugin. Claude Code pulls the update on its own.

Fork it and your copy fills up with your own finds. Installing my copy gives you my picks, which change every week. Claude Code wrote most of the files; I decide what goes in and use it on my own projects.

![How it works: save posts to mymind, a weekly Claude task sorts them, useful skills land in the plugin](docs/flow.svg)

## What you need

- [Claude Code](https://code.claude.com) with the `claude` CLI, and [git](https://git-scm.com) (Claude Code fetches the plugin with it)
- A [mymind](https://mymind.com) account (the free plan caps you at 100 cards at the time of writing, paid plans don't; see [pricing](https://mymind.com/pricing))
- A Claude plan with scheduled tasks and the mymind connector (Settings → Connectors)
- A GitHub account; Claude needs push access to your copy

## Setup

1. **Copy the repo.** On GitHub: **Use this template → Create a new repository**, or **Fork**. If your copy is private, sign in to GitHub with git on your PC.
2. **Credit the original.** Keep [`NOTICE.md`](NOTICE.md) and put its credit line at the top of your README.
3. **Set your username** in two files. Don't add a `version` field, or auto-update stops working.
   - [`.claude-plugin/marketplace.json`](.claude-plugin/marketplace.json) → `owner.name`
   - [`plugins/auto-kit/.claude-plugin/plugin.json`](plugins/auto-kit/.claude-plugin/plugin.json) → `author.name`, `repository`
4. **Trim the skills (optional).** Your copy starts with [the skills in this repo](#skills-in-this-copy). Delete folders under `plugins/auto-kit/skills/` you don't want and remove their rows from `project-pipeline`. Keep `project-pipeline` itself; if you delete everything else, the weekly check refills it from your own finds.
5. **Install your copy:**

   ```powershell
   claude plugin marketplace add <your-username>/<your-repo>
   claude plugin install auto-kit@auto-kit
   ```

6. **Turn on auto-update** so new skills arrive by themselves. Add to `~/.claude/settings.json` (Windows: `C:\Users\<you>\.claude\settings.json`):

   ```json
   "extraKnownMarketplaces": {
     "auto-kit": {
       "source": { "source": "github", "repo": "<your-username>/<your-repo>" },
       "autoUpdate": true
     }
   }
   ```

7. **Load the pipeline in every project.** Add to your `CLAUDE.md`:

   ```text
   For every new project (website, web app, dashboard, 3D scene, motion video), start by loading the auto-kit:project-pipeline skill and follow its phases.
   ```

8. **Create a mymind space** (e.g. "AI") and share reels, posts and screenshots into it.
9. **Schedule the weekly check.** Fill in the placeholders in [`docs/weekly-check-prompt.md`](docs/weekly-check-prompt.md) (your repo, your space, the plugins and skills you already have) and schedule it in Claude. If a scheduled session can't push to your repo, run it as a weekly reminder in a chat with the repo attached. The prompt books its own next run.

## How the weekly check works

1. mymind stores each link you share and writes an AI summary of it.
2. Claude reads every item in the space without the `claude-checked` tag. It uses that summary, tags, screenshots, web search and GitHub. It never scrapes Instagram or TikTok.
3. It sorts each find:
   - **Skill with an open license** (MIT, Apache-2.0 …) → copied into `plugins/auto-kit/skills/`, Markdown only
   - **Checklist or prompt** → rewritten as a skill in its own words
   - **Plugin, MCP server, CLI tool, connector** → install command in the report. These run code on your machine, so Claude never adds them itself
4. Each new skill gets a row in the "Skill bundles" table of [`project-pipeline`](plugins/auto-kit/skills/project-pipeline/SKILL.md) (phase, project types, mode: always / choose / if) and a sentence in the text of its phase.
5. Claude validates the plugin, commits, tags the mymind items and sends you a report: what it added, what it skipped and why, what's left for you.

### Tags

Each checked item gets `claude-checked`, one status tag and one or more topic tags.

| Status | Meaning | Next |
|---|---|---|
| `claude-installed` | Every tool, skill or checklist in the item is in the repo or in your installed plugins. One missing or unclear part and the item doesn't get this tag | Listed for deletion. Reply "delete" and Claude moves them to mymind's trash (30 days) |
| `claude-todo` | You need to install a plugin, MCP server, CLI tool or connector | Listed every week until you report it installed, then it becomes `claude-installed` |
| `claude-unclear` | Claude couldn't tell which tool the post means | Listed every week until you say |
| `claude-keep` | Nothing to install (know-how, inspiration, non-Claude tools) | Stays, no reminders |

Topics: `knowledge` (general AI know-how), `design`, `video`, `security`, `coding`, `ai-tool` (non-Claude AI service), `offtopic`.

## What `project-pipeline` does

- Sorts the project into WEB, 3D, VIDEO or CODE and loads only the skills for that type: a website gets web skills, no 3D or video skills
- Runs quality, test and process skills every time
- Offers three distinct style directions and lets you pick, checking sibling projects so it doesn't repeat itself. Look-defining skills (layout catalogs, themes, brand styles) never run by default, so your sites don't all look the same
- Phases: classify → style → design system → build → motion → test → polish, plus 3D-asset and video phases
- Tells you when a skill is missing and carries on

## Safety and limits

- No hooks, MCP servers, `bin/` files or scripts land in the repo. You decide what code runs on your machine.
- Claude checks each candidate's maintainer, activity, license and instructions (data leaks, ignored rules, code run without asking). Offensive security tools are left out.
- The weekly task runs nothing from third-party repos.
- Skills without a license that allows copying stay out; you get the install command.
- If neither the post nor mymind's summary names the tool, the item gets `claude-unclear` and the report asks you.
- Some skills only run when you call them, e.g. `/auto-kit:review-animations`.

## License

Created by **HCvCH**. Everything written for this repo: [CC BY-NC-SA 4.0](LICENSE), copy and adapt it for non-commercial use with credit, share changes under the same license. No commercial use. Copied skills keep their own licenses ([THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)). [NOTICE.md](NOTICE.md) says which part falls under which.

## Skills in this copy

My own copy, as an example. Yours will grow in its own direction.

<details>
<summary>26 skills</summary>

**Written for this repo**

| Skill | For |
|---|---|
| `project-pipeline` | The orchestrator above |
| `video-pipeline` | Picks the video format and the skills to build it |
| `web-security-checklist` | Pre-launch security review for AI-built web apps |
| `claude-md-audit` | Audits and slims down CLAUDE.md files (run it yourself) |
| `design-references` | Style catalog, font pairings, libraries, poster and ad rules |
| `image-to-code` | Builds sections from reference images |
| `maps-to-website` | Local-business website from a Maps link |
| `ffmpeg-media` | ffmpeg recipes for cutting, reframing, captions and audio |
| `ai-video-prompts` | Prompts for AI video generators in seven formats |
| `workflow-stacks` | Tool stacks and free replacements for paid tools |
| `claude-code-resources` | Map of Claude Code repos, guides and packs |

**Copied with license**

| Skill | For | Source |
|---|---|---|
| `hallmark` | Page structure, themes and audits against generic AI layouts | [nutlope/hallmark](https://github.com/nutlope/hallmark) |
| `humanizer` | Removes AI writing patterns | [blader/humanizer](https://github.com/blader/humanizer) |
| `web-design-guidelines` | UI review against Vercel's guidelines | [vercel-labs/agent-skills](https://github.com/vercel-labs/agent-skills) |
| `find-skills` | Suggests installable skills from skills.sh | [vercel-labs/skills](https://github.com/vercel-labs/skills) |
| `security-audit` | Defensive security review (validator scripts not included) | [cloudflare/security-audit-skill](https://github.com/cloudflare/security-audit-skill) |
| `i-have-adhd` | Action-first, numbered output (run it yourself) | [ayghri/i-have-adhd](https://github.com/ayghri/i-have-adhd) |
| `apple-design` | Apple-style fluid, physical motion for the web | [emilkowalski/skill](https://github.com/emilkowalski/skill) |
| `emil-design-eng` | UI polish and component details | [emilkowalski/skill](https://github.com/emilkowalski/skill) |
| `animate` | Building a single animation the right way | [emilkowalski/skill](https://github.com/emilkowalski/skill) |
| `animation-performance` | Keeping animations inside the frame budget | [emilkowalski/skill](https://github.com/emilkowalski/skill) |
| `find-animation-opportunities` | Where motion is missing, and where it isn't | [emilkowalski/skill](https://github.com/emilkowalski/skill) |
| `improve-animations` | Audit and plan for existing motion code | [emilkowalski/skill](https://github.com/emilkowalski/skill) |
| `review-animations` | Strict motion review (run it yourself) | [emilkowalski/skill](https://github.com/emilkowalski/skill) |
| `break-ui` | Stress-test UI with worst-case data | [emilkowalski/skill](https://github.com/emilkowalski/skill) |
| `pick-ui-library` | Picks a library for a frontend task (run it yourself) | [emilkowalski/skill](https://github.com/emilkowalski/skill) |

</details>

My `project-pipeline` also calls separately installed tools: the plugins `superpowers`, `ui-ux-pro-max`, `diagram-design` and the skills `design-taste-frontend`, `impeccable`, `playwright-cli`, `img2threejs`, `remotion-best-practices` and a motion graphics skill. Swap them for yours.
