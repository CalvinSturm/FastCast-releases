# FastCast v0.9.2 — Open Beta

**Long recordings finish saving again.**

This is a fixes-only hotfix for v0.9.1. Capture, streaming, Instant Replay,
audio and encoding are unchanged. If you record for more than about an hour at
a time, install this update.

## Long recordings could fail to save

FastCast writes a recording as a series of 15-second working clips and joins
them into one MP4 as it goes. In v0.9.1, a recording longer than about an hour
could get stuck in that join: after you pressed Stop, **Saving…** could run
for hours. If FastCast was closed or the PC shut down during that time, the MP4
was left incomplete and would not play. Only the 15-second clips were left, in
the recording's `.fastcast-parts` folder.

It happened when the audio in those clips started several seconds after the
video, which a long take of a mostly still screen can build up to. Windows' MP4
writer then waited for audio that FastCast could only write once the wait was
over. Each clip took minutes to join instead of milliseconds. The join that runs
during the recording fell behind and handed off to a full join at Stop, and
that hit the same wait on every remaining clip.

Each clip now joins in milliseconds. On the 2h21m recording where this was
found, all 530 clips joined in 52 seconds.

## Recovering a recording that did not save

If a recording's `.fastcast-parts` folder is still next to where the MP4 should
be, v0.9.2 can rebuild it. When FastCast starts, it says:

> A recording did not finish saving. Select it under Recent recordings to
> rebuild it.

Select the entry marked **Not saved · Recover** under **Recent recordings**.
FastCast rebuilds the MP4 from the clips, and it no longer gets stuck on the
clips that caused the problem.

If you already deleted the `.fastcast-parts` folder, the recording cannot be
recovered.

## Pro price

FastCast Pro is **$19** until the v1.0 launch, when the price rises to **$29**.
The buy link and the upgrade hint in the app now show this. They previously
showed the Founding Supporter Sale price, which has ended. What Pro unlocks is
unchanged.

## Upgrading

Install the v0.9.2 MSI over v0.9.1. Your settings, destinations and remembered
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
