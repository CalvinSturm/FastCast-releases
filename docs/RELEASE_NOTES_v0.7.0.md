# FastCast v0.7.0 — Open Beta

**Multistreaming.** One capture, encoded once, published to up to three RTMP
destinations at the same time. The Stream card is now three configurable
destination rows instead of a single URL field, each with its own platform,
stream key, on/off switch and live status.

Multistreaming is a **FastCast Pro** feature. Free streams to one destination —
and Free now records at **60 fps**, which used to be behind Pro.

## Streaming to more than one place

Encoding is the expensive part of streaming, and FastCast does it **once**. The
finished video and audio packets are handed to one sender per destination, so a
second and third destination cost upload bandwidth, not CPU or GPU.

Each destination runs on its own: its own connection, its own retry timer, its
own drop counter. A platform that goes down, refuses your key or simply
disappears mid-stream cannot stall, slow or disconnect the others — and it
cannot disturb the local recording, which keeps writing regardless of what the
network is doing.

Each row shows what it is actually doing: `live`, `connecting`, `retrying`,
`failed`, or `Off`. When Go Live is not available, the card names the row that
is holding it back and which field is missing, rather than leaving you to guess.

**Upload bandwidth is on you.** Three destinations need roughly three times the
upstream of one. FastCast does not measure your connection and will not warn you
before you saturate it.

## Destination presets

YouTube, Twitch, Kick, TikTok, Facebook, LinkedIn and Custom.

YouTube and Twitch ship with their ingest URL, so those rows need only your
stream key. Kick, TikTok, Facebook and LinkedIn issue **per-account or
per-session endpoints** — there is no single correct URL to hardcode — so those
rows ask for the Server URL from the platform's own dashboard, next to where you
copied the key.

**A preset is an endpoint, not an official integration.** It means FastCast
knows the shape of that platform's ingest, not that the platform has certified
FastCast or that the combination has been tested. Of the seven, only YouTube has
recorded live evidence so far. Platform names and marks identify where *you*
chose to send your stream; see `THIRD_PARTY_NOTICES.md`.

## 60 fps is now free

60 fps moved out of Pro. It is what makes gameplay and tutorial footage look
like itself, so a 30-fps-only free tier read as a broken recorder rather than a
smaller one.

The frame-rate cap now sits at **120 fps**, which stays Pro. The hardware check
is unchanged: a capture path or encoder that cannot sustain 60 still says so,
and says it as a hardware limit rather than an upsell.

## Optional: remember your stream keys

Stream keys have always been session-only — every launch asked again. You can
now opt in to having them remembered, from **Advanced → Remember stream keys**.
It is **off by default**.

When it is on, each destination's key is stored in **Windows Credential
Manager**, encrypted by Windows under your user account, and restored the next
time you launch. Keys never go into `settings.ini`, a log, a diagnostic or a
support bundle.

Turning the toggle off deletes what was stored, immediately — as does removing a
destination, or pointing one at a different platform.

**What this protects, and what it doesn't.** A copied settings folder, a backup,
a folder sync, or another Windows account on the same PC gets nothing. Software
already running as *you* can read the key back, because Windows decrypts it for
your account automatically. That is true of every local credential store,
including your browser's; if you would rather not have keys stored at all, leave
the toggle off.

## Also new

- **A compact recording-countdown editor**, and key controls on every
  destination row.
- **Platform marks on every destination row** — each row shows its platform's
  mark and brand colour, so a three-destination setup is readable at a glance
  instead of by reading three labels. Drawn as vector geometry, sharp at any
  display scaling. `Custom` gets a neutral globe, because it is not a platform
  and should not borrow one's identity.
- **The live preview is cleaner.** The webcam box's red outline and white corner
  grips are editing controls, and the preview is also what your recording looks
  like — so they now appear only while your pointer is over the preview, and
  while you are dragging.
- **Your settings are migrated automatically.** A single stream URL from an
  earlier version becomes destination 1. A YouTube or Twitch URL adopts that
  preset and drops the stored URL, so a future endpoint correction reaches you
  without you editing anything. A Kick URL keeps its URL, because FastCast
  cannot regenerate a per-account endpoint.

## Fixed

- **Go Live could not be clicked on a fresh install.** The button read the old
  Advanced "RTMP URL" field while the click path read the destination list, so
  configuring a destination and pasting its key left the button permanently
  disabled. Every reader now shares one readiness rule.
- **Destination rows could stay locked after a recording or stream ended**,
  leaving no way to remove a destination. The rows freeze during a run by
  design; they now reliably thaw when it finishes.
- **Platform buttons all stayed lit** once each had been pressed. They are
  drawn controls that the app was not repainting when the selection moved, so
  the one that lost the selection kept its lit pixels — going into Advanced and
  back "fixed" it, which was the giveaway. Only the selected platform is lit
  now, and the unselected ones visibly recede.
- **Switching a destination to another platform kept the previous platform's
  stream key** in the box, where it looked valid and could not be. The field now
  clears with the switch.
- **Two contradictory readiness warnings could appear at once.** Each surface
  states it once, in place.
- The compact dashboard's YouTube and Twitch buttons wrote a retired field the
  recorder ignores, so clicking "YouTube" there could leave the stream pointed
  somewhere else.
- A Free user who left destination 1 configured-but-disabled and enabled
  destination 2 silently got **no** destinations at all.
- Removed a bundled Kick ingest URL that could never be correct for anyone —
  Kick issues per-account hosts.
- **Kick setup is fixed end to end**: Kick destinations are normalized onto
  RTMPS, and a dashboard URL pasted without an application path gets `/app`
  appended.
- **A finished recording now appears immediately** instead of after the last
  destination disconnects.

## Privacy

No telemetry, no accounts, no platform logins, no crash upload, no auto-update
and no background polling were added in this release.

Stream keys have exactly one storage location, and only if you ask for it:
Windows Credential Manager, as described above. Nothing else on disk ever
receives one — the persisted destination format has no key field at all, so this
is structural rather than a rule someone has to remember. A key embedded in a
URL is redacted out of warnings, and a malformed URL or key disables only that
destination, naming it without echoing what you typed.

Support bundles remain local-only, redacted, and generated only when you ask.

## Known limitations

- Only YouTube has recorded live evidence among the seven presets.
- Upload bandwidth is not measured, and FastCast will not warn you before three
  destinations exceed your connection.
- The encoded payload is copied once per destination rather than shared.
- Stream teardown can still block behind a destination wedged in a kernel write:
  the publish loop has no write timeout.

## Requirements and install

Windows 10 (20H1 or newer) or Windows 11, 64-bit. Portable ZIP — unzip and run,
no installer, nothing written outside your user profile.

The build is **unsigned**, so SmartScreen shows an "unknown publisher" warning:
choose **More info → Run anyway**.
