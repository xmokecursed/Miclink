# Privacy Policy

**Effective date:** September 11, 2026

MicLink is designed around a simple principle: your microphone audio should
never leave the physical USB cable between your phone and your PC. This
document explains exactly what the app does and doesn't do with your data.

## What MicLink does

- Captures audio from your phone's microphone, **only while you have
  actively tapped Start** on the phone app.
- Streams that audio over a **USB cable only**, via Android's `adb`
  debugging bridge, to the MicLink app running on your own PC.
- Writes that audio into a virtual microphone device on your PC, so other
  apps you choose (Discord, Zoom, OBS, etc.) can use it.

## What MicLink does not do

- **No internet access for your audio, ever.** Audio data travels only
  over the USB cable between your specific phone and your specific PC. It
  is never uploaded, streamed to a server, or transmitted over Wi-Fi or
  mobile data.
- **No cloud accounts, sign-ins, or user profiles.** There's nothing to
  create an account for — the apps don't know or care who you are.
- **No analytics, telemetry, or crash reporting.** MicLink doesn't
  collect usage statistics, doesn't phone home, and doesn't track how or
  when you use it.
- **No advertising, and no data is sold or shared with any third party**,
  because none is collected in the first place.
- **No recording or storage of your audio.** Audio is streamed live and
  never written to disk by MicLink on either the phone or PC side.

## About the permissions MicLink requests

**On Android:**
- **Microphone (`RECORD_AUDIO`)** — required to capture audio at all. This
  is the app's core function.
- **Foreground service / notification** — Android requires a persistent
  notification while an app accesses the microphone in the background
  (e.g. with the screen locked), so streaming can continue reliably. This
  is an Android OS requirement, not something MicLink chose to add for its
  own purposes.
- **Internet (`INTERNET`)** — this permission is required by Android for
  *any* app that opens a network socket, even a purely local one. MicLink
  uses it only to open a loopback (USB-only) connection to your PC — it
  does not grant, and the app does not use, any actual internet access.
  You can verify this yourself in the source code, linked below.

**On the PC:** MicLink runs as a normal desktop application. It uses your
system's `adb` tool to detect your phone over USB, and writes audio into
whatever virtual audio device you have installed (e.g. VB-Audio Virtual
Cable). It does not request or need administrator privileges to run (only
the one-time virtual cable driver installation does, which is a separate,
third-party piece of software).

## Third-party software MicLink relies on

MicLink itself doesn't bundle or embed any third-party analytics or
tracking libraries. It does depend on you separately installing:

- **Android Platform Tools (`adb`)** — published by Google, used to
  establish the USB connection.
- **VB-Audio Virtual Cable** (Windows) or **BlackHole** (macOS) — the
  virtual audio device driver your operating system uses to expose
  MicLink's output as a microphone to other apps.

Neither of these is developed by, or affiliated with, this project. Their
own privacy practices are governed by their respective publishers, not by
this policy.

## Changes to this policy

If this policy is ever updated, the change will be reflected in this file
within the repository, with an updated effective date at the top.

## Questions

Open an [issue](../../issues) on this repository if you have questions
about how MicLink handles data.
