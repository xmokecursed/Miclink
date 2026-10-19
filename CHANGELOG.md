# Changelog

All notable changes to MicLink are documented here.

## [1.1.0] — 2026-10-19

### Added
- **Voice enhancement (PC app).** A new processing stage for clearer, crisper
  sound: removes low rumble, reduces boxy low-mid build-up, lifts the speech
  presence range, and adds a little high-frequency detail. Choose **Off**,
  **Clear**, or **Clear + quiet-voice boost** in Settings.
- **Automatic volume for quiet voices.** A leveler measures loudness
  continuously and raises soft voices toward a comfortable level (up to
  +24 dB in boost mode), while gently turning loud voices down. It stops
  boosting in very quiet moments so room noise isn't pulled up, and a soft
  limiter prevents clipping.
- **Auto volume on the phone.** Optional Android Automatic Gain Control
  (Settings → Auto volume).
- **"Microphone disconnected" alerts** on both devices: a system tray
  notification on the PC and a high-priority heads-up notification on the
  phone.
- **Auto-close after 5 minutes with no phone connected** (PC app and phone
  streaming service), with a 1-minute warning and a visible countdown on the
  PC. Can be turned off on the PC.
- The PC app now **re-establishes the USB connection automatically** when
  you unplug and replug the cable while streaming.

### Changed
- **New gray-and-white design** on both the phone and PC apps (light and dark
  modes). The phone app no longer takes its colors from your wallpaper, so it
  stays gray and white.
- Phone app: status card with an icon, clearer Start/Stop button, and a
  separate level card. Settings now explain what each option does.
- PC app: cards, a gain readout, and a window that resizes to fit its content.
- Error messages on the PC no longer vanish after two seconds.

### Fixed
- **Possible crackle or channel swap from the network stream.** TCP can split
  the audio mid-sample. The PC app now keeps the stream aligned to whole
  samples instead of assuming every network chunk is.

---

## [1.0.0] — 2026-09-11

First public release.

### Fixed
- **Choppy, low-quality audio.** The PC app was discarding most of every
  incoming audio chunk instead of buffering it properly, causing
  significant audio quality loss and dropouts. Audio now streams cleanly
  with no data loss under normal conditions.
- **Console window flashing repeatedly.** The PC app's background device
  check (runs every 2 seconds) was briefly flashing a console window each
  time on Windows. This no longer happens.
- **Microphone audio reachable over Wi-Fi.** The phone's local streaming
  socket was listening on all network interfaces instead of USB-only,
  meaning anyone on the same Wi-Fi network could technically connect and
  listen in. Now restricted to the USB connection only, as originally
  intended.
- **App crash risk when stopping mid-connection-issue.** Stopping the
  stream while the connection was in a bad state could, in rare cases,
  crash the app. Fixed with a safer shutdown sequence.
- Settings on the phone (sample rate, stereo, noise suppression) no longer
  silently fail to apply if changed mid-stream — they're now locked while
  actively streaming, with a clear explanation why.

### Improved
- Reduced end-to-end audio latency by trimming buffering on both the
  phone and PC sides.
- The PC app now finds `adb` automatically in its default install
  location, even if it isn't on your system PATH.
- Adaptive app icon added for the Android app.
- Settings (gain, mute, theme, audio format) now persist between restarts
  on both phone and PC.

---

## Pre-release development history

For transparency, here's what led up to the 1.0.0 release:

### 2026-09-10
- Fixed several missing dependencies and Compose API annotations that
  prevented the Android app from building cleanly from source.
- Reduced Android-side capture buffering (4x → 2x minimum) to lower
  latency.
- Added persistent settings storage on both phone and PC.
- Added a proper adaptive launcher icon for the Android app.

### 2026-09-07
- Diagnosed and fixed the core audio quality bug (see 1.0.0 notes above).
- Diagnosed and fixed the Wi-Fi exposure security issue (see 1.0.0 notes
  above).
- Added a bounded backpressure queue on the Android transport layer to
  prevent a slow network connection from stalling audio capture.

### 2026-09-06
- Initial project scaffold: Android capture/transport/UI layers, PC
  receiver/virtual-cable-routing/UI layers, first working end-to-end
  audio pipeline.

---

[1.1.0]: ../../releases/tag/v1.1.0
[1.0.0]: ../../releases/tag/v1.0.0
