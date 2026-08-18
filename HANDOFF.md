# Handoff

State of this repo and what's still open. Rewritten in place — newest entry on top.

- 2026-08-16 — Renamed the branch to `main` and pushed it. GitHub's default branch still points at the old name — see open item 3. Recorded the outstanding `playground` repo request and the existing `Howto101` repo, which were only in chat.
- 2026-08-16 — Added `docs/obs-longform-setup.md` (researched, untested). Aligned the skill README with `INSTALL.md`, which contradicted it on install method.
- 2026-08-16 — Built the `project-kickoff` skill and wrote `docs/how-my-setup-works.md`. Both committed. Skill is not yet installed on the laptop, and the dedicated skills repo does not exist yet.

---

## Current state

Branch: `main`.

`claude/directory-save-location-nle28s` still exists on GitHub, points at the identical commit, and is still marked as the repo's **default branch**. Clearing that is open item 3.

Other repos on this account: `Andersenbuilds/Howto101` (private, last pushed 2026-08-11) — the "How to 101" app, separate from this work.

```
HANDOFF.md                          this file
INSTALL.md                          how to install the skill, no terminal
docs/how-my-setup-works.md          notes on git, repos, what persists
docs/obs-longform-setup.md          OBS settings for 1080p YouTube long-form
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

### 2. Create a dedicated skills repo

Not done — the cloud session's GitHub App lacked repo-creation permission. From a local session with your own GitHub login this is unblocked.

Create an empty repo (personal, private is fine), then:

```
cp -r skills/project-kickoff <skills-repo>/
```

Commit it there. Don't try to carry the git history across — it's two commits and none of it matters.

Leave `docs/how-my-setup-works.md` here. It's notes about the setup, not a skill; the skills repo shouldn't become a junk drawer.

### 3. Finish the branch rename

`main` exists and is pushed. Two steps left, neither doable from a cloud session — changing a repo's default branch needs GitHub settings access the connected app doesn't have.

1. On github.com: `Settings → General → Default branch`, switch to `main`.
2. Then delete `claude/directory-save-location-nle28s`. GitHub refuses to delete a default branch, so step 1 must come first.

Both branches point at the same commit, so nothing is at risk either way — this is tidying, not recovery.

### 4. The `playground` repo, never created

Asked for early on: a private personal repo called `playground`. Never created — the cloud session's GitHub App lacks repo-creation permission (403 on personal, 404 on org), and there's no `gh` CLI. Still outstanding, and trivial from a local session or github.com.

Worth deciding whether `playground` and the skills repo in item 2 are the same thing or two separate repos.

### 5. Memory files (open question, not a task)

`AB_COLLECTED_KNOWLEDGE.md` and the other memory files live in claude.ai Project knowledge, so git doesn't reach them and Claude Code can't read them. Moving them into a repo would mean maintaining them somewhere both can see. Real workflow change, not a free upgrade — undecided.

## Decisions already made

Don't relitigate these:

- **Skill installs to `~/.claude/skills/`, not a repo's `.claude/skills/`.** An in-repo skill only loads inside that repo. `project-kickoff` exists to start *new* projects, so an in-repo copy would only be available where it isn't needed.
- **Don't carry git history when moving the skill to a skills repo.** Clean slate is fine.
- **Text in git, heavy media out.** GitHub rejects files over 100MB and raw video blows past that. The scaffold gitignores media by default.
- **Git history doesn't replace memory files.** A new session reads files, not commit logs. Keep updating the memory files; commit them too. Reasoning is in `docs/how-my-setup-works.md`.
