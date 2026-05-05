# Lookdev Asset Pipeline

Date: 2026-05-03
Status: Production pipeline baseline

## Purpose

This pipeline exists because the target quality is not "a working coded orb."

The target is:

```txt
Dribbble-grade organic animation
+ AI state reactivity
+ Eden/Jarvis routing meaning
+ browser runtime integration
```

That requires a motion production pipeline before implementation.

## Core Decision

The recommended path is hybrid:

```txt
Lookdev asset first
Runtime reaction second
State system third
```

Do not continue by endlessly tuning a WebGL shader without a locked visual target.

## Pipeline Overview

```txt
Reference Lock
-> Motion Bible
-> Lookdev Experiments
-> Hero Direction Selection
-> Asset Export
-> Runtime Integration
-> Signal Wiring
-> Motion QA
-> Production Hardening
```

## Phase 0: Reference Lock

Goal:

- choose the references that define the target
- stop changing the visual direction every implementation pass

Inputs:

- user's local reference videos
- Dribbble orb/motion references
- any selected TouchDesigner/Blender/Spline examples

Deliverables:

- `Reference-Teardown.md`
- reference board with 3-5 primary references
- explicit adopt/adapt/reject list

Acceptance:

- one primary visual family is selected
- references are not treated as vague inspiration
- each reference has a role: form, light, particle, motion, interaction, or transition

## Phase 1: Motion Bible

Goal:

- define the orb's body language before code

Deliverable:

- `Motion-Bible.md`

Acceptance:

- state grammar exists
- continuous signal model exists
- transition durations exist
- visual layer response matrix exists
- red team checklist exists

## Phase 2: Lookdev Experiments

Goal:

- create high-quality visual candidates before choosing the runtime strategy

### Track A: TouchDesigner Lookdev

Best for:

- living organic motion
- feedback loops
- audio-reactive / signal-reactive visuals
- particle and glow behavior
- quick visual iteration

Output candidates:

- black-core orb
- membrane + cilia
- particle lattice
- diagonal synapse wave
- state-reactive pulse studies

Risks:

- browser integration is indirect
- export can become video-like rather than truly interactive
- requires separate TouchDesigner authoring skill

Use when:

- the priority is organic feel and motion richness

### Track B: Blender Lookdev

Best for:

- high-fidelity lighting
- materials
- volumetric glow
- camera framing
- polished hero loops

Output candidates:

- prerendered idle loop
- lighting/material reference frames
- particle/corona stills
- high-quality turntable

Risks:

- less real-time interactive
- render/export iteration can be slower
- exact state reactivity must be recreated in WebGL or layered on top

Use when:

- the priority is optical quality and premium still frames

### Track C: Spline Lookdev

Best for:

- fast browser-friendly 3D sketches
- interactive prototypes
- quick camera/material layout

Output candidates:

- embedded 3D scene prototype
- simple interactive state demo
- form and scale exploration

Risks:

- may not reach the organic shader depth needed
- can look like a generic 3D web object

Use when:

- fast visual prototyping is more important than final optical depth

### Track D: Pure WebGL Lookdev

Best for:

- direct runtime control
- shader parameter experiments
- AI state reactivity
- final web integration

Output candidates:

- GLSL shader prototype
- particle field prototype
- signal-driven motion controller
- browser QA captures

Risks:

- taste iteration is slower
- high optical quality requires shader artist-level tuning
- easy to produce a technical demo instead of a premium asset

Use when:

- the visual direction is already locked
- runtime reactivity matters more than prerender perfection

## Phase 3: Hero Direction Selection

Compare candidates using this scorecard:

| Criterion | Weight | Question |
| --- | --- | --- |
| Still-frame quality | High | Does it look premium without motion? |
| Organic motion | High | Does it feel alive rather than procedural? |
| State readability | High | Can user infer broad state without label? |
| Runtime feasibility | High | Can this run in the Eden front? |
| Reactivity | High | Can it respond to real signals? |
| Performance risk | Medium | Will browser/GPU cost be acceptable? |
| Production complexity | Medium | Can Codex maintain and integrate it? |
| Asset portability | Medium | Can it be exported/versioned cleanly? |

Selection rule:

```txt
Choose one hero direction.
Do not merge multiple beautiful candidates unless they share the same motion grammar.
```

## Phase 4: Asset Export Strategy

There are three viable export models.

### Model A: Pure Runtime WebGL

Use:

- all layers are shader/Three.js driven
- asset files are minimal

Good for:

- maximum state reactivity

Bad for:

- fastest path to premium optical quality

### Model B: Prerender Base + WebGL Overlay

Use:

- prerendered base loop for premium glow/material
- WebGL overlay for particles, cilia, rim pulses, state effects

Good for:

- premium first impression
- manageable runtime reaction

Bad for:

- full interactivity
- transparent video/browser compatibility

Important:

- if alpha video causes browser issues, use black-background additive/screen blending or image-sequence fallback
- test Safari/Chrome behavior before committing to a format

### Model C: TouchDesigner Runtime Bridge

Use:

- local TouchDesigner instance runs the visual system
- app sends control signals over OSC/WebSocket/HTTP bridge

Good for:

- most organic and real-time visual depth
- live performance-style control

Bad for:

- dependency on a running external app
- harder distribution
- more operational complexity

