# Eden Front UI Review

Date: 2026-05-03
Status: Orb-only implementation review

## Reviewed Direction

The current direction is:

- one front, no visible mode switching
- central status orb
- bottom conversation/work stream/execution log/approval area
- right connection/status/context panel
- Codex App as the primary execution host
- Obsidian as durable long-term memory
- local bridge and Eden Ops Harness as the control layer

## Verdict

This direction is stronger than the earlier visible Eden/Jarvis mode-switch concept.

Reason:

- the user should not need to classify intent before speaking
- the system can still route internally
- the UI can feel like one coherent assistant
- status visibility can replace manual mode selection
- later voice and motion input become easier because there is one command surface

## Current Orb Decision

The orb-only phase now uses a locally owned `ReferenceSphereOrb` shader as the base primitive.

Reason:

- the latest reference is a black-core particle-lattice sphere, not a Siri/blob orb
- direct local ownership gives better control over rim, lattice, diagonal wave, and corona
- the shader can still expose state and synthetic audio concepts for future voice/text input
- Eden/Jarvis route colors and motion tuning stay inside our own code

Implementation boundary:

- keep only the central orb and 18 comparison buttons for this phase
- do not reintroduce panels, logs, approval overlays, or mode switching yet
- use motion and color changes for approval/interrupted states instead of overlays

## What Changed

Previous concept:

- Eden mode
- Jarvis mode
- Hybrid mode
- user-visible switching

Current concept:

- one command surface
- internal routing expressed through orb animation, color, ring density, activity layer, and rim behavior
- state shown through orb behavior, work stream, top rail, and status panel
- work split is still enforced behind the scenes

## Critical Requirements Before Code

1. The orb must not become decorative-only.
2. Approval queue must be visible whenever actions are pending.
3. Right panel must show connection and permission state.
4. The system must distinguish chat, work stream, execution log, and approvals.
5. Internal Eden/Jarvis/Hybrid routing must be reflected through the orb and audit metadata, not exposed as mode tabs or center-panel actor labels.
6. The front project must stay separate from the installed development harness.

## UX Risks

| Risk | Severity | Mitigation |
| --- | --- | --- |
| Orb consumes attention without improving control | High | Map animation/color to real state and keep work stream/approval text explicit. |
| Logs become noisy and unreadable | Medium | Collapse verbose logs; keep work stream human-readable. |
| No visible actor label causes ambiguity | Medium | Use consistent orb signatures, context chips, and clear task/action wording. |
| Approval queue gets buried | High | Pin pending approvals in bottom dock and right panel. |
| Voice/motion added too early | Medium | First prove text command and state loop. |
| Local bridge becomes unsafe | High | Use permissions, allowlist, audit, and no public exposure. |

## Implementation Recommendation

Start with a mocked UI.

MVP data can be fake but should model real future objects:

- currentState
- inferredActor
- activeTask
- contextSources
- connections
- threadRegistry
- workStreamEvents
- executionLogEvents
- pendingApprovals
- memoryCandidates

The first code milestone should not connect Gmail, Calendar, Obsidian, or Codex yet. It should prove that the command surface can express the real operating model.

## Acceptance Review Checklist

- The first screen shows what the system is doing.
- The current orb lab keeps exactly 18 comparison presets.
- The WebGL canvas renders nonblank.
- The old custom ring/sphere/torus/blob implementations are removed.
- Route color changes are visible across the three families.
- Responding has a stronger synthetic speech modulation path.
- The design supports later voice/motion input by replacing synthetic audio with real input/output volume.
