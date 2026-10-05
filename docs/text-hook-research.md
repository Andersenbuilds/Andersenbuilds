# Text hooks — breakdown of @mino.mp4's "text hooks" short

Source: a 1:46 TikTok by @mino.mp4 (talking head, 576×1024 download), sent by Malthe on 2026-10-05. Script below was pulled from the video's burned-in captions with OCR (Whisper was blocked on the cloud network). Cut count was measured from frame differences. Nothing here is guessed from the title. Visual notes come from frames that were actually looked at.

- 2026-10-05 — First version. Analysis + an implementation plan. The template is `templates/text-hook-overlay.html`.

---

## 1. What the video claims (the 3 rules)

| # | Rule | His example |
|---|---|---|
| 1 | **Always use a specific name or a specific number.** It tells the viewer why they should listen. | "Software engineer at Google." "I'm 22 years old." |
| 2 | **The 10x pass (MrBeast's thought experiment).** Write one draft. Then ask: *"What would this look like if it was 10 times more extreme?"* | Mild: "POV: reading a letter from college to my mom." 10x: "POV: getting kicked out of my house by my mom for becoming a disappointment." |
| 2b | **Add an audience keyword.** One word that tells a specific crowd "this is about you." | He shipped "POV: You became a disappointment to your Korean mom." "Korean" pulls in the Asian audience. |
| 3 | **The overlay method (bonus).** Show pictures instead of text to represent the idea. | For a storytelling video he put the Spider-Man: Brand New Day poster next to the Odyssey poster as the hook. |

His claimed payoff: about 5 extra minutes per video, "the highest lever you can pull," "can 10x your views."

**The most useful moment in the video is one he barely stresses.** After the 10x version he says: "Now obviously that didn't happen. My mom still loves me." Then he pulls back to a version that is extreme *but true*. So the real method has three steps, not two:

1. **Draft:** write the plain version.
2. **10x:** push it as far as it goes.
3. **Truth pull-back:** walk back to the most extreme version that is still 100% true.

Step 3 is the one AndersenBuilds needs. The brand runs on real numbers. A 10x hook that isn't true wins the 3-second hold and then loses the trust. Be extreme about the **stakes and framing**, never about the **facts**.

## 2. Hook breakdown (0–5s)

- **Visuals:** The hook overlay is already on screen in frame 1. There is no build-up. Top third: a **proof stack** of 4 view-count chips (1.6M, 564.6K, 218.9K, 3.8M) plus a white "Net followers 19.3K" analytics card. Under it, two lines of white text: *"this takes 5 MINUTES but got me 19K followers last month."* His face is in the middle third. Word-by-word captions sit in the lower-middle.
- **Audio:** "The most underrated skill in content right now is mastering text hooks."
- **Why it works:** two hooks run at the same time on two channels.
  - *On-screen* = a cost/reward gap: "5 MINUTES" (tiny cost, in caps) against "19K followers" (big result). The proof stack makes it believable before he says a word.
  - *Spoken* = a contrarian claim: "most underrated skill." It creates a curiosity gap.
  - The viewer who reads and the viewer who listens both get hooked. Neither has to wait for the other.

## 3. Pacing and retention mechanics

- **Length:** 105s. That is long for a short. He survives it with a numbered list ("Number one…", "Third…"). The numbers work like a progress bar, so viewers know how much is left.
- **Cuts:** 18 hard jump cuts in 105s, about **1.7 per 10s**. That is slow. The real pacing comes from:
  - **Captions:** 1–3 words per card, changing about every 0.5s. This is the main thing moving on screen.
  - **RGB lighting:** red/blue/green LEDs in the background, so the colour changes between cuts.
  - **Big gestures and faces:** e.g. a scrunched face on "gripping titles" at 0:31.
- **Context phase (0:04–0:16):** credibility. "30,000 followers in the last 2 months." Then the **only B-roll in the video** at 0:10–0:13: a laptop showing a Miro board of his hook research, as he says "I spent two hours today compiling everything." It proves the effort and acts as a pattern interrupt at the 10s mark.
- **Value phase (0:16–1:40):** three rules. Each one is proven with **his own video** as a picture-in-picture thumbnail with its view count (1.1M at 0:45–1:04, 218.9K at 1:23–1:28, a poster collage at 1:29–1:32). The proof is always his own work, never someone else's.
- **Retention reward (1:10):** "This one's a bonus tip, just because I like you so much because you stayed until 63 seconds into the video." He rewards the people still watching, right before the stretch where completion usually drops.
- **Dead zones:** the longest runs with no cut are 0:36–0:53 (17s) and 1:08–1:24 (16s). Both are saved by the picture-in-picture inserts and fast captions. Without those, they would be drop-off points.

## 4. CTA

Soft and nearly hard-stop: "Try this out." Then TikTok's own end card (from the download, not his edit). No follow ask, no keyword, no link. It's one action, which is good, but it builds nothing he owns.

**Do not copy this part.** Every AndersenBuilds short ends on the one list ask, in Malthe's real voice.

## 5. What to copy, what not to

| Copy | Don't copy |
|---|---|
| Hook overlay on screen from frame 1, no intro | Fake 10x hooks. He admits "that didn't happen." AndersenBuilds only uses true ones. |
| Proof stack on screen during the hook | Big view counts as the proof. Malthe's numbers are small right now. Use **cost / time / day count** as the proof (`$1,400`, `Day 23`, `6 hrs → 12 min`). Small follower numbers undercut themselves. See `overlay-ideas.md`. |
| Specific identity + number ("Software engineer at Google") | His RGB-lit bedroom look. The brand is locked to 4 colours, no glow. See `AB_CARD_BASELINE.md`. |
| Own-video picture-in-picture as proof for each point | A 105s runtime. Malthe's floor is 3 shorts/week. Keep one rule per short at 30–45s and you get three shorts out of this one idea. |
| Numbered list as a progress bar | A dead-end CTA ("try this out") |
| Mid-video retention reward line | |

## 6. Implementation for AndersenBuilds

### A. The 3-step hook pass (Claude, inside the script workflow)

Add it as a step before grading. It also works as a Make.com step (Sonnet is fine, it's cheap autopilot work).

```
You write short-form text hooks for AndersenBuilds: a non-technical grocery store
apprentice in Denmark building an AI business in public on a $1,400 budget.
Audience: solopreneurs and freelancers, 22–40, not developers.

Topic and true facts for this video:
{{topic}}
{{facts}}

Do three passes. Show all three.
1. DRAFT: one plain, honest hook, max 12 words.
2. 10X: ask "what would this look like if it was 10 times more extreme?" and write it.
   Exaggerating is allowed in this pass only.
3. TRUE 10X: walk back to the most extreme version where every claim is in {{facts}}.
   Must contain one specific number or name, and one audience keyword
   (e.g. "non-coder", "solo", "freelancer", "grocery store apprentice").
   If a claim isn't in {{facts}}, cut it.

Then list 2–3 pictures that could replace words in the TRUE 10X hook
(overlay method), using only screenshots or photos Malthe can take himself.
```

### B. Google Sheets: new columns in the content idea spine

`Hook draft` · `Hook 10x` · `Hook true 10x (final)` · `Audience keyword` · `Proof number` · `Overlay pictures`

The Make.com scenario reads `topic` and `facts`, runs prompt A, and writes the three hooks back into the row. This build is itself a short ("I made Claude write my hooks 10x harder, then made it fact-check itself").

### C. On-screen: `templates/text-hook-overlay.html`

The proof-stack + hook-line overlay from Mino's first frame, rebuilt to brand: proof chips, a two-line hook with one orange keyword, and up to 3 picture slots for the overlay method. Open it in a browser, edit the fields, record it in OBS at 1080×1920, put it on top of the talking-head in CapCut for the first 3–5s. See the file for steps.

### D. Test plan (so this is measured, not assumed)

The video claims "10x your views." Treat that as a hypothesis. Malthe's metrics are **3-second hold** and **completion rate**, not views.

- Next 6 shorts: 3 with the overlay hook + true-10x line, 3 with the current hook style.
- Compare 3-second hold and completion rate in the Sheet. Ignore total views.
- Keep it if the 3-second hold is clearly higher on the overlay ones. Drop it if not. 6 shorts is a small sample, so read it as a direction, not proof.

## 7. Three repurposed hooks (AndersenBuilds, all true as long as the bracketed numbers are real)

1. **Specific identity + number:** "I'm a grocery store apprentice with $1,400 and zero code. Day [X] of building an AI business."
   *Overlay:* proof chips `$1,400 budget` · `Day [X]` · `0 lines of code`.
2. **True 10x:** Draft "I automated my hook writing." → 10x "AI writes all my videos now." (false) → true 10x: "I made Claude rewrite my hooks 10 times harder. Then I made it fact-check itself."
   *Overlay:* screenshot of the Sheet row showing draft → 10x → final.
3. **Overlay method (pictures, few words):** "By day I stack shelves. At night I build this."
   *Overlay:* photo of a grocery shelf next to a screenshot of the Make.com scenario.

## 8. Format replication with the locked stack

- **OBS:** record the talking-head at 1080×1920 vertical. Record `text-hook-overlay.html` as a separate clip.
- **CapCut:** overlay clip on top of the talking-head for 0–5s, starting at frame 1 with no fade-in delay. Auto-captions in 1–3-word cards, lower-middle. Picture-in-picture of your own earlier short (with its real numbers) when you mention it as proof.
- **Voice:** cloned voice for the body is fine. The CTA is a real-voice cut, one ask: the list.
- **Length:** one rule per short, 30–45s. Rule 1, rule 2 and the overlay method = three shorts from this one breakdown.

---

## Appendix: full script (from captions, cleaned)

> The most underrated skill in content right now is mastering text hooks. Text hooks is the reason why I've been able to grow roughly 30,000 followers in the last 2 months on this [account]. And I spent two hours today compiling everything that I know about good text hooks so you guys can actually master it.
>
> Number one is you must always use a specific name or a specific number. Software engineer. Software engineer at Google. So saying I'm 22 years old — that helps you actually know why you should listen to me next.
>
> There is a thought experiment that MrBeast talks about to make the most gripping titles: what would this look like if it was 10 times more extreme? Every time you write your text hook, I want you to write it first. One draft. And then I want you to think to yourself: what is the 10 times most extreme version? For example, I had this video that got a million views of me reading a letter getting kicked out of Boston College to my mom. And the mild version is "POV: reading a letter from college to my mom." The most 10x extreme is "POV: getting kicked out of my house by my mom for becoming a disappointment." Now obviously that didn't happen. My mom still loves me, no worry. So I just said "POV: You became a disappointment to your Korean mom." Keyword: Korean, right. Because that identifies with the Asian crowd. Right? That's important.
>
> Third, and this one's a bonus tip, just because I like you so much because you stayed until 63 seconds into the video: well, I use the overlay method. There's a new type of text hook where instead of using text, you just show pictures to represent these ideas. So let's say, for example, [I] made this video talking about storytelling. I use Hollywood movie posters in the overlay hook, where I put, like, Spider-Man Brand New Day next to the Odyssey poster.
>
> And you combine all of these things — they genuinely take you, like, 5 extra minutes when making every single video, but it's the highest lever that you can pull. That can genuinely 10x your views. Try this out.

On-screen hook text (0–10s): "this takes 5 MINUTES but got me 19K followers last month" over chips 1.6M / 564.6K / 218.9K / 3.8M and a "Net followers 19.3K" card.
