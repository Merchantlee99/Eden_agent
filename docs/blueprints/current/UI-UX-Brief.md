# Eden Front UI/UX Brief

Date: 2026-05-03
Status: Planning baseline

## Product Type

Personal AI command surface for thinking, memory, development, scheduling, and controlled automation.

This should feel like a quiet operational console, not a landing page, not a generic chatbot, and not a decorative science-fiction mockup.

## User Goal

The user should be able to speak or type a request into one interface and understand:

- what the system is doing
- which context it is using
- whether it is thinking, verifying, building, waiting, or executing
- what actions need approval
- what has already happened

## Key UX Decision

There is no visible Eden/Jarvis mode switch, and the center panel should not show visible labels such as Eden, Jarvis, or Hybrid.

The front presents one continuous command surface. Eden, Jarvis, and Hybrid are internal actor states decided by routing, context, and task type.

The user should not need to think:

- "Should I switch to Eden?"
- "Should I switch to Jarvis?"
- "Is this a Hybrid task?"

The UI should instead communicate:

- current activity through the Overlay Pet's motion, posture, glow, density, pulse rhythm, and tension
- current activity
- current context
- current permission level
- current blockers

## First Screen Layout

```txt
┌────────────────────────────────────────────────────────────────────┐
│ Top status rail: identity, current task, permission profile         │
├───────────────────────────────────────────┬────────────────────────┤
│                                           │ Right Status Panel      │
│                                           │ - Connections           │
│             Central Status Overlay Pet            │ - Active context        │
│                                           │ - Memory candidates     │
│                                           │ - Thread registry       │
│                                           │ - Calendar snapshot     │
├───────────────────────────────────────────┴────────────────────────┤
│ Bottom Command Dock                                                │
│ - Conversation                                                     │
│ - Work stream                                                      │
│ - Execution log                                                    │
│ - Approval queue                                                   │
└────────────────────────────────────────────────────────────────────┘
```

## Central Status Overlay Pet

The Overlay Pet is the system presence and state indicator. It is not just decoration.

It should express six motion states:

- idle
- responding
- thinking
- working
- approval
- blocked

The Overlay Pet can encode state through:

- motion speed
- color accent
- volume-like expansion/contraction
- organic flow density
- pulse rhythm
- confidence or verification state

The Overlay Pet should not display the internal actor name or change into a route-specific body.

Motion state should be separate from internal route:

- idle: slow breathing, low glow, stable organic motion
- responding: speech-like volume pulse
- thinking: slower scan-like organic flow
- working: higher output volume and driven movement
- approval: slowed motion, suspended tension
- blocked: broken rhythm and visible flow break

Blocked covers both errors and blocked work at the Overlay Pet level. The exact reason should appear in the work stream, execution log, or right status panel, not as a separate Overlay Pet family.

If text appears near the Overlay Pet, it should describe the task state, not the internal actor name.

Avoid:

- excessive surface noise that hides state
- constant visual noise
- animation that implies progress when no work is happening
- making the Overlay Pet the only place where state is communicated

## Bottom Command Dock

The bottom area is the main working surface.

It contains:

- conversation input
- work stream
- execution log
- approval queue

Recommended behavior:

- conversation stays visible
- work stream shows human-readable progress
- execution log is compact and expandable
- approval queue is visually distinct and never hidden behind decorative UI
- approvals show exactly what will change before execution

This is not a mode switch. It is a multi-lane work dock.

## Right Status Panel

The right panel should answer: "What is this system connected to, what does it know, and what is it allowed to do right now?"

Sections:

- Connection Status
- Active Context
- Thread Status
- Memory Queue
- Calendar Snapshot
- Pending External Actions
- Permission Profile

Connection examples:

- Codex App Server
- Obsidian CLI
- Obsidian Vault
- Google Calendar
- Google Drive
- Gmail
- GitHub
- Local Files
- Local Model Router

Each connection should have:

- status
- last check time
- permission level
- failure message if disconnected

## Top Status Rail

Minimal top area:

- product identity: Eden Command
- current task title
- permission profile
- emergency pause / stop control

This is not a navigation bar.

## Interaction Model

Primary command input examples:

- "이번 주 일정과 개발 우선순위를 정리해줘."
- "이 아이디어가 실제로 말이 되는지 검증하고 실행계획으로 바꿔줘."
- "이 로컬 프로젝트에서 프론트 MVP를 만들어줘."
- "방금 논의한 내용을 Obsidian 후보 기억으로 저장해줘."
- "승인 대기 중인 작업을 보여줘."

Routing should happen internally:

- daily/schedule/memory questions route toward Eden
- coding/local-file/GitHub questions route toward Jarvis
- product planning that leads to implementation routes toward Hybrid

The routed target is not shown as a mode, actor label, or separate Pet appearance. It can be available in audit/debug views, but the normal user experience should rely on one Overlay Pet identity, work stream wording, context chips, and approval state.

## Approval UX

Every approval item must include:

- action title
- target app or file
- exact change summary
- risk level
- source context
- approve button
- reject button
- inspect details button

Approval examples:

- write candidate memory to Obsidian
- create calendar event
- send Gmail draft
- run shell command
- modify local file
- push Git branch

## Accessibility

Minimum requirements:

- keyboard navigable command input
- visible focus states
- 44px minimum interactive targets
- readable text at 16px base body
- no status conveyed by color alone
- reduced-motion support
- sufficient contrast in dark and light themes

## Responsive Behavior

Desktop first for MVP.

Required desktop layout:

- central Overlay Pet remains visible
- bottom dock remains usable
- right panel can collapse but must not disappear entirely

Mobile can be deferred, but the model should eventually become:

- Overlay Pet/status first
- command input second
- status panel as sheet
- logs and approvals as bottom sheet lanes

## Acceptance Criteria

- The user can interact without choosing a mode.
- The current activity is perceptible through the Overlay Pet without requiring visible Eden/Jarvis/Hybrid labels or separate Pet appearances.
- Work stream, execution log, and approval queue are visible or one click away.
- Right panel clearly shows connection and permission state.
- The Overlay Pet adds situational awareness rather than replacing functional UI.
- The design can support voice and motion input later without changing the architecture.
