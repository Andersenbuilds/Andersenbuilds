# Installing project-kickoff

No terminal needed. Claude Code runs the commands — you type plain English.

## Steps

1. Open the Claude Code desktop app.
2. Open your `skills` folder with it (folder picker — no terminal).
3. Paste the prompt below.

## The prompt

```
Clone https://github.com/Andersenbuilds/Andersenbuilds into a temp location,
copy skills/project-kickoff into this folder, then symlink it into
~/.claude/skills/ so edits here go live without copying. Confirm the skill
loads by listing ~/.claude/skills. Clean up the temp clone when done.
```

That's it. Verify by typing `/project-kickoff` — it should autocomplete.

## What that leaves you with

```
<your skills folder>/project-kickoff/     the real files, where you edit
~/.claude/skills/project-kickoff          a pointer to them
```

One copy, edited in your own folder, live in Claude Code immediately. No syncing, no second copy drifting out of date.

Later, when your skills folder becomes a git repo, the skill is already inside it and gets committed like any other file.

## If the symlink gives trouble

Windows sometimes needs elevated permissions for symlinks. If it fails, tell Claude to copy the folder instead:

```
Just copy project-kickoff into ~/.claude/skills/ instead of symlinking.
```

Tradeoff: two copies, so after editing in your skills folder you'd ask Claude to re-copy it. Works fine, one extra step.

## Adding skills later

Same pattern for every future skill: write it in your skills folder, symlink it into `~/.claude/skills/`, and it's available in every project.
