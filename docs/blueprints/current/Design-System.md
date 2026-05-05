# Eden Front Design System

Date: 2026-05-03
Status: Planning baseline

## Design Direction

Quiet operational intelligence.

The product should feel focused, controlled, and technically capable. It should not look like a SaaS marketing dashboard, a generic AI chat app, or a purely decorative sci-fi interface.

## Visual Principles

- One continuous command surface.
- No visible Eden/Jarvis mode tabs or center-panel actor labels.
- Information density is acceptable, but hierarchy must be clear.
- The orb is a state instrument, not a hero illustration.
- Logs and approvals must remain more legible than animation.
- Avoid card-inside-card layouts.
- Avoid one-note purple, blue-slate, beige, or orange/brown palettes.

## Color Tokens

Base:

- background: `#0B0D10`
- surface: `#11151A`
- surface-raised: `#171C22`
- border: `#28313A`
- text-primary: `#E7ECEF`
- text-secondary: `#9AA7B2`
- text-muted: `#66737F`

Accent:

- thinking: `#7DD3FC`
- verifying: `#A7F3D0`
- building: `#FDE68A`
- approval: `#FBBF24`
- blocked: `#F87171`
- idle: `#94A3B8`

Use accent colors sparingly for state and affordance. Do not flood the entire UI with one accent family.

## Typography

Recommended stack:

```css
font-family: Inter, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
```

Scale:

- body: 16px
- small: 13px
- micro/status: 12px
- panel title: 14px medium
- current task: 18px medium
- orb state label: 20px medium

Rules:

- letter spacing: 0
- no viewport-based font scaling
- avoid huge hero type inside operational panels
- preserve readable line length in logs and approvals

## Spacing

Base unit: 4px.

Recommended:

- xs: 4px
- sm: 8px
- md: 12px
- lg: 16px
- xl: 24px
- page gutter: 20px

## Radius

- small controls: 6px
- panels: 8px
- command dock: 10px only if visually justified
- orb: circular

Avoid heavily rounded pill-heavy UI unless the element is a natural chip/status token.

## Layout Tokens

Desktop:

- top rail height: 44px
- right panel width: 320px to 380px
- bottom dock height: 34vh to 42vh
- orb zone min height: remaining viewport

Command dock:

- input height: 48px to 64px
- stream/log lane minimum height: 160px
- approval lane should be visible when pending actions exist

## Components

Required MVP components:

- StatusOrb
- TopStatusRail
- CommandInput
- WorkStream
- ExecutionLog
- ApprovalQueue
- RightStatusPanel
- ConnectionStatusItem
- ContextSourceList
- MemoryCandidateItem
- PermissionBadge
- ThreadStatusItem
- StopControl

## Icons

Use lucide icons where available:

- Send
- Mic
- CircleStop
- Check
- X
- GitBranch
- Calendar
- Mail
- Folder
- Database
- Shield
- AlertTriangle
- Terminal
- Brain
- RefreshCw
- Eye

Use icon buttons for clear tool actions. Text buttons are acceptable for approval actions where ambiguity is dangerous.

## Motion

Motion should indicate state, not decorate the interface.

Durations:

- hover/focus: 120ms to 180ms
- panel transitions: 180ms to 240ms
- orb breathing: slow idle, faster during active work

Reduced motion:

- replace orb animation with a static luminous ring plus explicit state text
- keep all state labels visible

## Orb Routing Signatures

The orb expresses internal routing without text labels.

Thinking, memory, daily context:

- calmer breathing
- cyan/violet accent
- stable luminous shell
- slower ring grain

Development, files, GitHub, execution:

- rose/blue accent
- sharper rim
- clearer progress behavior

Hybrid planning-to-build work:

- magenta/electric transition
- stronger synthetic color handoff
- alternating calm and structured motion
- visible handoff pulse when moving from planning to execution

These signatures combine with six motion states. Route color expresses the work character; motion expresses current activity.

## Orb Motion States

The orb has six primary motion states:

- Idle
- Responding
- Thinking
- Working
- Approval
- Interrupted

This creates 18 core presets:

```txt
3 route color families x 6 motion states = 18 orb presets
```

The six motion states:

- Idle: slow breathing, low glow, stable organic motion.
- Responding: speech/text pulse through higher input/output volume.
- Thinking: slower scan-like organic flow.
- Working: stronger output volume and driven movement.
- Approval: slowed motion and suspended rim tension without a separate overlay.
- Interrupted: broken rhythm and visible flow break. This covers both error and blocked work at the orb level.

Each state should map to:

- orb treatment
- status label
- work stream event style
- optional right-panel highlight

The normal UI may still describe the exact cause as "error" or "blocked" in logs and panels. The orb should treat both as one interrupted motion family.

## Anti-Patterns To Avoid

- decorative dashboards that do not expose real state
- hidden approval queues
- logs that look like chat messages
- chat messages that pretend to be tool results
- mode tabs that force the user to classify their own intent
- visible center-panel labels that make the user think they chose the wrong actor
- storing raw personal memory in development project files
- excessive glow, blur, or particles that reduce readability
- animation that implies work is happening when the system is idle
