## HearSonic

Turn live input into grains, tuned resonance, echoes, and octave shimmer. Use the microphone with headphones, or process instruments and recordings in an AUv3 host. The harmonic wall takes inspiration from the RjDj Eargasm scene.

## Start listening

Connect headphones, allow microphone access, and press Start listening.

- Tilt: move left for slow, bass-heavy grains; right for harmonics and shimmer. Near the centre, Resonance adds tuned ringing.
- Warp: move up for longer grains, time scatter, reversals, and spectral feedback.
- Dark strip: set Low weight, the bass boost toward Dark.
- Bright strip: set Harmonics, including the harmonic wall at any Tilt.

Open a parameter group, then select a parameter to show its value, slider, and short description. Select it again to close the editor.

Feedback can occur. Press Panic to stop it, or hold Bypass to hear dry input. With VoiceOver, please activate Bypass to toggle it.

## Motion sensors

Motion and Pin center buttons are enabled only on devices which support accelerometer/gyroscope sensors.
Turn on Motion to move the ball with the device - balls rolls with gravity, displacement is relative to center which can be set using 'Pin center' button, long press to reset the center.
Center is rest position when the device is horizontal.

## Signal flow

Input trim feeds the dry path and parallel effect layers. Grains, resonance, harmonics, shimmer, Echo, and Space form the wet signal. The harmonic wall, Low weight, and Grit shape that signal before Dry / wet and Output gain.

Memory sets grain lookback and effect decay. Environment mode adapts to input activity and limits output peaks. Signal mode accepts quiet input without output limiting. Bypass keeps processing active; Input trim, Output gain, and the Environment limiter still apply.

Record and History Machine capture the final output.

## Panic and Init

Panic stops standalone audio, releases MIDI notes, and clears effect buffers. Press Start listening to resume. In a host, Panic clears the effect and releases bypass.

Init resets sound controls and Output gain. It keeps Input mode, MIDI mapping, and saved sessions.

## Audio settings

Choose Device rate (automatic), 44,100, 48,000, or 96,000 Hz. Changing the rate restarts audio. An AUv3 host sets its own rate.

New installations use Environment mode in the app and Signal mode in a host. MIDI notes default to Resonance pitch.

## Recording

Standalone only:

- Record starts a new take now.
- History Machine starts with buffered output, then records live audio.
- Press the active button or Record to finish and save the stereo file.

Choose the saved recording format in Settings. Estimated file size is shown per minute.

- AAC (default): 256 kbps in an M4A file, about 1.9 MB per minute. Rates above 48 kHz convert to 44.1 or 48 kHz.
- FLAC: lossless 24-bit at the processing rate. Estimated size is 40–65% of uncompressed audio; actual size varies with the sound.

Set history length in Settings: 15, 30, 60, 120, or 300 seconds; default 60. Recording with history can use twice the buffer memory. Sample rate, history length, and recording format are locked during recording.

## Sessions

Press the session name to save, load, rename, or delete sessions and choose presets. The app restores your current session automatically. Saved sessions keep all settings; factory presets keep Output gain, Input mode, and MIDI mapping. An AUv3 host saves the session with its project.

## MIDI

Choose Notes control in Settings. The app uses connected MIDI sources; the plug-in receives MIDI from its host.

- Resonance pitch: the latest note sets the chord root and keeps it after release.
- Grain playback pitch: notes transpose captured audio relative to note 60, on top of Tilt playback speed.
- Resonance + grain pitch: control both.
- Resonance pitch + gate: tune and gate resonance and the harmonic wall.
- Echo gate / Space gate: open the echo or reverb send while notes are held.
- Fragments gate: stutter the latest captured audio.

Velocity sets gated levels. Tails continue after release; sustain holds gates. Grain playback supports velocity, pitch bend, pressure, sustain, and MPE. CC 74 moves through captured audio.

## Current FX chain

The input splits into a dry path and parallel effect paths. Rough block diagram:

```text
+--------------------------+
| Mic / AU host input      |
| Input trim / cleanup     |
+--------------------------+
             |
             +------------------------------------------+
             |                                          |
             v                                          | Dry
+------------------------------------------+            |
| PARALLEL SOUND LAYERS                    |            |
| (* = also sent to Echo / Space)          |            |
|                                          |            |
| Filtered live input *                    |            |
| Tonal halo *                             |            |
| Capture -> Grains * ----------+          |            |
|                               |          |            |
| Live gesture --+--------------+          |            |
|                |              |          |            |
|                +--> Harmonics |          |            |
|                |        |     |          |            |
|                |        +-----+          |            |
|                |              v          |            |
|                |         Resonance * <-+ |            |
|                |             |         | |            |
|                |             +---------+ |            |
|                |                         |            |
|                +--> Shimmer <---+        |            |
|                        |        |        |            |
|                        +--------+        |            |
+------------------------------------------+            |
             |                                          |
             +-- * layers ---+                          |
             |               v                          |
             |      +--------------------------+        |
             |      | Echo  <---+              |        |
             |      |   |       |              |        |
             |      |   +-------+              |        |
             |      |   v                      |        |
             |      | Space <---+              |        |
             |      |   |       |              |        |
             |      |   +-------+              |        |
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
