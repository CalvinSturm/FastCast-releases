# FastCast v0.8.0 — Open Beta

**Save the thing you didn't know you needed to record.** FastCast can now keep
the last few minutes of your screen in memory and write them to an MP4 after the
fact — press **`Ctrl+Alt+F8`** and the clip is on disk, with the buffer still
running behind it.

This is a feature release. Recording, streaming, audio and encoding behave as
they did in v0.7.1; what is new sits alongside them.

## Instant Replay

Turn **Replay** on in the strip under the preview and pick how far back it
should reach — 30 seconds, 1 minute, 2 minutes or 5 minutes (the CLI takes
anything from 15 to 300 seconds). From then on FastCast holds that much footage
in RAM and writes **nothing** to disk until you ask it to.

Press **`Ctrl+Alt+F8`** and the last N seconds become an ordinary MP4 in your
output folder, listed in **Recent files** with its length and size like any other
take. Saving does not stop, restart or rewind the buffer, so you can save twice
in a row and keep both.

Nothing is re-encoded. The buffer retains the encoder's own H.264/AAC packets
and muxes them straight through, so a save costs a disk write rather than a
second encode pass, and the capture thread only ever does a pointer copy. Memory
is bounded by both the window you chose and a bitrate-derived byte cap
(64 MiB–1.5 GiB). Clips are written under a temporary name and renamed once
finalized, so a partial file can never be mistaken for footage.

From the command line:

```powershell
fastcast --replay [--seconds N] [--folder DIR] [--monitor N] [--fps N] [--no-audio]
```

**Replay and recording stay mutually exclusive**, and each direction is handled
the way it should be: pressing **Start recording** turns the buffer off and says
so, while arming the buffer during a take is refused with a reason rather than
interrupting the recording.

**Limits worth knowing.** A clip captures the selected **display** and its audio
— a selected app and the webcam overlay are dropped for now, and reported when
they are — and a saved clip can run up to one GOP longer than the window you
chose, because it has to start on a keyframe.

## FastCast in the notification area

Instant Replay is most useful when FastCast is not in your way, so FastCast now
has a tray icon. Right-click it to arm or disarm Replay, save a clip, show the
window, or exit.

Closing the window can hide FastCast to the tray instead of quitting — **off by
default**, so upgrading never changes what your close button already did. **Start
with Windows** is an opt-in tray toggle that launches FastCast hidden at sign-in.
Launching at login never arms the buffer: you get a tray icon and a live
`Ctrl+Alt+F8`, never a background capture you did not ask for.

Uninstalling now removes that startup entry. Before this release nothing wrote
it, so there is nothing stale to clean up from older versions.

## The interface got a real control system

Every button used to draw its own shell — its own corner radius, press travel,
hover ramp and caption padding — so the same interaction meant different things
on adjacent controls, and renaming a caption could resize a chip somewhere else
entirely. One painter now owns the whole family, and button widths are derived
from the padding that painter actually uses, so the layout can no longer disagree
with the drawing about how wide a button is.

Buttons also *look* like objects rather than outlines: an edge one step above
their own fill, a light catch along the top, and a contact shadow underneath,
instead of a bright hairline drawn around a flat fill. Pressing one drops the
light as well as darkening it. An "on" toggle is filled with the interaction
blue instead of being outlined in it — so accent now means exactly one thing (on,
selected, or focused) and hover is a neutral brighten. Controls that carry a
brand or feature colour, like the platform chips and Green screen, keep their
own.

What you will notice control by control:

- **Replay** is a toggle with a fixed caption, not a status pill that re-lettered
  itself to "Replay on" and grew the strip every time it was armed. Buffer state
  is reported in the status line, where a readout belongs.
- **Webcam** is a toggle whose width no longer changes with its state, anchored
  so that turning the camera on adds Crop and Green screen to its *left* rather
  than shifting the control you just clicked out from under the pointer.
- **Crop** is an ordinary button that opens the crop editor, still shown only
  while the webcam is live.
