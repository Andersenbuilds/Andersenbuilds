# Handoff

State of this repo and what's still open. Rewritten in place — newest entry on top.

- 2026-09-20 — Corrected both overlay templates. They were built off invented colors/type/motion (dark indigo, coral, mint, Sora, glow/pulse effects) because this session only had `Andersenbuilds/Andersenbuilds` attached and assumed no brand guide existed (see the old open item 6, now resolved). There IS one — `andersenbuilds-brand` repo, `design-system.md` + `AB_CARD_BASELINE.md` — locked 4-color palette (`#1A1A1A` ink / `#FAFAFA` off-white / `#C2410C` orange / `#6B6B6B` warm-grey), Inter only, no gradients/shadows/glow ever, fade-and-rise motion capped at 300ms. Both templates rebuilt to match it exactly; the CTA copy now mirrors the real `05_cta_popup.svg` from the V9 production pack. **This account has 9 repos total** (see below) — only 3 are attached to this session as of this entry. Worth checking what else is stale before trusting anything this repo says about "current state."
- 2026-09-20 — Added `templates/pipeline-overlay.html` (automation flow-diagram overlay: 4 nodes light up in sequence, default labels match the real Sheets → Claude → Make.com → Beehiiv stack). Same design tokens as `overlay-kit.html` by convention, not by a written spec — see open item 6.
- 2026-09-20 — Added `docs/overlay-ideas.md` (backlog of overlay/animation ideas beyond the two already built).
- 2026-09-20 — Added `docs/higgsfield-ai-benchmark.md` (researched capability/pricing benchmark) and `templates/overlay-kit.html` (reusable growth-counter + join-CTA motion overlay for shorts — see file header for how to record it into CapCut).
- 2026-08-16 — Renamed the branch to `main` and pushed it. GitHub's default branch still points at the old name — see open item 3. Recorded the outstanding `playground` repo request and the existing `Howto101` repo, which were only in chat.
- 2026-08-16 — Added `docs/obs-longform-setup.md` (researched, untested). Aligned the skill README with `INSTALL.md`, which contradicted it on install method.
- 2026-08-16 — Built the `project-kickoff` skill and wrote `docs/how-my-setup-works.md`. Both committed. Skill is not yet installed on the laptop, and the dedicated skills repo does not exist yet.

---

## Current state

Branch: `main`.

`claude/directory-save-location-nle28s` still exists on GitHub, points at the identical commit, and is still marked as the repo's **default branch**. Clearing that is open item 3.

**Other repos on this account (checked 2026-09-20 via `list_repos`, not from memory):**

| Repo | Visibility | What it is |
|---|---|---|
| `andersenbuilds-brand` | private | **The real brand system.** `design-system.md`, `AB_CARD_BASELINE.md`, production card SVGs, `AB_COLLECTED_KNOWLEDGE.md`, skills for ideas/script/voice/fact-sweep, landing page, research files. This is almost certainly the primary AndersenBuilds content repo. |
| `personal-skills` | private | **Already the dedicated skills repo** — open item 2 below is stale, this exists and already has `project-kickoff/` in it plus several others (stop-slop, task-observer, youtube-research, instagram-research, watch-video...) and Claude memory backups. |
| `Howto101` | private | "How to 101" app. |
| `BilBlik-app` / `BilBlik` | private | Separate project, not yet looked at from this session. |
| `byggepris` | private | Separate project, not yet looked at from this session. |
| `AI-Mastery` | private | Separate project, not yet looked at from this session. |
| `agent-lab` | private | Separate project, not yet looked at from this session. |

Only `Andersenbuilds/Andersenbuilds`, `andersenbuilds-brand`, and `personal-skills` are attached to this session right now. The rest exist but haven't been opened — don't assume this file's "open items" below are still accurate for anything that touches skills or the brand repo specifically, since two of them (2 and 6) turned out to already be solved elsewhere.

```
HANDOFF.md                          this file
INSTALL.md                          how to install the skill, no terminal
docs/how-my-setup-works.md          notes on git, repos, what persists
docs/obs-longform-setup.md          OBS settings for 1080p YouTube long-form
docs/higgsfield-ai-benchmark.md     Higgsfield AI capability/pricing research
docs/overlay-ideas.md               backlog of overlay/animation ideas
templates/overlay-kit.html          growth counter + join CTA motion overlay (open in a browser)
templates/pipeline-overlay.html     automation flow-diagram overlay (open in a browser)
skills/project-kickoff/
  SKILL.md                          the skill itself
  README.md                         install + usage
  references/interview.md           question bank, per track
  references/scaffolds.md           file templates, per track
```

## What project-kickoff does

