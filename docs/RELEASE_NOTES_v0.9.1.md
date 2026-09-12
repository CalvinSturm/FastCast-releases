# FastCast v0.9.1 — Open Beta

**Go Live works again, and the Stream card tells you what goes where.**

This is a fixes-only hotfix for v0.9.0. Recording, Instant Replay, audio and
encoding are unchanged. If you stream from a destination row (YouTube, Twitch,
Kick, TikTok, Facebook, LinkedIn or Custom), install this update.

## Go Live with a destination row

In v0.9.0, going live from a destination row stopped before FastCast ever tried
to connect. The row showed **Ready**, but pressing **Go live** ended with:

> add a Stream URL in the Stream card to go live

The cause was a last check before a run starts. It still looked at the old
single "RTMP URL" and "Stream key" fields under Advanced, which predate
destination rows and which a destination row never fills in. A correctly set-up
row could therefore never pass it.

That check now looks at the destinations the stream will actually go to: rows
that are switched on, within your plan's destination limit, with both a server
URL and a stream key. The old single-URL setup under Advanced still works if you
use it.

When Go Live is refused for this reason, the reason is now also written to
`fastcast.log`. Before, nothing was logged, so a support bundle couldn't tell a
stream that never started from one that was never attempted. The logged message
names no URL, stream key, or destination name.

## Destination fields say what goes in them

Every text box on a destination row now shows what belongs in it:

- The **stream key** box reads *Stream key* when empty.
- The **name** box on a YouTube or Twitch row reads *Name (optional)*.
- The **server URL** box on Kick, TikTok, Facebook, LinkedIn and Custom rows
  names where to find the address, for example *Server URL from your Kick
  dashboard*.

Hover over any of these boxes for a one-line tip about what goes there. On the
compact card, the fixed address YouTube and Twitch use is now labelled
**Server:** so it reads as information rather than something to copy.

These hints were meant to be there in v0.9.0, but they were drawn behind the text
boxes and never showed. On a YouTube row that left a blank name box right beside
the server address, and it was easy to paste the address into it. If you did
that, the row still works. Clear the name box, or give it a real name, to tidy
it up.

## Upgrading

Install the v0.9.1 MSI over v0.9.0. Your settings, destinations and remembered
stream keys are kept. Close FastCast first, or let the installer close it when
it asks.

The portable ZIP is extract-and-run, as before. Replace your old `fastcast.exe`
with the new one, because an older copy left elsewhere, such as on the desktop,
will not be updated.

## Requirements

Windows 10 (20H1 or newer) or Windows 11, 64-bit. A GPU with hardware H.264
encoding (NVIDIA, AMD or Intel) is strongly recommended.

The build is unsigned, so SmartScreen shows "unknown publisher". Choose
**More info → Run anyway**.

No telemetry, no account, no auto-update.
