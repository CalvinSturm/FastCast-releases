# FastCast - Native Windows Screen Recorder and Live Streaming App

FastCast is a native Windows screen recorder and live streaming app focused on reliable local recording, webcam overlay, desktop audio, microphone capture, and custom RTMP/RTMPS streaming.

It is designed for creators, educators, tutorial makers, coaches, and solo streamers who want a simpler setup than OBS for focused single-scene recording and streaming workflows.

FastCast is currently free during open beta. This public repository provides release downloads and version metadata only. The FastCast source code is private.

## FastCast at a glance

FastCast is a native Windows screen recorder and live streaming app.

It is built for:

- Local MP4 recording
- Desktop audio capture
- Microphone capture
- Webcam picture-in-picture overlay
- Custom RTMP/RTMPS streaming through stream keys
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
- Chroma key
- Plugin ecosystems
- Advanced filters
- Browser sources
- Multistreaming
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
- **Price:** Free during open beta
- **Source code:** Private
- **Distribution:** Portable ZIP release
- **Primary use:** Local screen recording and custom RTMP/RTMPS streaming
- **Main benefits:** Simple setup, local recording, webcam overlay, desktop audio, microphone capture, custom streaming, privacy-conscious design
- **Privacy:** No telemetry, no accounts, no crash upload, no background polling, no auto-update
- **Best for:** Creators, tutorial makers, educators, coaches, and solo streamers who want a focused Windows recording/streaming tool
- **Not designed for:** Full OBS replacement, complex scene production, plugin workflows, chroma key, multistreaming, or platform OAuth

## Download FastCast for Windows

Download the latest FastCast Open Beta ZIP from the **[Releases](https://github.com/CalvinSturm/FastCast-releases/releases)** page.

Latest release: **[v0.3.3](https://github.com/CalvinSturm/FastCast-releases/releases/tag/v0.3.3)** (Open Beta)

- `FastCast-0.3.3-win-x64.zip` — portable build. Extract and run `fastcast.exe`.
- `FastCast-0.3.3-win-x64.zip.sha256` — checksum for verifying the download.

### Requirements

- Windows 10 20H1 / 2004+ or Windows 11
- x64 system
- GPU with hardware H.264 encoding strongly recommended
- Software encoding fallback is included but slower

### SmartScreen note

The current Open Beta build is unsigned, so Windows SmartScreen may show an "Unknown publisher" warning. Click **More info → Run anyway** only if you trust the download source.

### Verify the download

The release includes a `.sha256` file so you can verify the ZIP was not corrupted or modified.

Expected SHA-256 for `FastCast-0.3.3-win-x64.zip`:

```text
3fa131022b93ab8250df74890e8091c12c3de558d1b93f53d2a10a50373eb4c7
```

Verify in PowerShell:

```powershell
Get-FileHash .\FastCast-0.3.3-win-x64.zip -Algorithm SHA256
```

The printed hash should match the value above.

## Privacy

FastCast does not include telemetry, accounts, crash upload, background polling, or automatic updates.

The in-app **Check for Updates** action only checks this public release feed. It does not download or install updates.

Stream keys are not saved to disk.

Support bundles are created only when you click **Save Support Bundle**. They are saved locally and redacted before being written.

## Open Beta status

FastCast is currently free during open beta.

A Pro version may be added later for advanced creator features, but there is no Pro tier, license, or account system today.

## FAQ

### What is FastCast?

FastCast is a native Windows screen recorder and live streaming app for local recording, webcam overlay, desktop audio, microphone capture, and custom RTMP/RTMPS streaming.

### Is FastCast an OBS alternative?

FastCast can be used as a simpler OBS alternative for creators who mainly need single-scene screen recording, webcam overlay, desktop/mic audio, and custom RTMP/RTMPS streaming. OBS is still better for complex scenes, plugins, chroma key, browser sources, multistreaming, and advanced broadcast workflows.

### Is FastCast free?

FastCast is currently free during open beta. A Pro version may be added later for advanced creator features, but nothing is gated today unless current release notes say otherwise.

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

### Does FastCast replace OBS?

No. FastCast is a focused single-scene recorder and streamer. OBS remains better for advanced production workflows.

## Reporting issues

If something breaks, click **Save Support Bundle** in FastCast and send the generated ZIP with a short description of what happened.

## Source code

FastCast source code is private and proprietary.

This repository is for public release downloads and version metadata only. FastCast v0.3.3 ships a proprietary `LICENSE.txt` and a `THIRD_PARTY_NOTICES.txt` inside the release ZIP.

## GitHub Pages

This repository includes a static GitHub Pages landing page in `index.html`.

See [`docs/GITHUB_PAGES.md`](docs/GITHUB_PAGES.md) for setup instructions.
