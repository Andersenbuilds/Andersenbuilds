---
name: project-kickoff
description: Interview the user about a new project, then create its directory structure and starter files. Use at the very start of any new project — when the user says "new project", "start something new", "set this up", "scaffold this", "kick this off", "help me start", or is sitting in an empty or near-empty directory describing something they want to build. Covers software repos, video and content production projects, no-code automation pipelines, and research projects. Trigger even if the user does not say the word "project" — a description of something they are about to start building counts. Do NOT use for documenting a codebase that already exists; that is what /init does.
---

# Project Kickoff

Turn a vague "I want to build X" into a scoped project with real files on disk, in one pass.

Two halves: a **structured interview** to pin down what is actually being built, then a **scaffold** that writes the folders and files from those answers. Do not skip the interview and do not scaffold from assumptions — the whole point is that the generated files reflect this specific project.

Run the steps in order.

---

## Step 0 — Read the room

Before asking anything, look at where you are:

- List the working directory.
- Check whether it is a git repo and whether it has commits.

Then:

- **Empty or bare git repo** → proceed to Step 1.
- **Files already exist** → say exactly what is there, and ask whether to scaffold alongside them or stop. Never overwrite an existing file. If a file the scaffold wants to write is already present, skip it and report the skip.

## Step 1 — Identify the track

Ask one question, with `AskUserQuestion`, offering these four:

| Track | For |
|---|---|
| **Software** | An app, script, tool, site, API — anything where code is the deliverable |
| **Content** | Video, short-form, written series — anything where published media is the deliverable |
| **Automation** | A pipeline that runs without you — Make.com, cron, webhook, API glue |
| **Research** | Answering a question or producing a document — the deliverable is findings |

The answer selects which section of `references/interview.md` to use. If the project honestly spans two tracks, pick the one that describes the *deliverable*, and note the second in `CLAUDE.md` later.

## Step 2 — Run the interview

Read `references/interview.md` now. Ask the **common round**, then the **track round** for the track from Step 1.

How to ask:

- Use `AskUserQuestion`, batching related questions into single calls. Two or three rounds total, not fifteen separate prompts.
- Give real options drawn from the question bank, not open text boxes, wherever the answer space is knowable.
- Every question in the bank has a documented default. If the user shrugs, picks "whatever you think", or skips — take the default, say which default you took, and move on. A stalled interview is worse than a reasonable assumption.
- If an answer makes a later question pointless, drop it. Do not ask about a database when they said no backend.

## Step 3 — Play it back

Before creating anything, write a short summary block: what is being built, for whom, what done looks like, the stack or tools, and the constraint that matters most (deadline, budget, time per week).

Ask for a yes. If the user corrects something, fix it and re-summarize. This is the last cheap moment to catch a misunderstanding.

## Step 4 — Scaffold

Read `references/scaffolds.md` now. Create the shared core plus the track-specific layout.

Rules:

- Fill templates with real interview answers. A generated `CLAUDE.md` that says "TODO: describe the project" is a failure — it should describe *this* project.
- Create directories even when empty, each with a `.gitkeep`, so the structure is visible immediately.
- Report each file as you create it.
- Skip and report any file that already exists.

## Step 5 — Close out

Print:

1. A tree of what was created.
2. The three most useful next actions, specific to this project — not generic advice. For software that might be installing dependencies and writing the first failing test; for content it might be drafting the first script.
3. An offer to `git init` and make the first commit, or to commit into the existing repo. **Offer — do not run it.** Wait for a yes.

---

## Conventions the generated files must follow

- **One living file.** Project state goes in `CLAUDE.md` and nowhere else. Do not also produce `PROJECT.md`, `NOTES.md`, `DECISIONS.md`, or dated snapshots. When state changes later, that file is rewritten in place with a new changelog entry at the top.
- **Pragmatic over complete.** Minimal dependency manifests, no CI configs, no linter zoo, no folder invented "for later". Add what the project needs to start.
- **Plain prose.** Short sentences. Real specifics over hype words. Write "runs three times a week" not "seamlessly orchestrates a robust cadence."
