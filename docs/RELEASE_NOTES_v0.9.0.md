# FastCast v0.9.0 — Open Beta

**Know which channel you're streaming to, and keep exactly as much footage as
you want.** This release is about the two places FastCast made you work things
out for yourself: a destination row that could not tell you *which* YouTube
channel it was, and a Replay buffer that offered four lengths and no others.

This is a feature release. Recording, streaming, audio and encoding behave as
they did in v0.8.0; what is new sits alongside them.

## Name your destinations

A destination on YouTube or Twitch can now be given a name — "Main channel",
"Gaming channel", "Client work" — typed into a field on its row. The row's chip
shows that name in place of the platform's, while the platform mark beside it
stays put, so you can tell two YouTube rows apart at a glance.

This matters more than it sounds. FastCast has always stored stream keys *per
destination* rather than per platform, so three YouTube rows with three
different keys already worked — they just both said "YouTube" and left you
counting rows to work out which was which.

Nothing changes for a destination you have already set up: an unnamed one shows
its platform name exactly as before, and its URL, key and on/off state are
untouched. A row that needs its own Server URL (Kick, TikTok, Facebook,
LinkedIn, Custom) keeps that field and is told apart by the URL it carries.

## Find your stream key without hunting for it

Each destination row now carries a **Get key ↗** link that opens the platform's
own stream-key page in your browser. YouTube, Twitch, Kick and Facebook have
one. Copy the key there, come back, and the row's paste button fills the field.

TikTok and LinkedIn deliberately have no link: TikTok issues a Server URL per
LIVE session and LinkedIn per eligible event, so there is no single page that
would be right for everyone — and a link that is right for some people and
wrong for others is worse than none.

FastCast sends nothing when you click it. There is no account, no sign-in from
inside the app, and the key is never read back — the link opens a public
dashboard page, and what happens there is between you and the platform.

## Custom Instant Replay lengths (Pro)

The Replay length picker gains a **Custom…** entry. Choose it and type any
length from **15 seconds to 5 minutes** instead of picking one of the presets.
Your value is remembered between sessions, and the picker names it
(`Custom · 90s`) so it is obvious which entry is active. Changing the length
restarts a running buffer exactly as switching presets already did.

**Instant Replay itself is free, and stays free** — the buffer, `Ctrl+Alt+F8`,
the tray controls, and all four lengths it shipped with (30 seconds, 1, 2 and
5 minutes). Nothing has been taken away from anyone. What Pro adds is choosing a
length that is not one of those four.

On Free, picking **Custom…** tells you what it costs and leaves your current
length exactly as it was.

## Pricing: the Founding Supporter Sale

FastCast Pro is now **pay what you think it's worth, from $1**, with **$29
suggested**. The $1 floor is a promotional entry price for early supporters
rather than what Pro is worth long-term, and every purchase funds continued
development.

The compact dock's link reads **Get Pro from $1 ↗** to match. Pro is unchanged
as a tier: 1440p/4K, 120 fps, multistreaming, advanced encoder controls,
chroma-key tuning, and now custom Replay lengths.

## A cleaner interface

Cleaner interface — simpler destination setup, clearer licensing controls, more
room for device names, and less duplicate UI. No layout, style or workflow
changes: the same cards, buttons and spacing, with the parts that read as
unfinished cleaned up.

## Free and Pro

| | Free | Pro |
|---|---|---|
| Recording and streaming | 1080p, up to 60 fps | adds 1440p / 4K and up to 120 fps, where your hardware supports them |
| Streaming destinations | one live at a time | up to three at once, from one encode |
| Instant Replay | yes — 30 s, 1, 2, 5 min | adds any custom length, 15 s – 5 min |
| Chroma key | one-click, auto-picked colour | adds manual colour and the tuning sliders |
| Encoder controls | automatic | adds manual encoder selection |
| Everything else | destination names, Get key links, webcam overlay, tray + Instant Replay hotkeys, support bundles | same |

Hardware still has the final say: 4K and 120 fps need a capture and encoder path
that supports them, whatever your licence says.

## Upgrading

Settings migrate automatically (schema v9 → v11). An existing Replay length
keeps the exact value it had, existing destinations keep their URLs, keys and
on/off state, and nothing needs reconfiguring.

A settings file written by v0.9.0 that holds a *custom* Replay length will be
snapped back to the nearest preset if it is opened by v0.8.0 — a graceful
downgrade, not a corruption.

## Requirements

Windows 10 (20H1 or newer) or Windows 11, 64-bit. The build is unsigned, so
SmartScreen shows "unknown publisher": choose **More info → Run anyway**.

No telemetry, no account, no auto-update.
