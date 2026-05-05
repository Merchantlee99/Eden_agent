# Reference Teardown

Date: 2026-05-03
Status: Organic glow implementation applied

## Purpose

The next Eden Front redesign should not start from code.

It should start by decomposing visual references into explicit design properties. This avoids generic AI UI output and makes Codex implementation more controllable.

## Local Video Reference Read

Reference files now driving implementation:

- `/Users/isanginn/Desktop/50334c5c05719cf504253211866bc8cd (1).mp4`
- `/Users/isanginn/Desktop/original-6433de79a34f799bf4a634cbbdda7967 (1).mp4`
- `/Users/isanginn/Desktop/1d6225926b6e7669a48071fa8fbbb470.mp4`

Observed traits to adopt:

- black negative space and black/dark center core
- black-core spherical silhouette
- cyan/magenta/blue luminous rim with white-hot highlights
- subtle glass shell and soft outer corona
- localized bright white rim highlights
- particle lattice bound to the sphere surface
- diagonal internal wave crossing the orb
- thin external orbit circle around the sphere
- sparse corona particles and radial hairline aura
- state changes through rim brightness, pulse, lattice density, progress arc, and fracture behavior
- organic glow built from separated rim bloom, close halo, wide halo, and cilia-like corona

Observed traits to reject:

- visible rectangular video/canvas boundary
- label-heavy internal state readouts
- multiple UI panels competing with the orb
- hard color cuts between states
- generic purple-blue gradient as the whole design language
- filled pearl-sphere layers from the previous pass
- flower/blob orb shapes that do not match the new reference
- mechanical 3D torus geometry

## Orb Families To Choose From

Pick one primary family:

| Family | Description | Risk |
| --- | --- | --- |
| Liquid | soft, organic, fluid surface | can feel decorative or wellness-like |
| Plasma | energetic, luminous, reactive | can feel generic AI/crypto |
| Glass | premium, refractive, optical | hard to render well in realtime |
| Energy Core | powerful central intelligence | can become too game/sci-fi |
| Reference Sphere | black core, particle lattice, hot rim, corona | needs careful shader tuning |

## Current Redesign Direction

Primary family: Reference Sphere.

Rationale:

- The provided `original-6433...` reference is a particle-lattice energy sphere, not a Siri-style blob.
- SmoothUI is useful for dot/blur/contrast ideas, but it is not a true 3D sphere renderer.
- voiceorb is the closest technical reference because it uses Three.js/GLSL, audio state, Fresnel edges, and shader displacement.
- ReactBits Orb is useful for hue and active distortion ideas, but OGL was not added because this app already uses Three.js/R3F.
- Eden can now customize route colors and motion behavior from an owned shader without depending on a third-party orb primitive.
- State meaning should come from color and motion intensity, not labels inside the orb.

Adopt:

- dark negative space for the app surface
- black-core spherical orb as the visual protagonist
- one signature orb
- route colors mapped into shader rim, lattice, and corona colors
- motion states mapped into pulse, speed, density, fracture, and synthetic audio envelope
- soft halo as support, not as a competing second orb
- imperfect living membrane rather than a perfectly mechanical circle
- status as instrument, not label-heavy UI

Reject:

- busy SaaS dashboard cards
- large visible mode labels
- old ring/torus/blob experiments
- free-floating particle fields detached from the sphere surface
- purple-blue gradient dominance
- multiple competing animated effects
- using third-party reference videos as app assets
- postprocessing bloom when it creates a visible rectangular canvas boundary

## Adoption Matrix

For each selected reference:

| Reference | Adopt | Adapt | Reject |
| --- | --- | --- | --- |
| `50334... (1)` basic state | dark core, glow shell, restrained halo | support direction only | filled pearl sphere |
| `original-6433... (1)` basic reinforcement | black-core presence, particle lattice, diagonal wave, bright rim glints, outer corona | primary idle/base shader direction | overbuilt 3D torus stack |
| `1d622...` speaking/texting | stronger pulse and faster modulation | responding-only motion profile | always-on activity dots |
| SmoothUI Siri Orb | CSS dot mask, blur/contrast, smooth loop ideas | reference only; no direct dependency | using it as final orb |
| shadcn-style app surfaces | restrained controls, accessible primitives, dense panels | use local owned components for current Vite app | default library look |
| voiceorb | Three.js/GLSL, state model, audio-reactive logic, Fresnel edge thinking | absorb technical logic into owned R3F shader | copying its visual palette |
| ReactBits Orb | hue rotation, active distortion, background blending ideas | port concepts into Three.js/R3F only if needed | adding OGL as a second renderer |

## Red Team Questions

- Does this visual feel specific to Eden?
- Does it still work without glow?
- Does it clarify state or just decorate?
- Would it look outdated in a year?
- Does it survive mobile?
- Does it make the operational UI harder to read?