- **Utility actions** — refresh, detailed view, browse, the destination rows'
  show-key / paste-key / remove, and Recent files' **Open** and **Show in
  folder** — are icon buttons with tooltips. The last two replace underlined text
  links with real click targets.
- **A clicked button no longer keeps a keyboard focus ring.** Windows leaves
  focus on a button after a mouse click, so the ring meant for keyboard
  navigation stayed drawn on whatever you last pressed. It is shown for keyboard
  focus only now, and returns the moment you tab.

Record and Go Live keep their visual priority and their behaviour.

## If you own Pro, FastCast stops selling it to you

A paid licence still saw the pitch: the compact dashboard kept an "Upgrade to
Pro" link under a "FastCast Pro" caption, and the Advanced card kept its Upgrade
button next to Activate and Deactivate. Both are now replaced by a single Pro
badge once your licence is active — offline grace included — and Activate /
Deactivate take the freed width.

Free, expired and invalid licences are unchanged: they keep "FastCast Free" and
the upgrade link, because for them it is still an offer worth making. Activating
or deactivating switches between the two immediately, with no restart.

## The mouse pointer shows in the preview

The live preview hardcoded the cursor off, so FastCast looked like it drops the
pointer while recordings had it all along. Both now follow one setting — on by
default, including for settings files written by older versions — with a **Show
cursor** toggle under Advanced. Toggling it re-points the preview immediately; a
recording keeps whatever it started with.

On **Advanced → Backend → DXGI** the pointer is still absent whatever the setting
says: Desktop Duplication excludes it by design, and compositing one in is
separate work.

## New application icon

The "F." mark is now a standalone blue-to-red glyph rather than a mark inside a
dark rounded tile, so it reads as itself against any taskbar, Explorer background
or theme. The embedded icon carries the same ten sizes as before (16 through
256), and the in-app header logo follows it automatically — both come from the
one resource.

## Also fixed

- **A saved replay clip no longer opens on silence.** The buffer evicted audio in
  step with video, by arrival order — but a hardware encoder returns its video
  well after the frames were fed (4.8 s at 30 fps on the GPU this was found on),
  while audio is kept the moment it arrives. Everything "older" than the cut in
  arrival order therefore included audio the clip still needed, so clips lost
  their first several seconds of sound, and a window shorter than the encoder's
  lag came out silent. Audio is now retained by timestamp and dropped only once
  the window has genuinely moved past it.
- **The Replay control no longer paints over the Re-sample chip.** With a camera
  on and the green-screen key armed, the length picker was drawn on top of
  Re-sample. The compact dashboard drops the visible Re-sample chip (right-click
  the Green screen chip to re-pick the colour) and abbreviates the length chip;
  the detailed surface keeps the chip and gains the margin.
- **`fastcastc.exe` with no arguments** no longer launches the FastCast window
  and then sits on a blank console. It is a companion for a FastCast that is
  already running, so with no arguments it prints short usage plus whether
  FastCast is up, and starts nothing. Launching is the explicit
  `fastcastc --launch`.
- **`fastcastc.exe` and Ctrl+C.** It no longer dies on the first interrupt and
  leaves FastCast running behind it; it absorbs the first one and waits for the
  real exit code. A second Ctrl+C still gives up immediately.

## Privacy, unchanged

No telemetry, no account, no crash upload, no auto-update, no background network
calls. Instant Replay is entirely local: RAM until you press the hotkey, then a
file in your own output folder. The only network activity is still what you start
— streaming to your chosen ingest, and the manual **Check for Updates** action.

## Install

Windows 10 (20H1 / 2004+) or Windows 11, 64-bit. Use
`FastCast-0.8.0-win-x64.msi` for the easiest setup, or
`FastCast-0.8.0-win-x64.zip` to extract and run.

The build is unsigned, so SmartScreen shows "unknown publisher": choose **More
info → Run anyway**. Verify your download against the published `.sha256`
sidecar. Full steps: [`DOWNLOAD_INSTALL.md`](DOWNLOAD_INSTALL.md).
