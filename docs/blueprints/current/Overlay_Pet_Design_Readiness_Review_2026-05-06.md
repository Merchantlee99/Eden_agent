# Overlay Pet Design Readiness Review

Date: 2026-05-06
Scope:

- `Swift_Native_Codex_Pet_Blueprint.md`
- `Eden_Jarvis_Final_Blueprint.md`
- `Overlay_Pet_State_Model.md`
- `Motion-Bible.md`
- `Lookdev-Asset-Pipeline.md`
- `Design-System.md`
- `UI-UX-Brief.md`
- `UI-Review.md`
- `Visual-QA.md`

## Verdict

Status: ready to proceed to external appearance design.

The architecture now supports one user-facing Overlay Pet identity. Eden, Jarvis, and Hybrid remain internal routes and must not create separate visible bodies, skins, route colors, badges, or mode labels.

## Review Findings

### Finding 1: Motion Bible route schema drift

Severity: P2

Issue:

`Motion-Bible.md` still used `reflective | execution | hybrid` as route values while the Swift Pet and final blueprint use `eden | jarvis | hybrid`.

Risk:

If left unresolved, asset naming, PetSignal generation, and route metadata could diverge between Swift, Gateway, and motion runtime.

Fix:

- Updated `PetSignal.route` to `eden | jarvis | hybrid`.
- Updated `routeScores` to `eden`, `jarvis`, and `hybrid`.
- Replaced route color family guidance with internal route semantics.
- Re-stated that route is metadata and not a visual identity selector.

Status: closed.

### Finding 2: Lookdev manifest still implied route-flavored base assets

Severity: P3

Issue:

The sample manifest used names like `idle-reflective`.

Risk:

This could encourage route-specific asset variants even though the desired direction is one Pet identity.

Fix:

- Updated sample asset names to `idle-base`.
- Updated signal source wording to `route=eden` metadata where needed.

Status: closed.

## Current Canonical Rules

These rules are now safe to use for the appearance design phase:

```txt
1. The user sees one Overlay Pet.
2. Eden, Jarvis, and Hybrid are internal routes only.
3. route and routeScores are metadata, not skin selectors.
4. Pet appearance changes by activity, intensity, posture, glow, and expression.
5. No route-specific bodies, costumes, color families, badges, or mode labels.
6. The Pet must read clearly at 72px, 96px, and 128px.
7. The Pet should work first as still identity, then as state animation.
```

## Design Phase Gate

Appearance design may proceed if the next step produces these artifacts:

```txt
Overlay_Pet_Style_Guide.md
Overlay_Pet_Image_Prompt_Pack.md
assets/overlay-pet/concepts/
assets/overlay-pet/states/
assets/overlay-pet/exports/
```

Recommended first visual batch:

```txt
12-20 static concept candidates
1 external silhouette only
transparent background
96px legibility test
idle / listening / thinking / working / approval / blocked / done expression sheet after one candidate is chosen
```

## GPT Image Readiness

GPT Image can be used for the appearance phase.

Recommended use:

- generate concept candidates
- explore silhouette, face language, material, and glow direction
- create transparent-background stills
- create expression sheets after a candidate is chosen

Do not use GPT Image as the runtime animation system. Runtime animation should still be handled by Rive, SpriteKit, SwiftUI/AppKit, or Metal/SpriteKit depending on the chosen visual style.

## Final Decision

Proceed to appearance design.

Do not start Swift implementation yet except for a placeholder Pet shell. The next high-leverage step is to lock the Pet's visual identity with generated concept candidates and a style guide.
