# FastCast v0.10.0 — Open Beta

**A background behind your camera, and safer stream keys.**

v0.10.0 lets you put an image, a solid colour or a looping video behind your
keyed webcam, reduces background noise on your mic, accepts OBS Virtual Camera
as a webcam, adds bitrate and keyframe limits for Custom destinations, and
fixes several ways a stream key could end up somewhere it shouldn't. If you
stream, install this update.

## Security fixes

**A stream key pasted into a server URL is no longer saved to disk.** Some
platforms show the server URL and the stream key as one combined URL, such as
`rtmp://host/app/<your key>`. If you pasted one of those into a Custom or Kick
row, FastCast saved the whole URL, key included, to `settings.ini` in plain
text. It now saves only the server and app part, and the same applies to the
Advanced stream URL. Streaming works exactly as before.

A key an earlier version saved this way stays in `settings.ini` until you next
change a setting, which rewrites the file without it. **If you ever pasted a
key into a URL, consider resetting that stream key on the platform.**

**Stream keys are masked in error messages and the log.** When an ingest server
rejects a stream, part of the error text comes from the server and could echo
your key back. FastCast now masks the key before that text is shown or logged.

**Invalid stream URLs no longer echo what you typed.** A malformed URL with
credentials in it could put part of the secret in the status line and the log.
The error is now fixed text, and URLs with a `user:password@` part are rejected.

**A warning for unencrypted Custom destinations.** When a server URL you
entered yourself uses plain `rtmp://`, the live status line turns orange and
names the destination, because your stream key and video cross the network
unencrypted. Use the `rtmps://` URL if your platform offers one. Nothing is
blocked, and the built-in presets are not flagged.

**Safer library loading.** A Windows theme library is now loaded only from the
Windows system folder, so a file with the same name next to a portable
`fastcast.exe` can't be loaded instead.

The `zip` library is updated for three published advisories. FastCast only
writes zips (the local support bundle) and was not exposed.

## A background behind your camera

Right-click the **Green screen** chip and choose what sits behind your keyed
camera:

- **Screen**, as before.
- **An image.** It is centre-cropped to fill the output without stretching.
- **A solid colour.**
- **A video.** Choose a clip once and FastCast plays it on a seamless loop,
  and remembers it next time. The clip's sound is not used yet.

You no longer need a monitor showing the picture full screen for FastCast to
capture. The background keeps working while FastCast is minimized and while you
use that monitor, and changes apply live, mid-stream included. If the file is
missing or can't be read, FastCast shows black with a warning. It never falls
back to showing your screen.

## Reduce background noise on your mic

Press **F2** for the detailed view and click the new icon on the **Mic** row,
between the level readout and the mute button. It removes steady background
noise such as fans, air conditioning, PC hum and keyboard clatter from your
microphone. It runs on your PC, with nothing downloaded or sent anywhere.

It works live while you record, stream or buffer Instant Replay, and FastCast
remembers it next time. It is off until you turn it on, and desktop audio is
never touched. It is free for everyone.

## OBS Virtual Camera as a webcam

Anything that sends to **OBS Virtual Camera**, such as OBS itself or a
face-blur or effects tool built on it, now shows up in FastCast's webcam list.
Pick **OBS Virtual Camera** and FastCast uses that feed like any other camera,
green screen and backgrounds included. If the sending app restarts, FastCast
picks the feed back up. If nothing is sending yet, you get a clear error
instead of a blank camera.

## Bitrate and keyframe limits for Custom destinations

Some ingest servers accept a stream and then drop it about 30 seconds later
when it doesn't match their encoder guide. A Custom row now has two small boxes
after its server URL: the maximum video bitrate (kbps) and the keyframe
interval (seconds) that server asks for. Leave them empty to keep FastCast's
own bitrate and 2-second keyframes.

When you stream to several destinations at once, the strictest limit any of
them states applies to all of them.

## Fixes

**A blocked microphone no longer loses the recording.** If Windows refused the
microphone, most often because *Microphone access* is off under Settings ›
Privacy & security › Microphone, the take failed at Stop with only "Access is
denied" and nothing was saved. FastCast now records without the microphone and
says so, naming the setting to turn back on. The same applies to desktop audio
and to a device that can't be opened. The audio track stays in the file as
silence, so it still plays everywhere.

**Stop no longer hangs on a stalled destination.** If an ingest server stopped
reading mid-stream, Stop, or closing FastCast, could wait on it indefinitely.
Stop now gives each destination about two seconds to finish sending before it
closes them. Under heavy congestion the last moments of the live stream may be
cut. The local recording is unaffected.

**The log records why a session ended** when a recording or Instant Replay
session ends with an error, so a support bundle shows the cause.

## Upgrading

Install the v0.10.0 MSI over v0.9.2. Your settings, destinations and remembered
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
