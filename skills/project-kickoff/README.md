# project-kickoff

A Claude Code skill. Interviews you about a new project, then creates its folders and starter files from your answers.

Covers four project types: software, content/video, automation pipelines, and research.

## Installing it

The folder is self-contained — nothing in it references an absolute path or the repo it was written in. Copy it wherever you want it and it works.

**For one machine, all projects:**

```
cp -r project-kickoff ~/.claude/skills/
```

**For a single project only:**

```
cp -r project-kickoff /path/to/project/.claude/skills/
```

Then start a new Claude Code session and run `/project-kickoff`. It also triggers on its own when you describe something you are about to start building.

## Moving it to a skills repo

Copy the whole `project-kickoff/` folder in. To use it from there, either symlink it into `~/.claude/skills/`:

```
ln -s /path/to/skills-repo/project-kickoff ~/.claude/skills/project-kickoff
```

or copy it across after each change.

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
