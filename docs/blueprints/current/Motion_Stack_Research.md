# Motion Stack Research

Date: 2026-05-03
Status: Superseded by Motion Bible + Lookdev Asset Pipeline

## Conclusion

For Dribbble-level orb work, do not rely on generic CSS, simple canvas particles, or a single prompt.

The practical path is:

```txt
Lookdev first
-> motion graphics asset or visual target
-> web reproduction
-> interactive state overlay
-> QA loop
```

Production direction now lives in:

- `Motion-Bible.md`
- `Lookdev-Asset-Pipeline.md`

This document remains as the tool-role research baseline.

## Tool Roles

| Tool | Best Use | Eden Orb Fit |
| --- | --- | --- |
| Three.js / R3F / GLSL | realtime 3D, shader, particle, state-reactive graphics | high |
| Blender | high-fidelity lookdev, lighting, material, prerendered loop | high |
| TouchDesigner | realtime generative motion, audio-reactive visuals, feedback loops | high |
| Spline | fast browser-based 3D prototyping and embeddable scenes | medium-high |
| GSAP | timeline, sequencing, scroll, uniform/camera orchestration | high |
| Theatre.js | browser-based keyframe editing for Three.js variables | high |
| Motion | React UI micro-interactions and layout animation | high for UI, medium for orb |
| Rive | stateful vector/2D UI motion | medium for indicators, low for volumetric orb |
| dotLottie | lightweight vector animation playback | medium for micro-motion, low for volumetric orb |
| Shader Park | shader idea sketching and SDF exploration | medium-high for prototyping |

## Real-Time Shader Path

Pros:

- responds directly to state, pointer, audio, and command flow
- no large video assets
- infinite variation
- strong fit for "living AI presence"

Cons:

- high visual quality requires shader/lookdev skill
- mobile GPU risk
- browser differences
- QA burden is high

Use when:

- state responsiveness matters more than optical perfection
- the team can iterate shader parameters with screenshot/video QA

## Prerender + WebGL Overlay Path

Pros:

- fastest way to high optical quality
- Blender/TouchDesigner can create stronger material, glow, and depth
- predictable playback
- easier mobile fallback

Cons:

- less interactive
- asset pipeline and video encoding complexity
- alpha/fallback differences across browsers

Use when:

- the first impression must look premium quickly
- interaction can be approximated through overlay rings, distortion, light sweeps, and particles

## Recommended Eden Path

Updated recommendation:

```txt
Motion Bible
-> reference lock
-> TouchDesigner / Blender / Spline / WebGL lookdev experiments
-> select one hero direction
-> integrate as hybrid runtime asset
-> connect continuous AI state signals
```

Phase 1:

- reference teardown
- choose one orb family
- create `Orb Lookdev Brief`
- prototype either Blender/Spline/TouchDesigner look or a high-quality R3F shader sample

Phase 2:

- compare realtime vs prerender on desktop/mobile
- keep only one signature orb direction
- rebuild Eden Front around that motion centerpiece

Phase 3:

- connect orb state to real system state
- add reduced-motion and low-power fallback
- perform screenshot and 10-30 second motion QA

## What Codex Can Do

Codex can:

- scaffold R3F/Three.js architecture
- write shader prototypes
- create state/uniform systems
- integrate GSAP/Theatre/Motion
- write asset manifests and fallbacks
- run browser screenshots and pixel checks
- generate Blender Python scripts if Blender is installed

Codex should not be trusted alone for:

- final taste judgment
- choosing the best reference
- deciding whether the result feels "Eden"
- licensing or paid asset decisions
- real-device visual approval