Recommended default:

```txt
Model B for product frontend
Model D/Pure WebGL only after visual target is locked
TouchDesigner runtime bridge only for local personal command center experiments
```

## Phase 5: Runtime Integration Architecture

The frontend should not speak directly in visual details.

Use this pipeline:

```txt
Codex / App Events
-> Semantic Activity
-> Continuous Signals
-> Motion Controller
-> Visual Runtime
```

Example:

```txt
tool call started
-> working
-> toolActivity rises, load rises, focus medium
-> rim stabilizes, particles align, cilia activate
```

Example:

```txt
approval required
-> approval
-> urgency medium, toolActivity zero, focus high
-> breath slows, rim tightens, particles suspend
```

## Signal Sources

Do not rely only on LLM text.

Preferred sources:

| Source | Signal |
| --- | --- |
| user microphone / voice activity | `voiceEnergy`, `activity=listening` |
| text input active | `activity=listening`, low `voiceEnergy` |
| LLM response stream | `activity=responding`, speech envelope |
| Codex tool call start/end | `toolActivity`, `load`, `activity=working` |
| file edit/test/build events | `toolActivity`, `progress`, `confidence` |
| Obsidian search/write | `memoryActivity`, reflective route |
| calendar/Gmail/Drive requests | `toolActivity`, route depending on task |
| approval queue | `activity=approval`, `urgency` |
| errors/blocked permissions | `activity=interrupted`, `errorPressure` |

## Folder Structure

Recommended project structure:

```txt
assets/orb/
  references/
  lookdev/
    touchdesigner/
    blender/
    spline/
    shader/
  exports/
    base-loops/
    overlays/
    stills/
  manifests/
    orb-assets.json

docs/ai/current/
  Motion-Bible.md
  Lookdev-Asset-Pipeline.md
  Reference-Teardown.md
  Motion-System.md
  Visual-QA.md
```

## Asset Manifest Contract

Future runtime assets should be described, not hardcoded.

Example:

```json
{
  "id": "eden-orb-v1",
  "family": "black-core-organic-sphere",
  "baseLoop": "assets/orb/exports/base-loops/idle-reflective.webm",
  "fallbackStill": "assets/orb/exports/stills/idle-reflective.png",
  "blendMode": "screen",
  "states": ["idle", "listening", "thinking", "responding", "working", "approval", "interrupted"],
  "signals": ["arousal", "focus", "load", "voiceEnergy", "toolActivity", "memoryActivity", "errorPressure"]
}
```

## Implementation Status

Implemented on 2026-05-03:

- Created the `assets/orb/` source folder scaffold for references, lookdev work, exports, and manifests.
- Created the public runtime manifest at `public/assets/orb/manifests/orb-assets.json`.
- Added a typed manifest contract in `src/orb/orbAssets.ts`.
- Added a runtime-facing `OrbSignal` model in `src/types.ts`.
- Added `src/orb/orbSignals.ts` to map comparison presets into continuous signal profiles.
- Connected the current 18-button comparison harness through `OrbSignal` before rendering.
- Removed the canvas remount cut so route/activity changes can interpolate through the existing shader uniform controller.

Current production status:

```txt
Motion Bible: defined
Lookdev pipeline: scaffolded
Runtime signal bridge: implemented
Hero lookdev asset: not created yet
Prerender/WebGL overlay runtime: not integrated yet
TouchDesigner/Blender/Spline asset source: folder only
```

## QA Gates

### Visual QA

Check:

- still frame against reference
- 10-second idle loop
- speaking/responding loop
- working loop
- interrupted state
- visible canvas/video boundary
- black background blending
- glow banding
- compression artifacts

### Motion QA

Check:

- state transition inertia
- afterglow
- no obvious loop
- no fake progress
- no overactive idle
- response rhythm not too regular

### Runtime QA

Check:

- browser console
- nonblank canvas/video
- CPU/GPU load
- reduced-motion fallback
- asset loading fallback
- state signal logging

## Production Acceptance

The pipeline is working when:

- a locked reference board exists
- one hero visual direction is selected
- at least one high-quality lookdev loop exists
- the frontend can display the lookdev asset cleanly
- a WebGL overlay can react to continuous signals
- the orb can show at least idle, listening, responding, working, approval, interrupted
- visual QA is based on screenshots or video captures, not subjective memory

## Red Team Risks

### Real Risks

- the orb looks beautiful but cannot react to AI state
- the orb reacts but looks cheap
- asset export produces browser artifacts
- TouchDesigner/Blender workflow becomes too manual
- user keeps changing references before lookdev lock
- Codex keeps coding before visual target is settled

### Mitigations

- lock 3-5 references before implementation
- separate base visual from reactive overlay
- create small lookdev trials before full integration
- save every QA capture under `docs/ai/current/qa`
- reject any result that needs labels to be understood
- treat Codex as integrator and QA assistant, not sole motion designer

## Immediate Next Step

The next step is not another shader pass unless it is explicitly tied to a chosen lookdev direction.

The next step is:

```txt
Create a reference board and choose the first lookdev track:
TouchDesigner, Blender, Spline, or WebGL.
```

Recommended first experiment:

```txt
TouchDesigner lookdev for organic motion
+ WebGL overlay plan for runtime reaction
```
