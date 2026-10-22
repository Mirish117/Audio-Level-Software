# Audio Level Software

An accurate audio level meter for a church or live-event booth running an **Allen & Heath GL2200** (or any analog mixer) and a **Blackmagic Web Presenter HD** live stream.

It is one file, `audio-level-meter.html`. Download it and double-click it to open it in **Google Chrome or Microsoft Edge**. Nothing to install, and no internet needed once it's on the computer.

## What it shows

There are three meters. Use any combination of them.

| Meter | What it measures | Feed it from |
|---|---|---|
| **Live Stream Output** | Exactly what viewers hear: loudness (LUFS), true peak, clipping, left/right balance, phase, and silence | The Web Presenter HD over USB, or a tap of the feed going to the camera (see below) |
| **House Mix (Main L/R)** | Gain structure of the GL2200 main mix (all the mics and instruments). Can be calibrated to read like the GL2200's own meters | A spare GL2200 output (main, matrix, mono or record out) into a USB audio interface |
| **Room Loudness (SPL)** | How loud the room actually is, in dBA, against a target range for your service style | A microphone in the room (USB mic or laptop mic), calibrated with an SPL meter or phone app |

Every meter gives **plain-English suggestions** that update every second, for example "Stream too quiet: raise the stream send by about 4 dB" or "Clipping: the camera's 3.5 mm input is being overloaded". The banner at the top shows the most urgent problem. The **event log** records every clip, peak over the limit, and silent stretch with a timestamp, and you can export it as CSV after the service.

### Targets used

* **Live stream:** −14 LUFS integrated, the YouTube and Facebook normalisation level (you can change it), with true peaks below −1 dBTP.
* **House mix:** GL2200 meters averaging around 0, with peaks staying out of the red.
* **Room:** contemporary worship 88–95 dBA, blended 82–90 dBA, traditional or spoken 75–85 dBA (1-minute average). It also warns when the whole-service average goes above NIOSH hearing guidance (94 dBA for 1 hour).

Measurements follow ITU-R BS.1770-4 and EBU R128: K-weighted, gated integrated loudness, 4× oversampled true peak, and loudness range (LRA). The room meter uses A-weighting.

## Hooking it up

### Live stream (most important)

Your signal chain is: GL2200 output → 3.5 mm cable → camera → Web Presenter HD → internet.

* **Best option:** connect the Web Presenter HD's USB-C port to the computer. It shows up as a webcam and audio input, usually named “Blackmagic Web Presenter”. That is the audio *after* the camera, which is exactly what goes out. Pick it in the Live Stream meter. Check that your Web Presenter keeps streaming while its USB webcam output is in use.
* **Otherwise:** split the feed that goes to the camera with a passive Y-splitter, and send one leg into a USB audio interface line input. This shows what leaves the mixer, but not any gain changes or distortion inside the camera.

### House mix

Connect a spare GL2200 output into a USB audio interface input. Set the interface gain so normal service peaks land around −12 dBFS, then don't touch it. Use **Targets & calibration → Calibrate** to make the meter read in GL2200 meter units.

### Room

Put a USB mic (or use the laptop mic) where the congregation sits. Calibrate it once against an SPL meter or a phone SPL app set to A-weighted, slow.

## Before you trust the numbers

* Set the input level in Windows or macOS sound settings to a fixed value. Turn **off** any "audio enhancements", automatic gain control and noise suppression for that input.
* Press **Reset all** at the start of each service, so the integrated loudness covers just that service.
* Chrome asks for microphone permission each time you open the file. Click Allow. Your input choices and calibrations are remembered.

## Common problems it catches

* **Distorted stream audio:** the GL2200's line-level output overloads the camera's 3.5 mm mic-level input. Set the camera input to LINE or use an attenuator cable (−20 to −40 dB), turn off the camera's auto level, and lower the send.
* **Audio on one side only:** a mono (TS) plug in a stereo 3.5 mm jack.
* **Stream silent while the house is live:** a muted send or an unplugged cable.
* **Loud peaks, quiet average:** add compression or limiting on the stream send instead of just turning it up.
