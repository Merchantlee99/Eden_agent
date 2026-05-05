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
| Overlay Pet minor state shift | 450ms-700ms |
| Overlay Pet medium state shift | 700ms-1200ms |
| Overlay Pet major activity shift | 1200ms-1800ms |
| ambient loop | 8s-18s |

## Easing

Use:

- standard UI: `cubic-bezier(0.2, 0.8, 0.2, 1)`
- precise/technical: `cubic-bezier(0.16, 1, 0.3, 1)`
- error/blocked: sharper ease-out, no bounce
- Overlay Pet transitions: spring or shader uniform interpolation

Avoid:

- linear motion except for constant ambient rotation
- bounce on serious/operational UI
- simultaneous unrelated animations

## Overlay Pet State Rule

The 18 route-preset model is deprecated.

```txt
1 Overlay Pet identity x runtime activity states
```

Implemented redesign direction:

- Overlay Pet family: ReferenceSphere, locally owned and Eden-customized
- UI shell motion: removed for this phase except activity comparison controls
- Overlay Pet motion: owned R3F/GLSL shader with state-driven uniforms and synthetic audio envelope
- Panel motion: out of scope

The Overlay Pet should be the only signature motion object in the first viewport.

Production note:

The current WebGL Overlay Pet is a prototype and comparison harness. The production direction is now:

```txt
Motion-Bible.md
-> Lookdev-Asset-Pipeline.md
-> selected lookdev asset
-> runtime WebGL/state overlay
```

The final Overlay Pet should not be judged by the current shader alone.

## Overlay Pet Rendering Logic

The current Overlay Pet is a real-time WebGL instrument, not a prerendered asset.

- Base: owned `ReferenceSphereOrb` shader.
- Renderer: Three.js/R3F plane shader that renders a spherical illusion.
- Structure: black core, particle lattice, diagonal internal wave, hot rim, outer corona.
- Customization: one Pet identity drives rim, lattice, hot highlights, and halo.
- Motion control: each activity state drives pulse, speed, density, fracture, progress, and synthetic audio uniforms.
- Speaking/texting: responding state uses higher, faster synthetic audio modulation.
- Halo: shader fake-bloom, CSS drop glow, rim bloom, close halo, wide halo, and radial cilia are separated.
- Transition: state comparison now keeps one R3F canvas alive and interpolates shader uniforms through the internal state ref. This preserves activity correctness while avoiding hard canvas remount cuts.

## Motion Bible Runtime Bridge

Implemented bridge:

- `PetSignal` is now the canonical runtime-facing state shape.
- Comparison controls create continuous `PetSignal` presets before being translated into the current shader state.
- Route remains metadata and must not select a different visual identity.
- `listening` and `done` exist in the signal model even if early comparison controls focus on fewer states.
- The Overlay Pet exposes `data-pet-activity` for QA and may expose route metadata only for debug/audit views.

Current bridge limit:

- The shader still receives a legacy `PetVisualState` adapter. The next production pass should move more signal values directly into visual uniforms instead of compressing them into `intensity`, `progress`, `audioLevel`, and `contextLoad`.

## Layered Animation Model

The Overlay Pet is treated as stacked motion layers inside one shader:

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
- Blocked: fracture streaks and broken pulse layered over the rim.

## State Semantics

External appearance rule:

- One Overlay Pet body communicates all work.
- Eden/Jarvis/Hybrid are internal route metadata.
- Route must not create separate color families, skins, bodies, badges, or visible actor labels.

Motion communicates activity:

- Idle: slow breathing, stable rim, low-density lattice.
- Responding: stronger synthetic speech modulation and brighter internal wave.
- Thinking: slower scan-like modulation and denser lattice.
- Working: brighter rim and progress arc behavior.
- Approval: low-volume held tension.
- Blocked: broken pulse and fracture behavior.

## QA Requirements

For motion-heavy work:

- screenshot at 390, 768, and 1440 widths
- no blank canvas
- no unreadable text
- no hidden approval controls
- check reduced motion
- check at least 10 seconds of loop behavior
- record whether the animation is functional, atmospheric, or excessive
