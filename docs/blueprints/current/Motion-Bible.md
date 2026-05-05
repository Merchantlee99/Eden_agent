# Eden Overlay Pet Motion Bible

Date: 2026-05-03
Status: Production direction baseline

## Purpose

This document replaces the previous "keep coding the Overlay Pet until it looks good" approach.

The target is not a functional status widget. The target is a living AI presence with Dribbble-grade fluidity, organic continuity, and state-reactive behavior.

The Overlay Pet must feel like:

- an intelligent presence
- a living energy core
- a real-time state instrument
- a quiet operational companion

It must not feel like:

- a generic AI blob
- a loading spinner
- a decorative WebGL demo
- a mode label with glow
- a dashboard ornament

## Non-Negotiable Outcome

The user should be able to glance at the Overlay Pet and feel:

```txt
It is listening.
It is thinking.
It is speaking.
It is working.
It is waiting for me.
It is blocked.
```

The user should not need to read a label to understand the broad state.

## Visual Identity

### Form

Primary form:

- black-core sphere
- luminous organic membrane
- particle field bound to the sphere
- diagonal synaptic energy wave
- hot rim accents
- outer cilia / corona
- volumetric glow in dark negative space

Reject:

- flat CSS circles
- generic purple-blue blobs
- torus-heavy sci-fi geometry
- flower-like soft blobs
- visible rectangular video or canvas boundaries
- fully filled pearl/glass balls without a dark core

### Material

The Overlay Pet is not made of glass, metal, smoke, or water.

It should feel like a semi-biological energy membrane:

- the center absorbs light
- the edge emits light
- the shell breathes
- the particles circulate
- the corona reacts like a nervous system

### Light

Light must be layered:

1. inner low glow
2. hot rim bloom
3. diagonal synapse trail
4. external cilia glow
5. wide volumetric aura

Avoid one large blur pretending to be glow.

## Motion Principles

### 1. Organic Motion Is Layered Timing

Organic animation is not random movement.

It needs several time scales running together:

| Layer | Timing | Role |
| --- | --- | --- |
| Breath | 4s-8s | life, readiness, baseline presence |
| Circulation | 2s-6s | internal processing and continuity |
| Speech pulse | 80ms-280ms | responding and voice-like rhythm |
| Micro tremor | 60ms-180ms | alive surface detail |
| Event surge | 300ms-900ms | state change, tool call, approval, error |
| Afterglow | 700ms-2400ms | memory of the previous state |

### 2. State Changes Need Memory

Bad:

```txt
idle -> instant working preset
```

Good:

```txt
idle breath tightens
rim brightens
particles align
outer corona activates
working circulation takes over
previous idle glow decays slowly
```

The Overlay Pet should carry inertia from the previous state.

### 3. No Perfect Repetition

Loops must not reveal an obvious cycle.

Use:

- different loop lengths per layer
- phase offsets
- non-uniform particle density
- slow drift
- low-amplitude noise
- occasional rare sparks

Avoid:

- all layers pulsing together
- perfectly even rays
- evenly spaced dots that look like UI ticks
- obvious sine-wave breathing only

### 4. Motion Must Map To Meaning

Do not animate only because it looks impressive.

Each layer has semantic responsibility:

| Layer | Meaning |
| --- | --- |
| Core darkness | depth, concentration, latent intelligence |
| Membrane deformation | aliveness, stress, attention |
| Rim brightness | current energy and confidence |
| Particle lattice | context search, memory, reasoning, data flow |
| Diagonal wave | speech, insight, active thought current |
| Outer cilia | sensing, tool activity, external connections |
| Wide aura | system arousal and attention |

## Continuous Signal Model

The previous 18-button route matrix is deprecated. Current comparison should use one Pet identity with activity-state controls.

The final runtime must use continuous signals:

```ts
type PetSignal = {
  route: "eden" | "jarvis" | "hybrid";
  routeScores?: {
    eden: number;
    jarvis: number;
    hybrid: number;
  };
  activity:
    | "idle"
    | "listening"
    | "thinking"
    | "responding"
    | "working"
    | "approval"
    | "blocked"
    | "done";
  arousal: number;       // 0..1, overall system energy
  focus: number;         // 0..1, concentration / inward pull
  load: number;          // 0..1, context or tool workload
  confidence: number;    // 0..1, stability of current answer/action
  urgency: number;       // 0..1, needs user attention
  voiceEnergy: number;   // 0..1, speaking/listening rhythm
  toolActivity: number;  // 0..1, real execution activity
  memoryActivity: number;// 0..1, Obsidian/context retrieval
  errorPressure: number; // 0..1, blocked/error stress
};
```

`route` is metadata. It is not a visual identity selector. The visible Overlay Pet remains one appearance across Eden, Jarvis, and Hybrid routing.

Discrete state chooses the motion family. Continuous signals shape the body.

Implementation note:

- `PetSignal` is now implemented in the frontend type model.
- The comparison harness now routes presets through continuous signal profiles.
- The current renderer still adapts `PetSignal` into the existing shader state; direct full-signal shader control remains a later production step.

## State Grammar

### Idle

Feeling:

- alive but quiet
- ready
- not pretending to work

Motion:

- slow breath
- low particle drift
- low outer cilia
- subtle diagonal current
- long afterglow from previous task

Failure mode:

- if too active, it feels dishonest
- if too static, it feels dead

### Listening

Feeling:

