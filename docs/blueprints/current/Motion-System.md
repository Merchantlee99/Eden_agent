# Motion System

Date: 2026-05-03
Status: Current WebGL prototype, superseded for production by Motion Bible

## Motion Principles

- Motion must communicate system state.
- One viewport should have one signature motion object.
- UI panels should use restrained micro-interactions.
- Large animation should never hide approvals, logs, or controls.
- State changes should interpolate, not cut.
- Reduced-motion support is mandatory.

## Timing Tokens

| Use | Duration |
| --- | --- |
| hover/focus | 120ms-220ms |
| small UI transition | 180ms-280ms |
| panel enter/exit | 260ms-450ms |
| orb minor state shift | 450ms-700ms |
| orb medium state shift | 700ms-1200ms |
| orb major route shift | 1200ms-1800ms |
| ambient loop | 8s-18s |

## Easing

Use:

- standard UI: `cubic-bezier(0.2, 0.8, 0.2, 1)`
- precise/technical: `cubic-bezier(0.16, 1, 0.3, 1)`
- error/interrupted: sharper ease-out, no bounce
- orb transitions: spring or shader uniform interpolation

Avoid:

- linear motion except for constant ambient rotation
- bounce on serious/operational UI
- simultaneous unrelated animations

## Orb State Rule

Keep the 18 preset model:

```txt
3 route color families x 6 motion states
```

Implemented redesign direction:

- Orb family: ReferenceSphere, locally owned and Eden-customized
- UI shell motion: removed for this phase except 18 comparison buttons
- Orb motion: owned R3F/GLSL shader with state-driven uniforms and synthetic audio envelope
- Panel motion: out of scope

The orb should be the only signature motion object in the first viewport.

Production note:

The current WebGL orb is a prototype and comparison harness. The production direction is now:

```txt
Motion-Bible.md
-> Lookdev-Asset-Pipeline.md
-> selected lookdev asset
-> runtime WebGL/state overlay
```

The final orb should not be judged by the current shader alone.

## Orb Rendering Logic

The current orb is a real-time WebGL instrument, not a prerendered asset.

- Base: owned `ReferenceSphereOrb` shader.
- Renderer: Three.js/R3F plane shader that renders a spherical illusion.
- Structure: black core, particle lattice, diagonal internal wave, hot rim, outer corona.
- Customization: Eden route colors drive rim, lattice, hot highlights, and halo.
- Motion control: each Eden motion state drives pulse, speed, density, fracture, progress, and synthetic audio uniforms.
- Speaking/texting: responding state uses higher, faster synthetic audio modulation.
- Halo: shader fake-bloom, CSS drop glow, rim bloom, close halo, wide halo, and radial cilia are separated.
- Transition: state comparison now keeps one R3F canvas alive and interpolates shader uniforms through the internal state ref. This preserves route/activity correctness while avoiding hard canvas remount cuts.

## Motion Bible Runtime Bridge

Implemented bridge:

- `OrbSignal` is now the canonical runtime-facing state shape.
- The 18 comparison buttons still exist, but they now create continuous `OrbSignal` presets before being translated into the current shader state.
- Route bias adjusts the signal profile instead of hardcoding every visual value per button.
- `listening` exists in the signal model even though it is not part of the 18-button comparison matrix yet.
- The orb exposes `data-orb-route` and `data-orb-activity` for QA and future runtime routing.

Current bridge limit:

- The shader still receives a legacy `OrbState` adapter. The next production pass should move more signal values directly into visual uniforms instead of compressing them into `intensity`, `progress`, `audioLevel`, and `contextLoad`.

## Layered Animation Model

The orb is treated as stacked motion layers inside one shader:

| Layer | Visual Role | Animation Logic | State Inputs |
| --- | --- | --- | --- |
| Core | black center and depth anchor | nearly static, only affected by global breathing scale | `uPulse`, `uAudioLevel` |
| Surface lattice | sphere-bound point field | longitude/latitude grid drifts with time; a second parallax lattice moves on screen-space rotation | `uDensity`, `uSpeed`, `uIntensity` |
| Diagonal wave | bright internal curve crossing the sphere | curved line oscillates, dotted wave head travels across the path | `uWavePower`, `uPulse`, `uAudioLevel` |
| Living membrane | slightly imperfect sphere boundary | noise-deformed edge and breathing scale create non-mechanical movement | `uLifeForce`, `uFracture`, `uAudioLevel` |
| Hot rim | luminous outer sphere edge | rim arcs rotate slowly; micro-sparks crawl along the edge | `uRimSharpness`, `uIntensity`, `uAudioLevel`, `uBloomPower` |
| Cilia / sheath | organic outer hairline aura | irregular radial rays, partial plasma sheaths, and sparse orbit dust avoid perfect UI rings | `uCiliaPower`, `uOuterPower`, `uSpeed` |
| Corona | volumetric outer glow | close halo, wide halo, ray noise, and sparse dots breathe around the sphere | `uCoronaPower`, `uBloomPower`, `uAudioLevel`, `uIntensity` |

Expected motion:

- Idle: slow breath, subtle lattice drift, visible diagonal synapse, restrained cilia.
- Responding: stronger breath, faster diagonal wave, brighter corona and speech-like pulse.
- Thinking: denser lattice with slower scan.
- Working: active rim/progress behavior and stronger external cilia/sheath.
- Approval: slowed and held outer circle tension.
- Interrupted: fracture streaks and broken pulse layered over the rim.

## State Semantics

Color family communicates responsibility:

- Cyan / Violet: reflective context, memory, calendar, Obsidian.
- Rose / Blue: execution, development, files, GitHub.
- Magenta / Electric: hybrid synthesis, strategy-to-execution bridge.

Motion communicates activity:

- Idle: slow breathing, stable rim, low-density lattice.
- Responding: stronger synthetic speech modulation and brighter internal wave.
- Thinking: slower scan-like modulation and denser lattice.
- Working: brighter rim and progress arc behavior.
- Approval: low-volume held tension.
- Interrupted: broken pulse and fracture behavior.

## QA Requirements

For motion-heavy work:

- screenshot at 390, 768, and 1440 widths
- no blank canvas
- no unreadable text
- no hidden approval controls
- check reduced motion
- check at least 10 seconds of loop behavior
- record whether the animation is functional, atmospheric, or excessive
