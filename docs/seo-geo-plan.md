# FastCast SEO/GEO Plan

This document describes how FastCast's public download/version-feed repository is optimized for
search engines (SEO) and AI answer engines (GEO, Generative Engine Optimization). It is a planning
and guardrail document. It must never introduce unsupported claims or imply access to the private
source code.

Hard rules for everything in this plan:

- Do not claim FastCast is open source. The release packaging is proprietary.
- Do not claim FastCast is better than OBS or a full OBS replacement.
- Do not claim feature parity with OBS.
- Do not claim scenes, chroma key, plugins, browser sources, multistream, platform OAuth, cloud
  sync, accounts, telemetry, or automatic updates unless the repo/release notes confirm them.
- Do not include fake ratings, reviews, or download counts.
- Do not keyword-stuff. Human-readable, trustworthy copy comes first.

## Product positioning

FastCast is a native Windows screen recorder and live streaming app focused on reliable local
recording, webcam overlay, desktop audio, microphone capture, and custom RTMP/RTMPS streaming.

It is designed for creators, educators, tutorial makers, coaches, and solo streamers who want a
simpler setup than OBS for focused single-scene recording and streaming workflows.

Short positioning: "OBS-level basics without OBS-level setup." Use carefully — never imply a full
OBS replacement.

Safer comparison wording: "FastCast is a simpler OBS alternative for creators who mainly need
single-scene screen recording, webcam overlay, desktop/mic audio, and custom RTMP/RTMPS streaming."

Approved wording:

- "Focused single-scene recording and streaming"
- "Beginner-friendly OBS alternative for basic creator workflows"
- "Designed for reliable local recording"
- "Portable Windows build"
- "Free during open beta"
- "No telemetry, accounts, crash upload, background polling, or auto-update"
- "Manual update check through this public release feed"
- "Hardware H.264 encoding strongly recommended"

Banned wording: "OBS replacement", "Better than OBS", "Professional broadcast suite", "Best screen
recorder", "Zero-latency streaming", "Works on every PC", "Free forever", "Open source",
"Automatic updates", "No setup required".

## Target keyword cluster

- Windows screen recorder
- native Windows screen recorder
- lightweight Windows screen recorder
- simple screen recorder for Windows
- OBS alternative
- beginner-friendly OBS alternative
- simple OBS alternative
- screen recorder with webcam overlay
- screen recorder with desktop audio
- screen recorder with microphone capture
- RTMP streamer for Windows
- RTMPS streamer for Windows
- live streaming app for Windows
- privacy-friendly screen recorder
- screen recorder without telemetry
- portable Windows screen recorder

## GitHub README strategy

The README is structured as a product landing page for GitHub readers, search engines, and AI
answer engines:

- Descriptive H1 title that names the product and category.
- A clear one-sentence definition in the first paragraph (good for AI extraction).
- "FastCast at a glance", "Who FastCast is for", and "Who should still use OBS" sections to set
  honest expectations and capture comparison queries.
- A "FastCast facts" key/value block that AI answer engines can extract directly.
- A "Download" section with the current version, asset names, requirements, SmartScreen note, and
  SHA-256 verification.
- A visible FAQ section (high-value for GEO and featured-snippet style answers).
- Privacy and source-private sections to reinforce trust.

Keep the README version, asset names, and SHA-256 in sync with the latest GitHub release.

## Release-note strategy

Each release note should consistently restate:

- Current version and asset names.
- Free during open beta.
- Private/proprietary source code.
- Privacy stance: no telemetry, accounts, crash upload, background polling, or auto-update.
- Windows requirements (Windows 10 20H1 / 2004+ and Windows 11, x64).
- Hardware H.264 encoder recommendation with software fallback.
- Custom RTMP/RTMPS support.
- Manual Check for Updates behavior (reads this public feed only).

When the README and release notes conflict, align the README to the latest release.

## Future landing page map

If/when there is a dedicated FastCast website, create focused pages:

- `/fastcast/`
- `/fastcast/windows-screen-recorder/`
- `/fastcast/obs-alternative/`
- `/fastcast/rtmp-streaming/`
- `/fastcast/webcam-overlay-screen-recorder/`
- `/fastcast/privacy/`
- `/fastcast/download/`
- `/fastcast/benchmarks/`

Recommended website title:
`FastCast - Native Windows Screen Recorder and Live Streaming App`

Recommended website meta description:
`FastCast is a native Windows screen recorder and live streaming app for local recording, webcam overlay, desktop/mic audio, custom RTMP/RTMPS streaming, and privacy-conscious creator workflows.`

