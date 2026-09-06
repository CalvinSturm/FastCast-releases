# <img width="36" alt="ChatGPT Image Aug 26, 2026, 07_32_37 PM" src="https://github.com/user-attachments/assets/6cbec981-2b77-4532-ae89-0c27382270d7" /> FastCast

Native Windows Screen Recorder and Live Streaming App

It is designed for creators, educators, tutorial makers, coaches, and solo streamers who want a simpler setup than OBS for focused single-scene recording and streaming workflows.

FastCast Free is free during the open beta and records at 1080p60. An optional paid **FastCast Pro** license unlocks 1440p/4K recording, 120 fps, and multistreaming to up to three platforms at once. This public repository provides release downloads and version metadata only. The FastCast source code is private.

**[Download FastCast v0.8.0 for Windows x64 (MSI installer)](https://github.com/CalvinSturm/FastCast-releases/releases/download/v0.8.0/FastCast-0.8.0-win-x64.msi)**

[Portable ZIP](https://github.com/CalvinSturm/FastCast-releases/releases/download/v0.8.0/FastCast-0.8.0-win-x64.zip)

<img width="730" height="792" alt="1" src="https://github.com/user-attachments/assets/adf5595c-836a-4b3a-8020-6f13479e8926" />


## FastCast at a glance

FastCast is a native Windows screen recorder and live streaming app.

It is built for:

- Local MP4 recording
- Desktop audio capture
- Microphone capture
- Webcam picture-in-picture overlay
- Custom RTMP/RTMPS streaming through stream keys
- Multistreaming to up to three platforms from one capture (Pro)
- Manual update checks through this public release feed
- Privacy-conscious creator workflows without telemetry or accounts

FastCast is not trying to replace every OBS feature. It is focused on a simpler, single-scene recording and streaming experience for Windows creators.

## Who FastCast is for

FastCast is a good fit if you want:

- A simple Windows screen recorder
- A lightweight OBS alternative for basic creator workflows
- Local recording with desktop and microphone audio
- Webcam picture-in-picture overlay
- Custom RTMP/RTMPS live streaming
- A per-user MSI installer or portable ZIP
- A privacy-conscious recorder with no telemetry or accounts
- A focused single-scene workflow instead of a full broadcast studio

## Who should still use OBS

OBS is still better if you need:

- Multiple scenes and complex scene switching
- Plugin ecosystems
- Advanced filters
- Browser sources
- Platform OAuth workflows
- Studio/broadcast production workflows
- Deep troubleshooting and advanced capture configuration

FastCast is for users who want a simpler local recording and custom RTMP/RTMPS streaming workflow on Windows.

## FastCast facts

- **Product:** FastCast
- **Developer:** Calvin Sturm
- **Category:** Windows screen recorder and live streaming app
- **Platform:** Windows 10 20H1 / 2004+ and Windows 11, x64
- **Current status:** Open beta
- **Price:** FastCast Free is free during the open beta; FastCast Pro is pay what you want, $0 or more (Gumroad; keys from the previous Lemon Squeezy store still work)
- **Source code:** Private
- **Distribution:** Per-user MSI installer and portable ZIP
- **Primary use:** Local screen recording and custom RTMP/RTMPS streaming
- **Main benefits:** Simple setup, local recording, webcam overlay, desktop audio, microphone capture, custom streaming, privacy-conscious design
- **Privacy:** No telemetry, no accounts, no crash upload, no background polling, no auto-update
- **Best for:** Creators, tutorial makers, educators, coaches, and solo streamers who want a focused Windows recording/streaming tool
- **Not designed for:** Full OBS replacement, complex scene production, plugin workflows, multistreaming, or platform OAuth

## Download FastCast for Windows

Download the latest FastCast Open Beta MSI or portable ZIP from the **[Releases](https://github.com/CalvinSturm/FastCast-releases/releases)** page.

Latest release: **[v0.7.1](https://github.com/CalvinSturm/FastCast-releases/releases/tag/v0.7.1)** (Open Beta)

- `FastCast-0.7.1-win-x64.msi` — recommended per-user installer; no administrator prompt.
- `FastCast-0.7.1-win-x64.msi.sha256` — MSI checksum.
- `FastCast-0.7.1-win-x64.zip` — portable build. Extract and run `fastcast.exe`.
- `FastCast-0.7.1-win-x64.zip.sha256` — portable ZIP checksum.

The published packages have a maintainer-confirmed manual smoke pass on Windows
(v0.7.1, August 28, 2026).

### Requirements

- Windows 10 20H1 / 2004+ or Windows 11
- x64 system
- GPU with hardware H.264 encoding strongly recommended
- Software encoding fallback is included but slower

### SmartScreen note

The current Open Beta build is unsigned, so Windows SmartScreen may show an "Unknown publisher" warning. Click **More info → Run anyway** only if you trust the download source.

### Verify the download

Each release package includes a `.sha256` sidecar so you can verify it was not corrupted or modified.

Expected SHA-256 values:

```text
MSI: 8e1d44847871f7a48710c27da3cc89124d30ec28f68c7a41d06b3738a354d775
ZIP: b5f7ec0dddb7c495a4e921786737e72a7dd5a7a7555d2b627c595ac513b75f8e
```

Verify in PowerShell:

```powershell
Get-FileHash .\FastCast-0.7.1-win-x64.msi -Algorithm SHA256
# or: Get-FileHash .\FastCast-0.7.1-win-x64.zip -Algorithm SHA256
```

The printed hash should match the corresponding value above.

## What's new in v0.7.1

**Stop is instant now.** However long you recorded, pressing Stop hands the app straight back to you. The file finishes writing on its own row in Recent files while you get on with the next take. Recordings are stitched together as they run rather than remuxed in one go at the end, so Stop no longer grows with the length of the take — 36 seconds of content went from 436 ms to 29 ms on the development machine, and it no longer scales with recording length at all.

**The app returns to idle while a take is still saving.** Stop used to freeze the whole window until the file was written and validated. Now the moment your screen, microphone and camera are released, the window comes back and the take finishes on its own Recent files row.

**Fixed: a finished recording could get stuck showing "Saving…".** The file was complete and playable, but the Recent card was never repainted.

**Fixed: apps and displays opened after FastCast started never appeared in Sources.** The lists were built once at startup and only the Refresh button rebuilt them — which the simple view does not show, so restarting was the only way to pick up a newly opened app. Every Sources picker now re-scans as you open it, and connecting or disconnecting a monitor updates the Screen list on its own.

Nothing about capture, encoding, audio or streaming changed: v0.7.1 records exactly what v0.7.0 recorded.

[Full release notes](docs/RELEASE_NOTES_v0.7.1.md)

## Command-line recording control (new in v0.5.1)

FastCast v0.5.1 adds command-line start/stop control of a running FastCast
window — useful for scripts, Stream Deck buttons, and schedulers:

```powershell
fastcastc --start-record              # start recording
fastcastc --start-record --monitor 2  # record display 2 first
fastcastc --stop-record               # stop the active recording
```

How it behaves:

- The commands control an **already-running** FastCast window and trigger the
  same guarded Start/Stop action as the button and the Ctrl+Alt+F9 hotkey, so
  a recording can never be double-started or stopped when idle. FastCast is
  never launched automatically: if it is not running, the command says so and
  exits nonzero.
- `--monitor N` records display N (the "Display N" entries of the app's
  Screen list). The choice sticks like a manual selection, replaces any
  window-capture selection, and an unknown display number is rejected.
- Exit codes are script-friendly: `0` for success and for harmless no-ops
  (already recording / nothing to stop), nonzero for failures (FastCast not
  running, start failed, unknown display). Output is plain text with no log
  noise.
- The release ZIP includes `fastcastc.exe` next to `fastcast.exe`. Use
  `fastcastc` from scripts and shells: it waits for the command and exits
  with its exit code. `fastcast.exe` accepts the same flags, but as a GUI app
  the shell does not wait for it.
- Like everything else in FastCast, this is local-only: no background
  service, no polling, no network.

## Privacy

FastCast does not include telemetry, accounts, crash upload, background polling, or automatic updates.

The in-app **Check for Updates** action only checks this public release feed. It does not download or install updates.

Stream keys are not saved to disk.

Support bundles are created only when you click **Save Support Bundle**. They are saved locally and redacted before being written.

## Free and Pro

FastCast Free remains free during the open beta and covers simple 1080p60 recording and streaming: monitor/window capture, microphone and desktop audio, webcam overlay, custom RTMP/RTMPS streaming, and local redacted support bundles.

FastCast Pro is pay what you want: enter $0 at checkout for a free license key, or pay any amount you like to support development. It is activated inside the app. Pro unlocks higher-resolution recording (1440p / 4K), 120 fps capture where your capture and encoder hardware support them, multistreaming to up to three destinations, and advanced encoder controls.

License activation is user-initiated and local-first: no accounts, no telemetry. The license key is sent only to the license endpoint of the store that issued it when you click Activate, is stored redacted on your machine, and a limited offline grace period covers previously-activated devices that go offline.

## FAQ

### What is FastCast?

FastCast is a native Windows screen recorder and live streaming app for local recording, webcam overlay, desktop audio, microphone capture, and custom RTMP/RTMPS streaming.

### Is FastCast an OBS alternative?

FastCast can be used as a simpler OBS alternative for creators who mainly need single-scene screen recording, webcam overlay, desktop/mic audio, and custom RTMP/RTMPS streaming. OBS is still better for complex scenes, plugins, browser sources, multistreaming, and advanced broadcast workflows.

### Is FastCast free?

FastCast Free is free during the open beta and covers simple 1080p60 recording and streaming. FastCast Pro is pay what you want: enter $0 at checkout for a free license key, or pay any amount you like to support development. Pro unlocks 1440p/4K recording, 120 fps capture where hardware supports it, multistreaming to up to three destinations, and advanced encoder controls.

### Does FastCast Pro require an account?

No. FastCast Pro is a license key you paste into the app. There are no accounts; activation is user-initiated, the key is stored redacted on your machine, and a limited offline grace period covers activated devices that go offline.

### Is FastCast open source?

No. FastCast source code is private. This public repository provides release downloads and version metadata only.

### Does FastCast collect telemetry?

No. FastCast does not include telemetry, accounts, crash upload, background polling, or automatic updates.

### Does FastCast save stream keys?

No. Stream keys are not saved to disk.

### What platforms does FastCast support?

FastCast targets Windows 10 20H1 / 2004+ and Windows 11 on x64 systems.

### Does FastCast support RTMP and RTMPS streaming?

Yes. FastCast supports custom RTMP/RTMPS streaming.

### Can I start and stop recording from the command line?

Yes, since v0.5.1. `fastcastc --start-record` and `fastcastc --stop-record` control a running FastCast window with script-friendly exit codes, and `--monitor N` picks which display to record. FastCast is never auto-launched and nothing runs in the background. See "Command-line recording control" above.

### Does FastCast replace OBS?

No. FastCast is a focused single-scene recorder and streamer. OBS remains better for advanced production workflows.

## Reporting issues

If something breaks, click **Save Support Bundle** in FastCast and send the generated ZIP with a short description of what happened.

## Source code

FastCast source code is private and proprietary.

This repository is for public release downloads and version metadata only. FastCast ships a proprietary `LICENSE.txt` and a `THIRD_PARTY_NOTICES.txt` inside both release packages.

## GitHub Pages

This repository includes a static GitHub Pages landing page in `index.html`.

See [`docs/GITHUB_PAGES.md`](docs/GITHUB_PAGES.md) for setup instructions.
