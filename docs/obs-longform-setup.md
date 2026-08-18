# OBS setup for 1080p long-form YouTube

Settings for horizontal 1080p long-form on a Windows laptop with integrated graphics, recording screen plus a webcam overlay.

> **Unverified.** This was researched from a cloud container with no access to the actual machine. The reasoning is sound and the numbers come from YouTube's published specs, but nothing here was tested on the hardware it's written for. Expect to adjust.

- 2026-08-16 — First version.

---

## 1. Don't disturb the shorts setup

The existing vertical 1080×1920 setup stays untouched. Long-form gets its own.

Two things must be created, not one:

- **Profile** — holds resolution, encoder, bitrate, output settings. `Profile → New`, name it `YouTube Long-form`.
- **Scene Collection** — holds sources and layout. `Scene Collection → New`, name it `YouTube Long-form` too.

**The trap:** profiles and scene collections switch independently. Switching the profile alone leaves the vertical layout sitting on a horizontal canvas, with sources in the wrong places and black bars. Give both the same name so a mismatch is obvious in the title bar, and switch both every time.

## 2. Video settings

`Settings → Video`

| Setting | Value |
|---|---|
| Base (Canvas) Resolution | Your native display resolution |
| Output (Scaled) Resolution | `1920x1080` |
| Downscale Filter | Lanczos |
| FPS | `30` |

Check your native resolution in Windows: `Settings → System → Display → Display resolution`.

If it's already 1920×1080, set base and output both to that. Nothing gets scaled and the result is as sharp as possible — the downscale filter is irrelevant.

If it's higher (1440p, 4K), leave base at native and let it scale down to 1080p. Lanczos is the sharpest option and matters most for small text in screen recordings.

**Why 30fps and not 60.** Most guides say 60. They assume a dedicated GPU. Integrated graphics running screen capture, a webcam decode, and video encoding at the same time will drop frames at 60fps. 30 halves the encoding load, halves the file size, and looks fine for tool demos and walkthroughs — there's no fast motion to smooth out. Only revisit this if you add gameplay or fast camera movement.

## 3. Encoder

`Settings → Output → Output Mode: Advanced → Recording tab`

Check the Encoder dropdown and take the first of these that appears:

**QuickSync H.264** (Intel integrated graphics) or **AMD HW H.264 / AVC** (AMD integrated):

| Setting | Value |
|---|---|
| Rate Control | CQP |
| CQ Level | `20` |
| Keyframe Interval | `2` |
| Profile | high |

**x264** (if neither hardware option is listed):

| Setting | Value |
|---|---|
| Rate Control | CRF |
| CRF | `20` |
| Keyframe Interval | `2` |
| CPU Usage Preset | `veryfast` |
| Profile | high |

Hardware encoders offload work from the CPU but produce lower quality per bitrate than x264 — that's why CQP 20 is set generously rather than at the usual 23.

x264 runs entirely on the CPU, which means fans. If the mic picks up fan noise, that's the cause; switching to a hardware encoder if available fixes it, or record voiceover separately.

## 4. Recording format

`Settings → Output → Recording`

| Setting | Value |
|---|---|
| Recording Format | `mkv` |
| Audio Track | 1 |

**Record MKV, not MP4.** If OBS or the laptop crashes 35 minutes into a take, an MP4 is unplayable — the index is written at the end of the file. MKV survives and plays up to the crash point. This matters far more for long-form than shorts.

CapCut may not accept MKV. Convert after each recording: `File → Remux Recordings`, drag the file in, hit Remux. It's a container swap, not a re-encode, so it takes seconds and loses nothing.

## 5. Why the recording is higher quality than the upload

Three encodes happen between OBS and a viewer:

```
OBS records  →  CapCut re-encodes on export  →  YouTube re-encodes on upload
```

Each pass loses quality. Recording at exactly YouTube's recommended bitrate means arriving degraded twice over. So record well above target, and let quality drain across the chain instead of starting at the floor.

| Stage | Target |
|---|---|
| OBS recording | CQP/CRF 20 (quality-based, no fixed bitrate) |
| CapCut export | 12–16 Mbps, H.264, MP4 |
| YouTube's recommendation for 1080p30 | 8 Mbps |

Exporting from CapCut above YouTube's number is deliberate — it leaves headroom for YouTube's own re-encode.

## 6. Audio

`Settings → Audio`

| Setting | Value |
|---|---|
| Sample Rate | `48 kHz` |
| Channels | Stereo |

`Settings → Output → Recording → Audio Encoder`: AAC, bitrate `192`.

**48 kHz is not optional.** If OBS records at 44.1 kHz while your mic runs at 48 kHz, audio drifts out of sync progressively — fine for the first minute, visibly off by minute twenty. It's a long-form-specific failure that shorts never expose. Make sure Windows agrees: `Sound settings → your mic → Properties → Format`, set to 48000 Hz.

## 7. Sources

In the Long-form scene collection, add in this order (top of the list renders in front):

1. **Video Capture Device** — your webcam
2. **Display Capture** — your screen
3. **Audio Input Capture** — your mic, if recording live narration

**Set the webcam to 720p30**, not 1080p60, in its properties. It ends up scaled into a corner at roughly a quarter width, so the extra resolution is invisible on screen but costs real decode headroom you don't have. Resize it by dragging with Alt held to crop, or plain drag from a corner to scale.

If Display Capture shows a black screen, that's a known integrated-graphics quirk — right-click the source, `Properties`, and try a different Capture Method.

## 8. Test before committing to a take

Do this once after setup, and again any time you change encoder settings.

1. Record two minutes of whatever you'd normally record, including moving windows around.
2. `View → Stats`.
3. Check **Frames missed due to rendering lag** and **Skipped frames due to encoding lag**. Both should be `0`.

If either is climbing:

- On x264, move the preset from `veryfast` to `superfast`
- Set the webcam to 480p, or remove it and film it separately
- Close Chrome tabs — they compete for the same integrated GPU
- Last resort, drop output to 1600×900; still far better than a stuttering 1080p

Then watch the two minutes back at full screen and check that small text is readable. If it isn't, the problem is scaling, not bitrate — recheck the base resolution in step 2.

---

## Sources

- [YouTube recommended upload encoding settings](https://support.google.com/youtube/answer/1722171?hl=en)
- [OBS Profiles documentation](https://obsproject.com/kb/profiles)
- [OBS forum — QuickSync on integrated graphics](https://obsproject.com/forum/threads/how-does-encoding-with-a-separate-gpu-intel-igpu-work-in-obs.93867/)
- [OBS forum — separate profiles for vertical and horizontal](https://obsproject.com/forum/threads/is-there-a-way-to-switch-from-horizontal-to-portrait-scenes-from-obs.174079/)
