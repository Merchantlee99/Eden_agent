# Orb State Model

Date: 2026-05-03
Status: Preset comparison model, not final runtime model

## Core Rule

The orb should feel like one continuous AI presence. It should not show visible Eden/Jarvis/Hybrid labels, and it should not use separate overlay badges for approval, error, or blocked states.

Instead:

```txt
route color family = work character
motion state = current activity
```

For comparison and QA, this creates:

```txt
3 route color families x 6 motion states = 18 core orb presets
```

Important:

The 18-preset matrix is a design/testing harness. It is not the final organic runtime model.

The final runtime model should be driven by continuous signals defined in `Motion-Bible.md`:

- `arousal`
- `focus`
- `load`
- `confidence`
- `urgency`
- `voiceEnergy`
- `toolActivity`
- `memoryActivity`
- `errorPressure`

## Route Color Families

| Family | Meaning | Visual Character |
| --- | --- | --- |
| Cyan / Violet | thinking, memory, daily context, calendar, Obsidian, reflective work | cool, luminous, stable, reflective |
| Rose / Blue | development, local files, GitHub, execution, automation | active, sharper, technical, energetic |
| Magenta / Electric | complex judgment, strategy, planning-to-execution handoff | synthetic, high-contrast, transitional |

These names are internal design references. They should not appear as user-facing mode names.

## Motion States

| State | Meaning | Motion Grammar |
| --- | --- | --- |
| Idle | ready but not actively working | slow breathing, stable organic motion |
| Responding | answering, narrating, explaining, speaking | speech-like volume pulse |
| Thinking | reasoning, comparing, remembering, checking assumptions | slower scan-like organic flow |
| Working | executing, editing, testing, fetching, updating | stronger output volume and driven movement |
| Approval | waiting for human confirmation before action | slowed motion and suspended tension |
| Interrupted | error or blocked flow | broken rhythm and visible flow break |

## Why Error And Blocked Are Combined

At the orb level, both error and blocked mean the same thing: the flow cannot continue normally.

The exact reason should be shown in:

- work stream
- execution log
- approval queue
- right status panel

The orb should only communicate that the system's flow is interrupted.

## 18 Preset Matrix

| Color Family | Idle | Responding | Thinking | Working | Approval | Interrupted |
| --- | --- | --- | --- | --- | --- | --- |
| Cyan / Violet | calm memory-ready idle | reflective answer pulse | context-gathering scan | note/calendar driven flow | quiet consent tension | soft broken context flow |
| Rose / Blue | execution-ready idle | implementation result pulse | code strategy scan | file/test/build driven flow | precise suspended tension | sharp broken-flow interruption |
| Magenta / Electric | strategy-ready idle | synthesis explanation pulse | complex judgment scan | planning-to-build color handoff | suspended decision glow | unstable split-flow interruption |

## Implementation Principle

Do not implement 18 unrelated animations.

Implement:

- 3 color presets
- 6 motion presets
- one continuous signal mixer
- one motion-memory system
- one interpolation/damping system

The renderer should combine them parametrically.

Example state shape:

```ts
type OrbRouteFamily = "reflective" | "execution" | "hybrid";

type OrbMotionState =
  | "idle"
  | "responding"
  | "thinking"
  | "working"
  | "approval"
  | "interrupted";

type OrbState = {
  route: OrbRouteFamily;
  motion: OrbMotionState;
  intensity: number;
  progress?: number;
  audioLevel?: number;
  contextLoad?: number;
  cause?: "none" | "approval" | "error" | "blocked";
};
```

## Transition Rule

State changes should be continuous.

Bad:

```txt
cyan thinking -> instant amber working cut
```

Good:

```txt
organic flow shifts -> volume profile changes -> hue moves -> activity intensity rises or falls
```

Recommended transition duration:

- small state change: 450ms to 700ms
- medium state change: 700ms to 1200ms
- major route change: 1200ms to 1800ms

Use shader uniform interpolation and spring-like easing, not hard class swaps.

See also:

- `Motion-Bible.md`
- `Lookdev-Asset-Pipeline.md`