Run `/project-kickoff` in an empty folder at the start of a new project. It interviews you about what you're building — a common round plus a track-specific round for one of four tracks (software, content, automation, research) — plays the answers back for confirmation, then writes the folder structure and starter files from those answers. Generated files describe the actual project rather than containing TODO placeholders. It ends by offering to `git init` and commit, without running it.

It's the complement to the built-in `/init`, which documents a codebase that already exists. This one fires before any code does.

## Open items

### 1. Install the skill on this machine

Not done. The only install so far was inside a cloud container, which is gone.

Worth knowing why it kept not happening: opening the Claude Code desktop app **resumed the cloud session** rather than starting a local one. Same container, no access to the laptop's filesystem. Starting a genuinely local session is a separate action.

See `INSTALL.md` — it has the full no-terminal path. Short version: the skill lives in Malthe's own `skills` folder and is symlinked into `~/.claude/skills/`, so there's one copy, edited in place, live in Claude Code immediately.

### 2. ~~Create a dedicated skills repo~~ — RESOLVED, already exists

`Andersenbuilds/personal-skills` already exists and already has `project-kickoff/` in it, plus several more skills (stop-slop, task-observer, youtube-research, instagram-research, watch-video, docx/pptx/artifact-design extras) and Claude memory backups. This session just didn't know about it until checking `list_repos` on 2026-09-20.

Not yet done: the copy of `project-kickoff/` living in *this* repo (`skills/project-kickoff/`) has never been diffed against the one in `personal-skills` — they may have drifted. Worth comparing before treating either as canonical.

Leave `docs/how-my-setup-works.md` here regardless. It's notes about the setup, not a skill.

### 3. Finish the branch rename

`main` exists and is pushed. Two steps left, neither doable from a cloud session — changing a repo's default branch needs GitHub settings access the connected app doesn't have.

1. On github.com: `Settings → General → Default branch`, switch to `main`.
2. Then delete `claude/directory-save-location-nle28s`. GitHub refuses to delete a default branch, so step 1 must come first.

Both branches point at the same commit, so nothing is at risk either way — this is tidying, not recovery.

### 4. The `playground` repo, never created

Asked for early on: a private personal repo called `playground`. Still never created — confirmed via `list_repos` on 2026-09-20, no repo by that name exists among the 9 on this account. Trivial from a local session or github.com.

Item 2's "is this the same repo" question is answered: `personal-skills` is a real, separate, already-existing repo, and `playground` still doesn't exist. Two different things.

### 5. ~~Memory files only live in claude.ai Project knowledge~~ — PARTLY WRONG

This claimed git can't reach the memory files. Checked 2026-09-20: `AB_COLLECTED_KNOWLEDGE.md` is a real, git-tracked file in the `andersenbuilds-brand` repo, alongside `AB_CARD_BASELINE.md`, `FACT_STATUS.md`, `TODO.md`, `DIRECTION.md`, session logs, and more.

Genuinely open question, now more specific: is the copy in `andersenbuilds-brand` the same one referenced as living in claude.ai Project knowledge, kept in sync by hand, or has it forked into two versions that disagree? Don't trust either one as sole source of truth until that's checked.

### 6. ~~No written visual brand guide~~ — WRONG, RESOLVED

There is one, and it's locked: `andersenbuilds-brand` repo, `design-system.md` (web/general) + `AB_CARD_BASELINE.md` (video cards/overlays, wins on conflict). Four colors only — ink `#1A1A1A`, off-white `#FAFAFA`, orange `#C2410C`, warm-grey `#6B6B6B` — Inter only, no gradients/shadows/glow ever, near-square not pill/rounded, fade-and-rise motion capped at 300ms.

`templates/overlay-kit.html` and `templates/pipeline-overlay.html` were originally built without this (dark indigo, coral, mint, Sora, glow/pulse effects) because this session hadn't attached `andersenbuilds-brand` yet. Both were rebuilt same day to match the real spec once found. Any *other* on-screen asset built in this repo from here on must be checked against `AB_CARD_BASELINE.md` first — don't repeat this.

## Decisions already made

Don't relitigate these:

- **Skill installs to `~/.claude/skills/`, not a repo's `.claude/skills/`.** An in-repo skill only loads inside that repo. `project-kickoff` exists to start *new* projects, so an in-repo copy would only be available where it isn't needed.
- **Don't carry git history when moving the skill to a skills repo.** Clean slate is fine.
- **Text in git, heavy media out.** GitHub rejects files over 100MB and raw video blows past that. The scaffold gitignores media by default.
- **Git history doesn't replace memory files.** A new session reads files, not commit logs. Keep updating the memory files; commit them too. Reasoning is in `docs/how-my-setup-works.md`.