## FAQ / GEO extraction strategy

AI answer engines favor content that directly answers a question in a short, factual way. Keep:

- One clear definition sentence near the top of the README and landing page.
- A question-and-answer FAQ with one focused answer per question.
- A key/value facts block that maps cleanly to attributes (product, platform, price, privacy).
- Consistent terminology across README, landing page, and release notes.

Maintain the FAQ as features ship. Never add an FAQ answer that claims an unshipped feature.

## Privacy / trust messaging

Privacy is a differentiator and must stay accurate to the release notes:

- No telemetry, no accounts, no crash upload, no background polling, no auto-update.
- Stream keys are not saved to disk.
- Support bundles are local-only and redacted.
- The only network activity is streaming to the chosen ingest and the manual Check for Updates,
  which reads this public release feed only.

Do not soften or overstate these. They are trust claims and must remain verifiable.

## Comparison positioning against OBS

Be fair and direct. FastCast is a simpler tool for focused single-scene workflows, not an OBS
replacement. Always pair the "OBS alternative" framing with a "who should still use OBS" section
covering scenes, chroma key, plugins, filters, browser sources, multistreaming, platform OAuth, and
advanced production. This honesty improves trust and is well-suited to AI answer extraction.

## Benchmark / proof requirements

Before publishing any performance or benchmark claim:

- Use real measurements on described hardware (GPU vendor/model, resolution, FPS, encoder).
- State the test conditions.
- Do not publish round-number or aspirational claims.
- Prefer qualitative, supportable statements (e.g., "hardware H.264 tested on NVIDIA and AMD")
  until reproducible benchmark data exists.

## Screenshot / image recommendations

Current asset: `assets/fastcast-gui-v0.3.2.png` (referenced by the landing page with descriptive
alt text). When adding more screenshots, prefer descriptive, keyword-aligned filenames and alt text.

Preferred filenames:

- `fastcast-windows-screen-recorder.png`
- `fastcast-obs-alternative-windows.png`
- `fastcast-webcam-overlay-screen-recorder.png`
- `fastcast-rtmp-streaming-windows.png`
- `fastcast-local-recording-desktop-audio.png`

Preferred alt text:

- `FastCast native Windows screen recorder interface.`
- `FastCast webcam overlay screen recording workflow.`
- `FastCast custom RTMP streaming setup for Windows creators.`
- `FastCast local recording with desktop audio and microphone capture.`

Do not rename or move existing images without updating every reference (`index.html`, social card
meta tags, and any docs that embed them).

## GitHub repository topics

Recommended repository topics for discoverability (set manually in the GitHub repo settings):

- `screen-recorder`
- `windows-screen-recorder`
- `live-streaming`
- `rtmp`
- `rtmps`
- `obs-alternative`
- `creator-tools`
- `video-recording`
- `webcam-overlay`
- `windows`

## Future article ideas

- Building a Native Windows Screen Recorder in Rust
- Why I Built a Simpler OBS Alternative for Windows Creators
- How FastCast Handles Desktop Audio and Microphone Capture
- Local Recording vs Live Streaming: What Creators Actually Need
- Custom RTMP/RTMPS Streaming Without OBS-Level Setup
- Privacy-Friendly Screen Recording: No Telemetry, No Accounts, No Auto-Update
- FastCast vs OBS for Simple Creator Workflows
- How Webcam Picture-in-Picture Helps Tutorial Videos

These article ideas must not reveal private source code internals. Keep them user-facing.

## SoftwareApplication schema (for a future website only)

Add this JSON-LD to the `<head>` of a future FastCast website page. Do not add JSON-LD to the
GitHub README — README markdown is not served as page head metadata and the JSON-LD will not be
parsed as structured data.

```json
{
  "@context": "https://schema.org",
  "@type": "SoftwareApplication",
  "name": "FastCast",
  "applicationCategory": "MultimediaApplication",
  "operatingSystem": "Windows 10, Windows 11",
  "description": "FastCast is a native Windows screen recorder and live streaming app for local recording, webcam overlay, desktop audio, microphone capture, and custom RTMP/RTMPS streaming.",
  "author": {
    "@type": "Person",
    "name": "Calvin Sturm"
  },
  "offers": {
    "@type": "Offer",
    "price": "0",
    "priceCurrency": "USD"
  }
}
```

Schema rules:

- No fake ratings.
- No fake reviews.
- No fake download counts.
- No fake public source repository.
- Do not claim open source.
- If a Pro version or paid tier exists later, update `offers` pricing/status honestly.
