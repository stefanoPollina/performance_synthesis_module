# CONTINUUM Performance Synthesis Module

**Beta 06 · Standalone Web Audio Synthesis Workstation**

A browser-based, multi-engine synthesis environment developed as a performance-focused branch of the wider **Continuum Mosaic** concept. Beta 06 organises nine synthesis engines into three independently controllable chains, converging on one shared master output.

> **Development status:** Experimental beta. JavaScript syntax validation has been reported for this build, but end-to-end browser audio, MIDI, timing, and performance testing has **not** been completed. Features listed below describe the implementation and intended behaviour, not a production-readiness guarantee.

## Architecture

```text
CONTINUUM PERFORMANCE SYNTHESIS MODULE
│
├── CHAIN 1
│   ├── Synth Engine A — 16 parts
│   ├── Synth Engine B — 16 parts
│   └── Synth Engine C — 16 parts
│       └── Chain 1 mix / level / mute
│
├── CHAIN 2
│   ├── Synth Engine A — 16 parts
│   ├── Synth Engine B — 16 parts
│   └── Synth Engine C — 16 parts
│       └── Chain 2 mix / level / mute
│
└── CHAIN 3
    ├── Synth Engine A — 16 parts
    ├── Synth Engine B — 16 parts
    └── Synth Engine C — 16 parts
        └── Chain 3 mix / level / mute
                 │
                 ▼
         SHARED EFFECTS / MASTER BUS
                 │
          Compressor → Master
                 │
            Audio Output
```

**Total architecture:** 3 chains × 3 engines × 16 parts = **144 synthesis parts**. The interface provides engine selection and independent editing, alongside chain-level mixing. The source defines a 96-voice allocation limit; **144 parts does not mean 144 simultaneous voices**.

### Cloning versus independence

The **Clone Chain 1 into Chains 2 + 3** command copies the first chain's configuration to the other chains. This is a **one-time copy**, not an ongoing mirror: subsequent parameter changes can be made independently. The chains continue to share global transport and the final master processing path.

## Features

### Synthesis and sound design

- Nine engine instances, each with 16 editable parts.
- Sound families exposed in the interface: virtual analogue, FM/phase, drawbar organ, metallic/bell, electric keys, strings, bass and user sample.
- Oscillator waveform, detune, sub-level, filter cutoff/resonance, ADSR envelope, level and pan controls.
- Six-operator FM editing with a 6 × 6 routing matrix and operator envelopes.
- Imported audio multisample zones with note-range, velocity-range and root-note settings.
- Eight modulation routes per part, with engine-level modulation controls.
- Per-part insert DSP controls, plus shared chorus, delay, reverb and compression.

### Performance and sequencing

- 49-key on-screen performance keyboard and computer-key input.
- 16 trigger pads with sample loading and microphone-recording controls.
- Up to 64 sequencer steps, organised into four pages.
- Per-step pitch, velocity, gate and probability controls.
- AudioContext-clock lookahead sequencing architecture.
- Arpeggiator, chord memory, hold, octave shifting and performance motion controls.
- Global tempo, swing, play, stop and panic controls.

### MIDI

The interface includes Web MIDI support for compatible browsers and devices, with provisions for:

- Note-on/note-off and velocity.
- MIDI channel modes and part routing.
- Pitch bend, sustain pedal, modulation/expression and channel pressure.
- MIDI CC learning and mapping.
- External MIDI clock input, start, continue and stop.

**MIDI clock output is not implemented.** Browser and device support vary; MIDI behaviour has not been fully hardware-tested.

### Scenes and projects

- Scene banks and slots with local browser storage.
- Scene JSON import/export.
- Complete-project JSON import/export controls.
- Engine/chain configuration duplication.

**Important:** Imported sample audio is not embedded in exported JSON. Sample files must be reloaded when restoring a project that uses them.

## Getting started

1. Download `Continuum_Performance_Synthesis_Module_Beta_06.html`.
2. Open it in a modern desktop browser supporting the Web Audio API.
3. Click **START AUDIO** to initialise the audio context.
4. Select a synthesis chain and engine, then choose a part to edit.
5. Play using the on-screen keyboard, pads or sequencer.
6. If using a MIDI controller, click **ENABLE MIDI** and grant browser permission where prompted.
7. Use the chain controls to balance or mute chains, or clone Chain 1's configuration to Chains 2 and 3.
8. Export a JSON project to preserve editable settings.

The application is distributed as a **single HTML file** with its interface and JavaScript bundled together. No build step is required for basic local use. Microphone capture and some MIDI/browser permissions may require HTTPS or `localhost`.

## Example workflow

| Chain | Engine A | Engine B | Engine C |
|---|---|---|---|
| 1 · Rhythm | Bass synthesis | FM percussion | Short rhythmic textures |
| 2 · Harmony | Analogue pads | Multisampled keys | Organ layers |
| 3 · Expression | Lead synthesis | Metallic timbres | Evolving drones |

These are illustrative assignments, **not** factory presets. Each engine can be programmed separately while its audio contributes to the combined output.

## Current limitations

- **Experimental:** Full browser integration, MIDI hardware and audio-path regression testing remain outstanding.
- Global transport and shared effects are not completely independent per chain.
- The source contains an overall **96-voice** limit, so polyphony and CPU usage must be managed across the nine engines.
- Project JSON preserves sample-zone references and settings, **not** the audio files themselves.
- External MIDI clock is input-oriented; clock output is not available.
- The current build is a single-file beta, not yet a packaged plugin, VST/AU instrument or DAW-hosted application.
- Timing, voice release, modulation interactions and compatibility across browsers require further verification before live-performance reliance.

## Development priorities

1. Browser-level functional tests covering all nine engines and three audio chains.
2. Verify isolated engine control and clone behaviour, including save/restore.
3. Confirm MIDI channel mapping, clock sync, controller learn and sustain behaviour with hardware.
4. Stress-test voice allocation, CPU load, routing, effect processing and long sessions.
5. Extend per-chain automation and cross-chain control routing while preserving engine independence.
6. Add reliable project/sample packaging and deployment documentation.

## Relationship to Continuum Mosaic

**Continuum Mosaic** is the broader modular development environment. **Continuum Performance Synthesis Module** is a focused performance instrument developed from that architectural approach: independently programmable synthesis engines organised into higher-level chains and unified by a common audio output.

## Version

**Beta 06** — Three chains, each containing three 16-part synthesis engines, with independent chain controls and a shared master bus.

---

*Continuum is an independent synthesis project. The interface is hardware-inspired and is not affiliated with Roland.*
