---
name: claude-md-audit
description: Audit and slim down CLAUDE.md files (global and project) when Claude ignores rules, answers slowly, contradicts itself or burns tokens on stale context. Use when the user asks to clean up, review or shorten their CLAUDE.md, or after a model upgrade.
disable-model-invocation: true
---

# CLAUDE.md audit

Every line in a CLAUDE.md is loaded into every session. Stale, duplicated or contradictory instructions cost tokens and make newer models follow the wrong rule. This skill finds those lines and proposes a shorter file. It never rewrites the file without the user's go-ahead.

## 1. Collect

Read every instruction file that loads into a session:

- the global file (`~/.claude/CLAUDE.md`, on Windows `C:\Users\<user>\.claude\CLAUDE.md`)
- the project file (`./CLAUDE.md`, `./.claude/CLAUDE.md`) and any files they import with `@path`
- rules that live elsewhere and overlap: skill descriptions the user relies on, `settings.json` permissions

Report the size of each file in lines and an estimate in tokens (about 4 characters per token).

## 2. Classify every instruction

Put each instruction into exactly one bucket:

| Bucket | Meaning | Action |
|---|---|---|
| Keep | Specific, still true, changes behaviour | keep, tighten wording |
| Stale | Refers to tools, paths, models, versions or workflows that no longer exist | remove |
| Duplicate | Says the same as another line, a skill, or the model's default behaviour | remove or merge |
| Conflict | Contradicts another line or a newer instruction | ask which one wins |
| Vague | "Write clean code", "be careful" — no testable behaviour | make specific or remove |
| Belongs elsewhere | Long how-to or reference material | move into a skill or a separate file loaded on demand |
| Workaround | Compensates for an old model's weakness ("ALWAYS", "NEVER" in caps, repeated warnings) | soften or remove; newer models over-apply shouted rules |

Verify "stale" claims before calling them stale: check that the path, command or tool really is gone.

## 3. Report

Show a table: line or section, bucket, reason, proposed action. Then the token count before and after. List conflicts as questions.

## 4. Rewrite — only after the user agrees

- Keep the user's own wording where it is already precise.
- Order: what the project is, hard rules (security, privacy, things never to do), workflow, style.
- One instruction per line, no repetition, no capital-letter shouting.
- Move bulky reference material into a skill or a linked file instead of deleting it.
- Back up the old file next to it (`CLAUDE.md.bak`) before writing.

## 5. Check

Start a fresh session mentally against the new file: would each removed rule have changed an answer? If yes, restore it.

---
Written in own words from a public "clean up your CLAUDE.md" audit-prompt idea; no third-party text copied.
License: CC-BY-NC-SA-4.0 — © HCvCH, https://github.com/HCvCH/claude-auto-kit (see NOTICE.md)
