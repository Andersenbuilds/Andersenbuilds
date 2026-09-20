# Overlay & animation ideas — backlog

Brainstormed list of motion overlays for shorts and long-form, filtered through the 5 priorities (list growth, 3+ shorts/week floor, completion rate / 3-sec hold, public automation building, day-90 product). Only `overlay-kit.html`'s two components (growth counter, join CTA) are built. Everything else here is backlog, not committed work — build on demand, not proactively.

- 2026-09-20 — First version.

---

## Build next (highest leverage, nothing built yet)

- **Automation flow-diagram overlay** — nodes lighting up in sequence as a real Make.com scenario fires (Claude → Make → Beehiiv), synced to voiceover. Makes the automation pipeline legible in 2 seconds instead of "here's a screen full of boxes." Directly serves priority #4 — the automation *is* the content.
- **API ping animation** — a pulse/dot traveling between two labeled boxes when narrating "this calls Claude" / "this hits the Beehiiv API." Cheap, reusable in every automation video.
- **Time/cost-saved ticker** — "$0 → 340 DKK saved" or "6 hrs → 12 min," counting during the hook. Same mechanic as the existing growth counter, different number. Strong for "I automated X" hooks — priority #3.
- **Status checklist** — steps ticking ⏳ → ✓ as a workflow runs on screen.

## Already built

- **Growth counter** (`templates/overlay-kit.html`) — ticks to a subscriber number with a drawing-in 7-day trend line.
- **Join CTA** (`templates/overlay-kit.html`) — pulsing lower-third pill, "join the free list."

## Worth building later, not urgent

- **Progress bar toward the 90-day / 2.5M DKK goal** — same counter mechanic as the growth counter, pointed at the bigger number. Doubles as build-in-public content on its own.
- **Before/after split-reveal** — manual process vs. automated, wiped/swiped to compare. Good for "here's what changed" hooks.
- **Chapter/section title cards** — slide in, hold, slide out. Long-form pacing only.
- **Top-of-screen progress bar** — shows how much of a long-form video is left. Direct long-form retention lever.
- **Social-proof ticker** — "1,248 builders already in," animating up. Hold until the number is big enough to be a flex — small numbers undercut themselves.
- **QR-to-subscribe** — long-form only, corner overlay during a natural pause, scans straight to Beehiiv.

## Deliberately not building yet

- **Logo sting/intro** — actively risky against the 3-second hold; don't add a delay before the hook.
- **Testimonial/quote cards** — no testimonials yet, nothing to put in it.
- **Lower-third name cards** — not doing guest interviews.
- **Price-reveal/launch countdown** — real need, but it's a day-90 problem. Building it now is the "shiny tool before finishing the current step" trap.