- receptive
- open
- sensitive to user input

Motion:

- membrane opens slightly
- outer cilia become more visible
- particles face inward
- voiceEnergy reacts to microphone/text input
- rim is not yet bright like responding

Failure mode:

- if it looks like speaking, the user will think the AI is interrupting

### Thinking

Feeling:

- inward concentration
- evaluating, recalling, checking

Motion:

- darker core grows slightly
- particle field condenses
- diagonal wave slows
- rim brightness lowers but sharpens
- outer corona reduces

Failure mode:

- if motion is too fast, it reads as working, not thinking

### Responding

Feeling:

- speaking, narrating, explaining
- energy leaves the core toward the user

Motion:

- voice-like pulse
- diagonal synapse becomes strong
- rim flashes with syllable-like rhythm
- particles ripple outward
- wide aura rises and falls with speech envelope

Failure mode:

- if response pulse is regular, it feels fake

### Working

Feeling:

- real execution
- files, tools, calendars, search, tests, GitHub, Obsidian

Motion:

- outer cilia and circulation become directional
- rim becomes brighter and more stable
- particles align into flow
- progress can be implied by rotating energy, not a literal progress bar

Failure mode:

- if it looks like generic progress, the intelligence disappears

### Approval

Feeling:

- the system is holding
- user decision is required
- nothing irreversible is happening

Motion:

- breath slows
- rim tightens
- particles suspend
- aura contracts
- tension without alarm

Failure mode:

- if it looks like an error, approvals become stressful

### Blocked

Feeling:

- flow is blocked
- something needs attention
- not catastrophic by default

Motion:

- membrane stress
- broken wave
- short brightness stutter
- particles lose alignment
- errorPressure affects fracture intensity

Failure mode:

- if too red or violent, every minor blocker feels like a crash

## Internal Route Semantics

Route is not a visible mode label, skin, badge, or color family. It exists for routing, audit, task wording, and detail/debug panels.

| Route | Meaning | Allowed User-Visible Treatment |
| --- | --- | --- |
| Eden | memory, schedule, thinking, Obsidian | same Pet identity; reflective wording if needed |
| Jarvis | coding, local files, GitHub, tools | same Pet identity; execution wording if needed |
| Hybrid | planning-to-execution, strategy, synthesis | same Pet identity; synthesis wording if needed |

Forbidden:

- route-specific Pet bodies
- route-specific skins
- route color families as primary identity
- visible Eden/Jarvis/Hybrid labels on the Pet

## Layer Response Matrix

| Signal | Core | Particles | Rim | Synapse | Cilia | Aura |
| --- | --- | --- | --- | --- | --- | --- |
| arousal | small contraction | density up | brightness up | speed up | length up | width up |
| focus | darker center | inward flow | sharper edge | slower but brighter | reduced | narrower |
| load | deeper field | more layers | stable | moderate | tool pulses | medium |
| confidence | stable | ordered | clean rim | clean path | low noise | smooth |
| urgency | slight tension | blocked flow | sharper highlight | short pulse | spikes | tighter |
| voiceEnergy | minimal | ripple | syllable pulse | strong wave | low-mid | breathing pulse |
| toolActivity | minimal | directional flow | strong stable rim | moderate | strong | steady |
| memoryActivity | deeper core | context lattice | soft | slow current | low | cool glow |
| errorPressure | center wobble | broken alignment | flicker | fracture | jagged | unstable |

## Transition Rules

### Allowed Transition Pattern

```txt
detect event
classify activity
raise continuous signals
blend visual layers
decay previous state
settle into new baseline
```

### Timing

| Transition | Duration |
| --- | --- |
| idle -> listening | 300ms-700ms |
| listening -> thinking | 500ms-1000ms |
| thinking -> responding | 600ms-1200ms |
| thinking -> working | 700ms-1400ms |
| working -> approval | 500ms-900ms |
| working -> blocked | 150ms-450ms |
| blocked -> idle | 900ms-2200ms |

### Easing

Use:

- smooth exponential damping for signal changes
- spring-like response for membrane and cilia
- non-linear speech envelope for responding
- slow decay for afterglow

Avoid:

- CSS class swaps for Overlay Pet state
- hard remount as final runtime model
- all uniforms interpolating at the same speed

## Acceptance Criteria

The motion direction is acceptable only when:

- the idle still frame looks premium
- 10 seconds of idle does not reveal a cheap loop
- listening and responding are visually distinguishable
- thinking feels inward and slower than working
- working feels like real execution, not a generic loader
- approval feels suspended, not broken
- blocked feels blocked, not catastrophic
- route changes do not change Pet identity; activity and intensity carry visible meaning
- state changes carry inertia and afterglow
- the Overlay Pet remains the only signature motion object

## Red Team Checklist

Reject the result if:

- it looks like a screensaver
- it looks like a particle tutorial
- it needs labels to be understood
- it is beautiful but unrelated to AI state
- it is reactive but visually cheap
- it is too active while idle
- it claims progress when no work is happening
- it cannot be compared side-by-side with references
- it cannot survive a 10-second video review

## References For Production Logic

Use these as conceptual references, not as final visual dependencies:

- Rive state machines: designer-authored animation states and transitions
- TouchDesigner: real-time procedural visual lookdev
- Three.js ShaderMaterial: runtime uniform-driven WebGL control
- Theatre.js / GSAP: authored timing and variable choreography
