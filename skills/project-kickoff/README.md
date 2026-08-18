# project-kickoff

A Claude Code skill. Interviews you about a new project, then creates its folders and starter files from your answers.

Covers four project types: software, content/video, automation pipelines, and research.

## Installing it

The folder is self-contained — nothing in it references an absolute path or the repo it was written in. It works wherever you put it.

Claude Code reads skills from `~/.claude/skills/`. Keep the real folder wherever you edit it and symlink it in, so there's only ever one copy:

```
ln -s /path/to/project-kickoff ~/.claude/skills/project-kickoff
```

Edits then go live immediately, with nothing to keep in sync. If symlinking is awkward — Windows sometimes needs elevated permissions — copy it instead and re-copy after each change:

```
cp -r project-kickoff ~/.claude/skills/
```

Either way, start a new Claude Code session and run `/project-kickoff`. It also triggers on its own when you describe something you are about to start building.

**For a single project only**, put it in that project's `.claude/skills/` instead. Worth knowing this is usually the wrong choice for this particular skill — it exists to start *new* projects, so an in-repo copy only loads where you don't need it.

## What's inside

```
project-kickoff/
├── SKILL.md                   the pipeline: read the room, interview, confirm, scaffold
└── references/
    ├── interview.md           question bank per track, every question with a default
    └── scaffolds.md           folder layouts and file templates per track
```

`SKILL.md` loads when the skill triggers. The two reference files load only when that step is reached.

## Editing it

Change the questions in `references/interview.md`. Change what gets created in `references/scaffolds.md`. Change when it triggers by editing the `description` line in `SKILL.md` — that line is what Claude matches against, so it needs to name the situations and phrases that should set it off.
