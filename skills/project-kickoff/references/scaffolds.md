# Scaffold specifications

What to create, per track. Every placeholder in `{braces}` gets filled from interview answers — never leave one literal, and never write "TODO" where an answer exists.

---

## Shared core — every track

### `CLAUDE.md`

The single living file for project state. Changelog at the top, newest first. When state changes later, this file is rewritten in place — never copied to `CLAUDE_v2.md` or a dated variant.

```markdown
# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Changelog

- {today's date} — Project created. {one-line summary of the kickoff decisions.}

## Project

{one-sentence description from the interview}

Built for: {audience answer}
Track: {software | content | automation | research}

## Goal

{what "done" looks like, in checkable terms}

## Constraints

- Time: {time budget answer}
- People: {solo/collaborators answer}
- Visibility: {private/public answer}
{- any track-specific constraint worth pinning, e.g. deadline, run cadence, publishing cadence}

## Stack

{tools, languages, services actually chosen. Omit this section for research projects with no tooling.}

## Current state

Just scaffolded. Nothing built yet.

## Open loops

{anything the interview left unresolved — a deferred decision, an unanswered question, a "not decided" answer. If the interview resolved everything, write "None." and mean it.}
```

### `README.md`

Short. What it is, how to run it, nothing else. No badges, no roadmap section, no contributing guide unless collaborators were mentioned.

```markdown
# {project name}

{one-sentence description}

## Running it

{concrete commands for the chosen stack, or concrete steps for non-software tracks}

## Status

{one line — what works today}
```

### `.gitignore`

Match the track. Always include OS noise (`.DS_Store`), and always include `.env` if any credentials were named.

---

## Software track

```
src/
tests/            (skip entirely if testing answer was "none")
.env.example      (only if services/keys were named)
{manifest}
```

**Manifest by language:**

- Python → `pyproject.toml`, minimal: name, version, requires-python, and only the dependencies actually named. No dev-tooling section unless testing was requested.
- TypeScript/Node → `package.json` with name, version, type module, and a `start` script. Add `tsconfig.json` only if TypeScript specifically (not plain JS).
- Plain HTML+JS → no manifest. `index.html`, `style.css`, `app.js` at root instead of `src/`.

**Starter file:** create one real entry point (`src/main.py`, `src/index.ts`, or `index.html`) that runs and prints or renders something. Not an empty file — something the user can execute in the first minute to confirm the setup works.

**`.env.example`:** one line per named service, key name only, no values.

```
CLAUDE_API_KEY=
ELEVENLABS_API_KEY=
```

**`.gitignore`:** language-appropriate (`__pycache__/`, `.venv/`, `node_modules/`, `dist/`), plus `.env`.

---

## Content track

```
scripts/          one file per piece, drafts live here
assets/           raw media (gitignored unless assets are external)
published/        what has shipped, with dates
ideas.md          the running idea spine
```

**`ideas.md`:**

```markdown
# Ideas

One line per idea. Move to scripts/ when it gets drafted, delete when published.

## Up next

- 

## Someday

- 
```

**`scripts/`:** seed one template file named for the format, e.g. `scripts/_template.md`, with the structure the user's format needs (hook / body / CTA for short-form). If the project feeds an existing brand, do **not** restate voice rules here — write one line pointing at wherever they already live.

**`.gitignore`:** media extensions (`*.mp4`, `*.mov`, `*.wav`, `*.png`, `*.jpg`) unless assets were said to live externally, plus `.DS_Store`.

---

## Automation track

```
workflows/        one markdown file per automation
.env.example      (if credentials were named)
runlog.md
```

**`workflows/{name}.md`** — one per automation, documenting it in plain language before any code exists:

```markdown
# {automation name}

**Trigger:** {schedule, webhook, manual, file change}
**Source:** {where data comes from}
**Destination:** {where it ends up}
**Built with:** {Make.com | script | scheduled script}

## Steps

1. 
2. 

## On failure

{failure handling answer}

## Credentials

{names of keys needed, no values}
```

**`runlog.md`:** newest first, one line per run — date, outcome, anything odd. Seeded with a header and nothing else.

**If built as a script:** also create the software-track manifest and a `src/` entry point for the chosen language. A Make.com scenario gets no code scaffold — the workflow doc is the deliverable.

**`.gitignore`:** `.env`, plus language files if a script was scaffolded.

---

## Research track

```
sources/          saved references, one file or clipping per source
notes.md          working notes as you go
{output stub}     named for the chosen output format
```

**`notes.md`:** header plus a "Questions still open" section seeded with the central question.

**Output stub** — match the answer:

- Written summary → `summary.md` with the central question as the H1 and empty sections.
- Comparison table → `comparison.md` with a markdown table, columns filled from whatever is being compared if known.
- Decision → `decision.md` with Question / Options / Criteria / Decision / Reasoning headings.

**`.gitignore`:** `.DS_Store` and any large downloaded source formats (`*.pdf` only if they said sources get saved locally in bulk).

---

## After creating files

Report the tree. Then check one thing before closing out: does `CLAUDE.md` describe *this* project specifically? If any section could be pasted into an unrelated project unchanged, it is too generic — rewrite it from the interview answers.
