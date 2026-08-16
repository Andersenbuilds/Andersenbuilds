# Interview question bank

Every question below has a **default**. Use it when the user skips, shrugs, or says "you decide" — announce which default you took, then keep moving.

Ask the common round first, then only the track round matching Step 1.

---

## Common round — every track

Batch these into one or two `AskUserQuestion` calls.

**1. What is it, in one sentence?**
Free text. This is the only question with no default — if it cannot be answered, the project is not ready to scaffold, and the right move is to talk it through rather than create files.

**2. Why does it exist / who is it for?**
Options: Just me (a tool for my own use) · A specific audience (they can name it) · A client or employer · Public/open.
*Default: Just me.*

**3. What does "done" look like?**
Free text, but push for something checkable. "A working X I use every week" beats "a great X". If they give something vague, offer a sharper restatement and confirm it.
*Default: first working version running end to end.*

**4. Time budget?**
Options: A single session · A week of evenings · Ongoing, no end date · Hard deadline (ask the date).
*Default: A week of evenings.*

**5. Anyone else touching this?**
Options: Solo · Solo now, others later · Collaborators from the start.
*Default: Solo.*

**6. Should this stay private?**
Options: Private · Public · Not decided.
Matters because it changes what goes in `.gitignore`, whether secrets get a `.env.example`, and how the README is written.
*Default: Private.*

---

## Software track

**Language / runtime.**
Options: Python · TypeScript/Node · Plain HTML+JS (no build step) · Something else (ask).
*Default: Python for scripts, tools, and data work; TypeScript for anything with a web UI.*

**Framework.**
Only ask if the language answer leaves it open. Offer the two or three that actually fit what they described, plus "none — plain files".
*Default: none. Do not add a framework the project has not asked for.*

**What shape is it?**
Multi-select: Command-line tool · Web UI · API/service · Scheduled job · Library.
*Default: Command-line tool.*

**Does it need to store data?**
Options: No · Local files (JSON/CSV/SQLite) · A real database (ask which).
*Default: No. If they are unsure, local files — SQLite is easy to graduate from.*

**Where does it run when it's finished?**
Options: My machine only · A server/VPS · Serverless or a host like Vercel/Railway · Not decided.
*Default: My machine only.*

**Testing?**
Options: Real tests from the start · A smoke test I can run by hand · None for now.
*Default: A smoke test. Skip the test folder entirely if they say none.*

**External services or API keys?**
Free text or multi-select if they hinted at any (Claude API, ElevenLabs, Beehiiv, Google Sheets, Stripe, …). Each named service becomes a line in `.env.example`.
*Default: none — and then no `.env.example` is written.*

---

## Content track

**Format and length.**
Options: Short-form vertical, under 60s · Short-form, 60–90s · Long-form video · Written (newsletter/article) · Mixed.
*Default: Short-form vertical, under 60s.*

**Platforms.**
Multi-select: Reels · TikTok · YouTube Shorts · Newsletter · Blog.
*Default: Reels + TikTok + YouTube Shorts.*

**Cadence and volume.**
Options: One-off · Weekly batch (ask how many) · Ongoing series, no fixed cadence.
*Default: Weekly batch of 3.*

**Standalone, or part of an existing pipeline?**
Options: Standalone · Feeds an existing brand/channel (ask which).
If it feeds an existing channel, the scaffold should not duplicate voice or brand rules — it should point at wherever they already live rather than restating them.
*Default: Standalone.*

**Where do raw assets live?**
Options: In this folder · External drive or cloud (ask where) · Not decided.
Drives whether `assets/` is real or a pointer, and whether media extensions get gitignored.
*Default: In this folder, with media gitignored.*

**Is there a written companion?**
Options: No · Newsletter issue per video · Blog post per video.
*Default: No.*

---

## Automation track

**What starts it?**
Options: Schedule (ask how often) · Webhook or incoming event · Manual run · File or sheet change.
*Default: Schedule, daily.*

**Where does data come from, and where does it end up?**
Free text for both. Be concrete — "Google Sheet named X" not "a spreadsheet".
*Default: none assumed; ask again once if the answer is too vague to write down.*

**How is it built?**
Options: Make.com scenario · A script I run · Script on a schedule (cron/GitHub Actions) · Not decided.
*Default: A script I run. Easiest to test, easiest to promote to scheduled later.*

**Credentials needed?**
Free text or multi-select from services already mentioned. Each becomes a line in `.env.example`.
*Default: none.*

**What happens when it fails?**
Options: Notify me · Retry then notify · Log it and move on · Not thought about it.
*Default: Log it and move on — with a note in `CLAUDE.md` that failure handling is unresolved.*

**How often will it actually run?**
Only ask if the trigger is a schedule and they have not already said. Volume decides whether a run log is a file or needs somewhere real to go.
*Default: daily.*

---

## Research track

**What is the central question?**
Free text. Push for a question with an answer, not a topic. "Which of these three tools is cheapest at my volume" beats "research AI tools".
*No default — same as the common round's first question.*

**What kinds of sources count?**
Multi-select: Official docs · Academic papers · Blogs and forums · My own testing · Interviews.
*Default: Official docs + my own testing.*

**What is the output?**
Options: A written summary · A comparison table · A decision with reasoning · Input for something else (ask what).
*Default: A written summary.*

**Deadline?**
Options: None · Specific date (ask) · Blocking something else (ask what).
*Default: None.*
