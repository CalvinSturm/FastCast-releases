# FastCast v0.7.1 — Open Beta

**Stop is instant now.** However long you recorded, pressing Stop hands the app
straight back to you. The file finishes writing on its own row in Recent files
while you carry on — set up the next take, change your source, close the window
when it is done.

A maintenance release. Nothing about capture, encoding, audio or streaming
changed: v0.7.1 records exactly what v0.7.0 recorded.

## Stop no longer waits for the whole recording

Recordings are stitched together **as they run** rather than remuxed in one go
at the end. Stop joins the result that is already written and renames it.

Measured on the development machine:

| Content recorded | Stop before | Stop now |
|---|---|---|
| 12 seconds | 175 ms | 33 ms |
| 36 seconds | 436 ms | 29 ms |

The old cost grew with the length of the take. The new one does not move — the
~30 ms that remains is the moov write and the output probe, both fixed.

A separate 50 ms sleep in the finalize wait was removed as well; it accounted
for 32.6 ms of a 50.7 ms Stop, the single largest piece of the very path this
work exists to shorten.

## The app comes back before the file is done

Stop used to freeze the whole window until the file was written and validated,
because "a recording is running" and "this file is still being written" were the
same state. They are now separate.

The moment your screen, microphone and camera are actually released, the window
returns to idle and the take moves onto its own **Recent files** row showing
`Saving…`, then swaps in place to the finished entry with its length and size.

While a take is saving, its row deliberately offers no action and shows no
length or size — the MP4 has no index yet, so opening it early would fail or
play as truncated footage. Devices are only reported free once they genuinely
are, so the worst case is a slightly longer wait, never a camera reopened while
the previous take still holds it.

## Fixed

- **A finished recording could sit on `Saving…` indefinitely.** The file was
  complete and playable, but the Recent card was never repainted — a full repaint
  only ran when the recording session boundary flipped, which now happens when
  the app returns to idle rather than when the file finishes. Seen holding
  `Saving…` for more than 30 seconds after the recording was done.
- **Apps and displays opened after FastCast started never appeared in Sources.**
  The lists were built once at startup, and the only thing that rebuilt them was
  the Refresh button — which is not shown on the simple view, so restarting
  FastCast was the only way to pick up a newly opened app. Every Sources picker
  now re-scans as you open it, and connecting or disconnecting a monitor updates
  the Screen list on its own.
- **Refresh no longer throws away your App selection.** It reset the App picker
  to "Entire screen" every time. Your choice is now tracked by the window
  itself, not by its position in the list, so an app opening in the background
  cannot quietly move capture onto something else. If the app you picked has
  closed, or the display you picked was unplugged, FastCast says so instead of
  silently switching.

## Known limitations

- **You cannot start a new recording while the previous one is still saving.**
  The attempt is refused with a reason. The finished take still owns its encoder
  until it is written out, and sharing that safely is a deeper change than this
  release makes.
- The incremental stitch has **not** been manually validated against a long
  take, a slow disk, a nearly full drive, or crash recovery. If you record long
  sessions or work close to a full disk, keep an eye on your output for now and
  report anything that looks wrong.

## Requirements and install

Windows 10 (20H1 or newer) or Windows 11, 64-bit. Use the per-user MSI for the
easiest setup, or the portable ZIP for extract-and-run. The MSI installs under
your local app data and adds Start-menu and Apps & Features entries; uninstall
keeps your settings, logs and recordings.

The build is **unsigned**, so SmartScreen shows an "unknown publisher" warning:
choose **More info → Run anyway**.
