# Overlay Pet State Model

Date: 2026-05-03
Status: Canonical visual state model for the Swift-native Overlay Pet

## Core Rule

The Overlay Pet should feel like one continuous AI presence.

There is one external appearance:

```txt
one body
one silhouette
one face language
one material language
one animation grammar
```

Eden, Jarvis, and Hybrid remain internal routing concepts. They must not create separate visible characters, skins, badges, mode labels, or route-specific body forms.

The Pet communicates:

```txt
activity state = current system behavior
intensity = how much energy the system is using
attention/urgency = how much the user needs to notice
```

Important:

The previous 18-preset matrix was a temporary Overlay Pet comparison harness. It is not the final runtime model.

The final runtime model is one Overlay Pet driven by continuous signals:

- `arousal`
- `focus`
- `load`
- `confidence`
- `urgency`
- `voiceEnergy`
- `toolActivity`
- `memoryActivity`
- `errorPressure`

## Single Appearance Rule

| Allowed | Forbidden |
| --- | --- |
| same base Pet body in every mode | separate Eden/Jarvis/Hybrid bodies |
| same eyes/face system | route-specific face identity |
| same material and silhouette | separate skins, costumes, or route badges |
| activity-driven motion | mode-switch animation that looks like a different character |
| subtle intensity changes | route color families as primary visual identity |

Route may appear in logs, audit metadata, routing decisions, or detail panels. It should not be the Pet's external identity.

## Motion States

| State | Meaning | Motion Grammar |
| --- | --- | --- |
| Idle | ready but not actively working | slow breathing, stable organic motion |
| Responding | answering, narrating, explaining, speaking | speech-like volume pulse |
| Thinking | reasoning, comparing, remembering, checking assumptions | slower scan-like organic flow |
| Working | executing, editing, testing, fetching, updating | stronger output volume and driven movement |
| Approval | waiting for human confirmation before action | slowed motion and suspended tension |
| Blocked | error, denial, or blocked flow | compressed posture and visible flow break |

## Why Error And Blocked Are Combined

At the Pet level, error and blocked mean the same thing: the flow cannot continue normally.

The exact reason should be shown in:

- compact status
- approval surface
- work stream or detail panel
- audit/event log

The Pet should communicate that the system's flow is blocked, not explain the full cause through body shape.

## State Matrix

| Single Pet Appearance | Idle | Responding | Thinking | Working | Approval | Blocked |
| --- | --- | --- | --- | --- | --- | --- |
| Eden Overlay Pet | calm available presence | speech/text pulse | inward focus scan | active tool/work motion | held consent tension | compressed blocked rhythm |

## Implementation Principle

Do not implement route-specific visual variants.

Implement:

- 1 base Pet identity
- 6-8 activity states
- one continuous signal mixer
- one motion-memory system
- one interpolation/damping system

The renderer should combine activity, urgency, confidence, tool activity, memory activity, voice energy, decision pressure, and error pressure parametrically.

Example state shape:

```ts
type OverlayPetActivity =
  | "idle"
  | "listening"
  | "responding"
  | "thinking"
  | "working"
  | "approval"
  | "blocked"
  | "done";

type OverlayPetVisualState = {
  activity: OverlayPetActivity;
  intensity: number;
  progress?: number;
  audioLevel?: number;
  contextLoad?: number;
  decisionPressure?: number;
  errorPressure?: number;
  cause?: "none" | "approval" | "error" | "blocked";
};
```

## Transition Rule

State changes should be continuous.

Bad:

```txt
thinking face -> instant different Jarvis character
```

Good:

```txt
same Pet identity -> posture shifts -> glow/intensity changes -> activity rhythm changes
```

Recommended transition duration:

- small state change: 450ms to 700ms
- medium state change: 700ms to 1200ms
- major activity change: 1200ms to 1800ms

Use animation-state interpolation and spring-like easing, not hard sprite or class swaps.

See also:

- `Motion-Bible.md`
- `Lookdev-Asset-Pipeline.md`
- `Swift_Native_Codex_Pet_Blueprint.md`
