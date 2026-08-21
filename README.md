# FastCast - Native Windows Screen Recorder and Live Streaming App

<img width="728" height="790" alt="fastcast_default" src="https://github.com/user-attachments/assets/2f5808e7-c872-45f1-b911-e46dffa07f7f" />

FastCast is a native Windows screen recorder and live streaming app focused on reliable local recording, webcam overlay, desktop audio, microphone capture, and custom RTMP/RTMPS streaming.

It is designed for creators, educators, tutorial makers, coaches, and solo streamers who want a simpler setup than OBS for focused single-scene recording and streaming workflows.

FastCast Free is free during the open beta and records at 1080p60. An optional paid **FastCast Pro** license unlocks 1440p/4K recording, 120 fps, and multistreaming to up to three platforms at once. This public repository provides release downloads and version metadata only. The FastCast source code is private.

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
- A portable app with no installer
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
- **Price:** FastCast Free is free during the open beta; FastCast Pro is an optional paid license (Gumroad; keys from the previous Lemon Squeezy store still work)
- **Source code:** Private
- **Distribution:** Portable ZIP release
- **Primary use:** Local screen recording and custom RTMP/RTMPS streaming
- **Main benefits:** Simple setup, local recording, webcam overlay, desktop audio, microphone capture, custom streaming, privacy-conscious design
- **Privacy:** No telemetry, no accounts, no crash upload, no background polling, no auto-update
- **Best for:** Creators, tutorial makers, educators, coaches, and solo streamers who want a focused Windows recording/streaming tool
- **Not designed for:** Full OBS replacement, complex scene production, plugin workflows, multistreaming, or platform OAuth

## Download FastCast for Windows

Download the latest FastCast Open Beta ZIP from the **[Releases](https://github.com/CalvinSturm/FastCast-releases/releases)** page.

Latest release: **[v0.7.0](https://github.com/CalvinSturm/FastCast-releases/releases/tag/v0.7.0)** (Open Beta)

- `FastCast-0.7.0-win-x64.zip` — portable build. Extract and run `fastcast.exe`.
- `FastCast-0.7.0-win-x64.zip.sha256` — checksum for verifying the download.

### Requirements

- Windows 10 20H1 / 2004+ or Windows 11
- x64 system
- GPU with hardware H.264 encoding strongly recommended
- Software encoding fallback is included but slower

### SmartScreen note

The current Open Beta build is unsigned, so Windows SmartScreen may show an "Unknown publisher" warning. Click **More info → Run anyway** only if you trust the download source.

### Verify the download

The release includes a `.sha256` file so you can verify the ZIP was not corrupted or modified.

Expected SHA-256 for `FastCast-0.7.0-win-x64.zip`:

```text
7eb28611347c32691819b7dc7d49f02947a2d2713f1aa22cb8246f9daaf56241
```

Verify in PowerShell:

```powershell
Get-FileHash .\FastCast-0.7.0-win-x64.zip -Algorithm SHA256
```

The printed hash should match the value above.

## What's new in v0.7.0

**Stream to three places at once.** One capture is encoded once and published to up to three RTMP destinations at the same time — so a second and third platform cost upload bandwidth, not CPU or GPU. Each destination connects, retries and fails on its own, so one platform dropping out cannot disturb the others or your local recording. Multistreaming is FastCast Pro; Free streams to one destination.

**Destination presets** for YouTube, Twitch, Kick, TikTok, Facebook, LinkedIn and Custom. YouTube and Twitch fill in their ingest server for you; the others issue per-account endpoints, so those rows ask for the Server URL from the platform's own dashboard. A preset is an endpoint, not an official integration.

**60 fps recording is now free.** It used to be a Pro feature. The frame-rate cap is now 120 fps, which stays Pro.

**Remember stream keys, if you want to.** Off by default. Turn it on in Advanced and each destination's key is stored in Windows Credential Manager — encrypted under your Windows account, restored next launch, and deleted the moment you turn the toggle back off. Keys are never written to settings, logs, diagnostics or support bundles.

Plus a cleaner live preview: the webcam box's outline and corner grips now appear only when your pointer is over the preview, instead of sitting over the shot the whole time.

[Full release notes](docs/RELEASE_NOTES_v0.7.0.md)

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

FastCast Pro is an optional paid license, activated inside the app. Pro unlocks higher-resolution recording (1440p / 4K), 120 fps capture where your capture and encoder hardware support them, multistreaming to up to three destinations, and advanced encoder controls.

License activation is user-initiated and local-first: no accounts, no telemetry. The license key is sent only to the license endpoint of the store that issued it when you click Activate, is stored redacted on your machine, and a limited offline grace period covers previously-activated devices that go offline.

## FAQ

### What is FastCast?

FastCast is a native Windows screen recorder and live streaming app for local recording, webcam overlay, desktop audio, microphone capture, and custom RTMP/RTMPS streaming.

### Is FastCast an OBS alternative?

FastCast can be used as a simpler OBS alternative for creators who mainly need single-scene screen recording, webcam overlay, desktop/mic audio, and custom RTMP/RTMPS streaming. OBS is still better for complex scenes, plugins, browser sources, multistreaming, and advanced broadcast workflows.

### Is FastCast free?

FastCast Free is free during the open beta and covers simple 1080p60 recording and streaming. FastCast Pro is an optional paid license that unlocks 1440p/4K recording, 120 fps capture where hardware supports it, multistreaming to up to three destinations, and advanced encoder controls.

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

This repository is for public release downloads and version metadata only. FastCast ships a proprietary `LICENSE.txt` and a `THIRD_PARTY_NOTICES.txt` inside the release ZIP.

## GitHub Pages

This repository includes a static GitHub Pages landing page in `index.html`.

See [`docs/GITHUB_PAGES.md`](docs/GITHUB_PAGES.md) for setup instructions.
