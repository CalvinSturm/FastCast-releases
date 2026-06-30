# FastCast Releases

Public downloads and version feed for FastCast.

FastCast is a native Windows screen recorder and live streamer for local recording and custom RTMP/RTMPS streaming.

## Download

Download the latest ZIP from the **Releases** page:

- `FastCast-0.3.2-win-x64.zip`
- `FastCast-0.3.2-win-x64.zip.sha256`

Extract the ZIP and run `fastcast.exe`.

FastCast targets Windows 10 20H1 / 2004+ and Windows 11, x64.

A GPU with hardware H.264 encoding is strongly recommended. A software encoder is included as a fallback, but it is much slower.

## SmartScreen note

The Open Beta build is currently unsigned, so Windows SmartScreen may show an "Unknown publisher" warning.

Click **More info → Run anyway** if you trust the download source.

## Verify the download

The release includes a `.sha256` file so you can verify the ZIP was not corrupted or modified.

Expected SHA-256 for `FastCast-0.3.2-win-x64.zip`:

```text
fb48f1edc0798753f8a06a2c5aca5ccf39f135b4ba4da38d20e1b7386542a29e
```

## Open Beta status

FastCast is currently free during open beta.

A Pro version may be added later for advanced creator features, but there is no Pro tier, license, or account system today.

## Privacy

FastCast does not include telemetry, accounts, crash upload, background polling, or automatic updates.

The in-app **Check for Updates** action only checks this public release feed. It does not download or install updates.

Stream keys are not saved to disk.

Support bundles are created only when you click **Save Support Bundle**. They are saved locally and redacted before being written.

## Reporting issues

If something breaks, click **Save Support Bundle** in FastCast and send the generated ZIP with a short description of what happened.

## Source code

FastCast source code is private.

This repository is for public release downloads and version metadata only.

## GitHub Pages

This repository includes a static GitHub Pages landing page in `index.html`.

See `docs/GITHUB_PAGES.md` for setup instructions.
