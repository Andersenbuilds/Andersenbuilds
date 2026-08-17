# Handoff

State of this repo and what's still open. Rewritten in place — newest entry on top.

- 2026-08-16 — Built the `project-kickoff` skill and wrote `docs/how-my-setup-works.md`. Both committed. Skill is not yet installed on the laptop, and the dedicated skills repo does not exist yet.

---

## Current state

Branch: `claude/directory-save-location-nle28s`. This is also the repo's **default branch** — the repo was empty before this work, so there is no `main`.

```
HANDOFF.md                          this file
docs/how-my-setup-works.md          notes on git, repos, what persists
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

```
cp -r skills/project-kickoff ~/.claude/skills/
```

Then `/project-kickoff` is available in every folder, permanently. Verify with `ls ~/.claude/skills/project-kickoff`.

### 2. Create a dedicated skills repo

Not done — the cloud session's GitHub App lacked repo-creation permission. From a local session with your own GitHub login this is unblocked.

Create an empty repo (personal, private is fine), then:

```
cp -r skills/project-kickoff <skills-repo>/
```

Commit it there. Don't try to carry the git history across — it's two commits and none of it matters.

Leave `docs/how-my-setup-works.md` here. It's notes about the setup, not a skill; the skills repo shouldn't become a junk drawer.

### 3. Rename the default branch to `main` (optional)

Cosmetic. `claude/directory-save-location-nle28s` works fine but is an odd name for a repo's permanent default. Renameable from GitHub's branch settings, or:

```
git branch -m claude/directory-save-location-nle28s main
git push -u origin main
```

Then change the default in GitHub settings and delete the old remote branch.

### 4. Memory files (open question, not a task)

`AB_COLLECTED_KNOWLEDGE.md` and the other memory files live in claude.ai Project knowledge, so git doesn't reach them and Claude Code can't read them. Moving them into a repo would mean maintaining them somewhere both can see. Real workflow change, not a free upgrade — undecided.

## Decisions already made

Don't relitigate these:

- **Skill installs to `~/.claude/skills/`, not a repo's `.claude/skills/`.** An in-repo skill only loads inside that repo. `project-kickoff` exists to start *new* projects, so an in-repo copy would only be available where it isn't needed.
- **Don't carry git history when moving the skill to a skills repo.** Clean slate is fine.
- **Text in git, heavy media out.** GitHub rejects files over 100MB and raw video blows past that. The scaffold gitignores media by default.
- **Git history doesn't replace memory files.** A new session reads files, not commit logs. Keep updating the memory files; commit them too. Reasoning is in `docs/how-my-setup-works.md`.
