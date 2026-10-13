
## The effect

HearSonic is a reactive granular processor with band-selective spectral feedback for live audio, built primarily for outdoor headphone listening. It also works as an AUv3 effect on instruments and recordings in a host.

Captured input feeds overlapping grains, tuned resonance, frequency-shifted cross-feedback, stereo echoes, diffuse reverb, and octave-up shimmer. Initialy inspired by RjDj Eargasm scene has harmonic wall of four tuned feedback combs rings, excited towards Bright with Warp raised.

## Current FX chain

The input splits into a dry path and several parallel paths, rough block scheme for FX chain:

```text
+--------------------------+
| Mic / AU host input      |
| Input trim / cleanup     |
+--------------------------+
             |
             +------------------------------------------+
             |                                          |
             v                                          | Dry
+--------------------------+                            |
| PARALLEL SOUND LAYERS    |                            |
|                          |                            |
| Filtered live input      |                            |
| Capture -> Grains        |                            |
| Tonal halo               |                            |
| Harmonics                |                            |
| Resonance <---+          |                            |
|     |         |          |                            |
|     +---------+          |                            |
| Shimmer   <---+          |                            |
|     |         |          |                            |
|     +---------+          |                            |
+--------------------------+                            |
             |                                          |
             +----> +--------------------------+        |
             |      | Echo      <---+          |        |
             |      |     |         |          |        |
             |      |     +---------+          |        |
             |      | Space     <---+          |        |
             |      |     |         |          |        |
             |      |     +---------+          |        |
             |      +--------------------------+        |
             |                   |                      |
             v                   |                      |
+--------------------------+     |                      |
| Mix all effect layers    | <---+                      |
+--------------------------+                            |
             |                                          |
             +------------------+                       |
             |                  v                       |
             |      +--------------------------+        |
             |      | Harmonic wall <---+      |        |
             |      |     |             |      |        |
             |      |     +-------------+      |        |
             |      +--------------------------+        |
             |                  |                       |
             v                  |                       |
+--------------------------+    |                       |
| + Harmonic wall          | <--+                       |
| Low weight: bass boost   |                            |
| Grit: saturation         |                            |
+--------------------------+                            |
             |                                          |
             v                                          |
+--------------------------+                            |
| Dry / wet mix            | <--------------------------+
+--------------------------+
             |
             v
+--------------------------+
| Output gain / limiter    |
| Audio output             |
+--------------------------+
```

In the standalone app, Record and History Machine take the final audio output.

The controls set each layer's level and character. Memory sets how far grains look back and how long effect tails last. The output limiter applies only in Environment mode. Hear environment selects the dry path.

## Listening and the sound field

Connect headphones, allow microphone access, and press Start listening. Tilt runs horizontally from Dark through Neutral to Bright. Warp increases upward, from short fragments to longer grains and spectral feedback. The Dark and Bright strips set Low weight and Harmonics; the Bright strip also sets the harmonic wall.

**Be advised that various combinations can lead to audio feedback. Please use with caution. Hit Panic or Bypass when it happens.**

## Parameters
- Sound Fields canvas to move the spehere around to change its Tilt/Warp/Dark/Bright position
- Tap on parameter group to reveal each with its slider & value, tap again to close.
- There is brief text desctiption for each when opened.


## Panic and Init
Panic stops the standalone audio engine, releases MIDI notes, and clears effect buffers. Press Start listening to restart. In an AUv3 host, Panic releases the bypass and clears the plug-in.

New installations use Environment in the standalone app, Signal in a host, and Resonance pitch for Notes control.


## Audio settings
The standalone app uses the selected processing sample rate. Device rate (automatic) follows the output device. You can also select 44,100, 48,000, or 96,000 Hz. A rate change restarts the effect. The AUv3 plug-in uses the rate set by its host.


## History Machine and Record
These controls are available in the standalone app. History Machine keeps the most recent processed output while audio runs. Set the buffer duration in Settings: 15, 30, 60, 120, or 300 seconds. The default is 60 seconds.

History Machine starts a take with the available history and continues recording live audio. Record starts a take from the current moment. Press the active button or Record to finish, then save the stereo file. Choose the format in Settings: AAC at 256 kbps (the default) keeps takes small, about 1.9 MB per minute, and is saved as an M4A file at 44.1 or 48 kHz. FLAC is lossless 24-bit at the processing rate, about 40 to 65 percent of the uncompressed size depending on the sound. Settings shows the estimated size per minute. The history take can use up to twice the buffer memory. Changes to the sample rate, history duration, and recording format are disabled during recording.

## Sessions

Press the session name to save, load, rename, or delete sessions and select factory presets.

## MIDI In

Notes control in Settings selects what MIDI notes do. The standalone app listens to connected MIDI sources; the AUv3 plug-in receives MIDI from its host.

Resonance and the harmonic wall use the latest note as their chord root and retain it after release. Grain notes play captured input at semitone offsets from note 60, multiplied by the playback speed set by Tilt. Grain mode supports velocity, pitch bend, pressure, sustain, and MPE; CC 74 moves through captured audio.

- **Resonance pitch + gate:** Notes tune and ring the resonance and harmonic wall.
- **Echo gate / Space gate:** Notes open the echo or reverb send.
- **Fragments gate:** Each note stutters the latest captured moment.

Tails continue after release. Sustain holds the gate.
