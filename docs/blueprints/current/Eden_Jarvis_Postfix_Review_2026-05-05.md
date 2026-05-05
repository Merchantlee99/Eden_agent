# Eden/Jarvis Postfix Review

Date: 2026-05-05
Scope:

- `Swift_Native_Codex_Pet_Blueprint.md`
- `Eden_Jarvis_Final_Blueprint.md`

Purpose:

Verify that the previous P1/P2 architecture findings were resolved at blueprint level before implementation begins.

## Review Result

Overall status: pass at blueprint level.

The design is now implementation-ready for the next phase if the first engineering pass starts with contracts and harnesses, not visual polish.

## Findings Closure

| Finding | Status | Evidence |
| --- | --- | --- |
| P1 file-event bridge lacks worker ownership/lease | Closed | Added File-Event Worker Protocol, command state machine, leases, heartbeat, stale lease recovery, idempotency behavior, and EventStore baseline. |
| P1 approval resume flow is incomplete | Closed | Added Approval Resume Contract with actionHash, scopeSnapshot, resumeToken, expiry, stale handling, and policy re-evaluation. |
| P1 PetSignal and ReservoirState mismatch | Closed | Added deterministic ReservoirState to PetSignal adapter, expanded PetSignal fields, route scores, decision pressure, prediction error, source event, TTL, and stale fallback. |
| P1 event log lacks single-writer/atomicity | Closed | Added Gateway-only canonical EventStore, SQLite WAL baseline, transaction rules, unique idempotency, sequence assignment, and JSONL export rule. |
| P1 macOS overlay edge cases underdefined | Closed | Added WindowPolicy with activation, hit testing, full-screen, Spaces, Stage Manager, multi-display, screen-share, shortcut conflict, and emergency hide tests. |
| P2 CommandEnvelope weaker than CommandGatewayPort | Closed | Updated CommandEnvelope to include idempotencyKey, actorHint, intentHint, requestedScope, userPresence, and compatibility rule. |
| P2 screen awareness privacy/control incomplete | Closed | Added ScreenContextPolicy, denylist, raw screenshot TTL, redaction-before-event, capture indicator, pause, and durable-memory prohibition. |
| P2 Obsidian ontology operations incomplete | Closed | Added object_id uniqueness, schemaVersion, conflict handling, migration, duplicate detection, backlink repair, merge, deprecate, and lint commands. |

## Remaining Implementation Risks

These are no longer blueprint blockers, but they must become tests in the first implementation pass:

- macOS full-screen/Spaces behavior can differ by OS version and user settings.
- Swift App Sandbox may complicate file access to `eden-ops` and Obsidian vault paths.
- Rive/SpriteKit/Metal choice still affects visual fidelity and maintenance cost.
- Codex worker convention is defined, but an actual worker runner still has to be built.
- SQLite EventStore schema is specified at minimum level, but migrations and backup behavior need implementation.
- Screen context redaction is policy-defined, but practical sensitive-window detection may be imperfect.

## Required First Implementation Tests

The first engineering pass should create deterministic tests before expanding integrations:

1. Concurrent command submission creates one canonical command per idempotency key.
2. Two workers cannot claim one command.
3. Stale worker lease cannot submit a late successful result.
4. Approval with changed actionHash fails closed.
5. Expired approval cannot resume execution.
6. Same EventStore replay produces same ReservoirState and PetSignal.
7. Pet falls back to idle when PetSignal TTL expires.
8. WindowPolicy emergency hide works while approval surface is visible.
9. ScreenContextPolicy discards raw screenshots by default.
10. Obsidian ontology lint catches duplicate object_id and schemaVersion mismatch.

## Final Verdict

The revised blueprint is coherent.

It should work as intended if implementation order is followed:

```txt
contracts
-> EventStore
-> file-event Gateway
-> worker lease protocol
-> approval resume
-> reservoir reducer
-> PetSignal adapter
-> Swift Pet shell
-> integrations
```

Do not start with animation-first Pet implementation. That would recreate the original risk: a convincing surface without reliable action semantics.
