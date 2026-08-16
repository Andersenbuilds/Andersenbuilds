# How my setup works

Plain-language notes on git, repos, and what actually gets saved when working in Claude Code. Written down so a future session (or a future me) doesn't have to re-derive it.

- 2026-08-16 — First version. Written after a session on directories, repos, and what survives a container.

---

## Directory vs repo

**Directory = folder.** A place that holds files. "Directory" is just what developers call a folder.

**Repo = a folder with git switched on inside it.** Still an ordinary folder with your files in it. The difference is a hidden `.git` folder that records every version of every file, and can sync to GitHub.

Every repo is a directory. Not every directory is a repo.

Delete the hidden `.git` folder and you still have the same files in the same folder. You've just lost the history and the link to GitHub.

## What actually saves

Claude Code on the web runs in a container that gets wiped when the session ends. A plain folder there has nowhere to survive to.

Being a repo does not save anything on its own. It takes two steps:

1. **Commit** — records the current state of the files into git history, locally.
2. **Push** — sends that history to GitHub.

A repo that was never pushed dies with the container exactly like a plain folder. Git tracks history; GitHub is what makes it survive.

## What belongs in a repo

**Text belongs in.** Code, scripts, notes, docs. Cheap to track, all worth saving.

**Heavy media stays out.** GitHub rejects files over 100MB, and raw video blows past that instantly. Scripts and notes go in the repo; the `.mp4` files live on a drive. The content scaffold in `project-kickoff` gitignores media by default for this reason.

**Throwaway work stays out too.** Scratch tests and one-off experiments don't need history.

## Git history is not documentation

Git and memory files (`AB_COLLECTED_KNOWLEDGE.md` and similar) do different jobs. One does not replace the other.

- **Git records what changed.** Every version, forever.
- **The memory file records what's true right now.** One curated summary, readable in thirty seconds.

After 200 commits, `git log` can technically show how the project got here, but nobody reads 200 diffs to find out where things stand. Git preserves history. It doesn't synthesize it.

The decisive part: **a new Claude session reads files, not git history.** Nothing walks the commit log to rebuild context. It reads the memory file and knows where things are. That file *is* the handoff mechanism — committing more often would not replace it.

Best setup: keep updating the memory files, and commit them too. Readable current state in the file, full history of how it changed in git.

Open question: the memory files currently live in claude.ai Project knowledge, not on a filesystem, so git doesn't reach them where they are today. Moving them into a repo would mean maintaining them somewhere Claude Code can see.

## Where skills live

Claude Code looks for skills in two places:

- `~/.claude/skills/` — available in every project, on that machine.
- `.claude/skills/` inside a repo — loads automatically whenever working in that repo.

On the web, `~/.claude/skills/` starts empty every session, because the container is fresh. So for web work, skills committed to a repo's `.claude/skills/` are the ones that actually show up.

## Symlinks

Only relevant when working locally, not on the web.

A symlink is a pointer file. It looks like a normal folder but holds no content — it says "the real thing is over there," and anything reading it gets redirected.

Useful for skills: keep one real copy in a skills repo under git, and put a pointer to it in `~/.claude/skills/`. Edit the file in the repo and the change is live immediately, with no copying and nothing to keep in sync.

```
ln -s ~/skills-repo/project-kickoff ~/.claude/skills/project-kickoff
```

Symlinks are per-machine. Set up once on each computer.
