# Eden/Jarvis Cognitive Architecture v2

Date: 2026-05-05
Status: Full target architecture, not MVP scope

## 1. Target Definition

Eden/Jarvis is not a chatbot, not a single autonomous agent, and not only a front-end shell.

The target system is a personal cognitive operating layer:

- Eden: thinking, memory, daily context, decisions, schedules, communication context.
- Jarvis: development, local files, GitHub, Codex execution, validation, implementation.
- Hybrid: strategy-to-execution bridge where Eden frames and verifies while Jarvis implements.

The user should experience one continuous AI presence. Eden/Jarvis/Hybrid are internal routing states, not visible mode buttons.

## 2. Core Design Thesis

The upgraded Jarvis should combine five architectural ideas:

1. Skill-first agent architecture.
2. Dynamic working memory through a reservoir layer.
3. Predictive verification through prediction-error loops.
4. Obsidian ontology as durable long-term memory.
5. Front-end HCI as a live state instrument, not decorative UI.

Reference mapping:

| Reference | Architectural Translation |
| --- | --- |
| Reservoir Computing | Dynamic context reservoir / fading working memory |
| RNN, leaky integration, gated memory | Session memory and state decay |
| Predictive Coding | Prediction -> observation -> error -> verification -> update |
| Free Energy Principle | Balance accuracy, complexity, and uncertainty |
| Modular Architecture of Intelligence | Eden/Jarvis/Hybrid skill routing and task-belief switchboard |
| Thousand Brains / consensus voting | Multi-perspective review and red-team synthesis |
| Cognitive maps / hippocampus | Obsidian ontology and project/context graph |
| Memory consolidation / sharp-wave ripples | Promote only useful memories into canonical notes |
| Anthropic skills/agents guidance | Build skills and workflows first; use agent loops only where needed |
| AI agent safety cases | Approval gates, audit logs, secrets isolation, external-action policy |

## 3. Non-Negotiable Principles

- Codex App is the primary execution host, but it must not be treated as durable memory.
- Obsidian is long-term memory, but it must not become a raw transcript dump.
- Front-end state must be driven by real system events, not fake animations.
- Automation can be broad, but not boundaryless.
- External sends, money, credentials, deletion, publishing, and irreversible actions require policy gates.
- The system should challenge and verify the user's thinking without taking over the user's judgment.
- Claims must carry evidence status: observed, inferred, assumed, stale, or unverified.

## 4. System Layers

```txt
Human Input
  text / voice / motion / files / links
        |
Eden Front
  orb / command stream / execution log / approval dock / connection status
        |
Command Gateway
  event bus / thread registry / policy engine / tool router / audit log
        |
Cognitive Kernel
  intent encoder / reservoir / predictive loop / skill router / memory consolidator
        |
Execution Surfaces
  Codex App / Obsidian CLI / Calendar / Gmail / Drive / GitHub / browser / computer-use
        |
Memory + Audit
  Obsidian vault / events.jsonl / command traces / memory candidates / approvals
```

## 5. Runtime Actors

| Actor | Responsibility | Should Not Do |
| --- | --- | --- |
| Eden Front | Receive input, show state, expose approvals, show live traces | Contain the full reasoning engine |
| Command Gateway | Normalize commands, record events, route tools, apply permissions | Make unsourced strategic decisions |
| Cognitive Kernel | Maintain state, choose workflows/agents, verify claims, manage memory candidates | Directly bypass policy |
| Codex App | Deep reasoning, coding, local file work, validation, review | Be assumed callable from any front without a bridge |
| Obsidian CLI | Durable memory read/write/search | Store secrets or raw unreviewed everything |
| Connectors | Calendar/Gmail/Drive/GitHub actions | Execute irreversible actions without gates |

## 6. Critical Feasibility Boundary

The design is logically sound only if this boundary is respected:

```txt
Front cannot assume it can directly control an arbitrary open Codex App thread
unless a real Codex command bridge exists.
```

Therefore the architecture needs a `Command Gateway`.

Possible gateway modes:

- Local file/event bridge as the baseline adapter.
- Native Codex bridge if the app exposes stable thread control.
- Plugin/connector route when a supported Codex plugin can perform the action.
- API/local model fallback only when the user explicitly accepts cost or local capability limits.

If this boundary is ignored, the system becomes a mock UI that looks powerful but cannot reliably act.

### CommandGatewayPort

The front must depend only on a port contract, not on a specific Codex control mechanism.

```ts
type CommandGatewayPort = {
  submitCommand(input: CommandInput): Promise<CommandReceipt>;
  getCommandStatus(commandId: string): Promise<CommandStatus>;
  listEvents(query: EventQuery): Promise<EdenEvent[]>;
  requestApproval(request: ApprovalRequest): Promise<ApprovalReceipt>;
  resolveApproval(approvalId: string, decision: ApprovalDecision): Promise<void>;
  cancelCommand(commandId: string, reason: string): Promise<void>;
};

type CommandInput = {
  idempotencyKey: string;
  sessionId: string;
  actorHint?: "eden" | "jarvis" | "hybrid";
  intentHint?: string;
  text: string;
  attachments: string[];
  requestedScope: ExecutionScope;
  userPresence: "active" | "away" | "scheduled";
};

type CommandReceipt = {
  commandId: string;
  accepted: boolean;
  status: "queued" | "blocked" | "requires-approval";
  reason?: string;
};

type CommandStatus = {
  commandId: string;
  status: "queued" | "running" | "waiting-approval" | "succeeded" | "failed" | "cancelled" | "blocked";
  activeActor?: "eden" | "jarvis" | "hybrid" | "system";
  progressSummary: string;
  latestEventId?: string;
  pendingApprovalIds: string[];
};

type EventQuery = {
  sessionId?: string;
  commandId?: string;
  correlationId?: string;
  afterSequence?: number;
  limit: number;
};

type ApprovalRequest = {
  commandId: string;
  action: ActionDescriptor;
  previewRef?: string;
  reason: string;
};

type ApprovalReceipt = {
  approvalId: string;
  status: "pending" | "approved" | "rejected" | "expired";
};

type ApprovalDecision = {
  decision: "approve" | "reject";
  decidedAt: string;
  note?: string;
};

type ActionDescriptor = {
  actionType: string;
  destination: "local" | "obsidian" | "calendar" | "gmail" | "drive" | "github" | "web" | "public";
  reversible: boolean;
  sensitivity: "public" | "personal" | "private" | "secret";
  scope: ExecutionScope;
};
```

Baseline adapter:

```txt
front writes:
  eden-ops/inbox/commands/{commandId}.json

gateway appends:
  eden-ops/audit/events.jsonl
  eden-ops/audit/tool-calls.jsonl
  eden-ops/audit/approvals.jsonl

codex thread or local worker reads:
  eden-ops/inbox/commands/*.json

worker writes:
  eden-ops/outbox/results/{commandId}.json
  eden-ops/runtime/state/{sessionId}.json
```

Adapter rule:

- `file-event` is the compatibility baseline.
- `native-codex`, `plugin`, `connector`, `api`, and `local-model` are replaceable adapters behind the same port.
- The front never imports adapter-specific APIs.
- Every adapter must emit the same event schema.

## 7. Canonical Data Contracts

### EdenEvent

Every meaningful input, tool call, memory write, error, approval, and result becomes an event.

```ts
type EdenEvent = {
  id: string;
  schemaVersion: 1;
  createdAt: string;
  recordedAt: string;
  sequence: number;
  correlationId: string;
  sessionId: string;
  commandId?: string;
  parentEventId?: string;
  idempotencyKey?: string;
  status: "pending" | "running" | "succeeded" | "failed" | "cancelled" | "blocked";
  source: "user" | "front" | "codex" | "obsidian" | "calendar" | "gmail" | "drive" | "github" | "system";
  type:
    | "user.input"
    | "intent.detected"
    | "tool.started"
    | "tool.finished"
    | "claim.made"
    | "claim.verified"
    | "memory.candidate"
    | "memory.promoted"
    | "approval.requested"
    | "approval.resolved"
    | "error.raised"
    | "state.changed";
  actor: "eden" | "jarvis" | "hybrid" | "system";
  actorInstance?: string;
  trust: "user" | "local" | "connector" | "external" | "untrusted";
  sensitivity: "public" | "personal" | "private" | "secret";
  scope: ExecutionScope;
  summary: string;
  payloadRef?: string;
  relatedIds: string[];
  hash: string;
};

type ExecutionScope = {
  workspaceId?: string;
  workspacePath?: string;
  vaultId?: string;
  vaultPath?: string;
  threadId?: string;
  connectorIds: string[];
};
```

Event log invariants:

- Append-only by default.
- No event is deleted during normal operation.
- Corrections are represented as new events.
- `sequence` is monotonically increasing per event log.
- `idempotencyKey` prevents duplicate execution of the same command.
- `correlationId` groups all events caused by one user-level request.
- `hash` is calculated from the canonical JSON payload excluding `hash`.
- Replaying events from sequence 1 should reconstruct reservoir state, command status, and approval status.

### SkillDefinition

Skills are the operating units. Agents are only used when a skill needs open-ended tool iteration.

```ts
type SkillDefinition = {
  id: string;
  domain: "memory" | "calendar" | "email" | "development" | "research" | "review" | "front" | "system";
  capabilities: string[];
  inputs: string[];
  outputs: string[];
  allowedTools: string[];
  permissionLevel: "read" | "local-write" | "external-draft" | "external-send" | "destructive";
  evidenceRequired: "none" | "source" | "tool-result" | "test" | "human-approval";
  failureModes: string[];
};
```

### Claim

All non-trivial answers should be internally represented as claims.

```ts
type Claim = {
  id: string;
  text: string;
  status: "observed" | "inferred" | "assumed" | "unverified" | "stale" | "refuted";
  evidenceIds: string[];
  confidence: number;
  predictionError?: number;
  nextVerification?: string;
};
```

### MemoryCandidate

```ts
type MemoryCandidate = {
  id: string;
  kind: "preference" | "decision" | "project" | "constraint" | "fact" | "pattern" | "open-loop" | "artifact";
  status: "raw" | "candidate" | "canonical" | "deprecated" | "rejected";
  content: string;
  sourceIds: string[];
  confidence: number;
  sensitivity: "public" | "personal" | "private" | "secret";
  reviewAfter?: string;
  relations: Array<{ type: string; target: string }>;
};
```

## 8. Intent And Routing Logic

Intent classes:

- `think`: strategy, judgment, red-team, decisions.
- `remember`: store or update durable context.
- `retrieve`: search memory, files, calendar, email, Drive.
- `develop`: code, test, review, local repo work.
- `schedule`: calendar and time planning.
- `communicate`: Gmail drafts, follow-ups, message context.
- `operate`: browser/computer-use/local app actions.
- `research`: web/doc/source validation.
- `review`: independent critique, correctness, risk.
- `automate`: recurring or delayed actions.

Routing rule:

```txt
If the task is repetitive and deterministic -> workflow.
If the task is open-ended and tool feedback changes the next step -> agent loop.
If the task is high-risk -> workflow + explicit gate, even if an agent helps.
```

Actor selection:

```txt
Eden:
  think, remember, retrieve, schedule, communicate, research, personal context

Jarvis:
  develop, review code, local files, GitHub, tests, browser QA

Hybrid:
  product planning -> implementation
  personal decision -> concrete system change
  research finding -> Obsidian memory + code/front update
```

## 9. Reservoir Layer

The reservoir is not long-term memory. It is dynamic working state.

It holds fading activations such as:

```ts
type ReservoirState = {
  routeEden: number;
  routeJarvis: number;
  routeHybrid: number;
  arousal: number;
  focus: number;
  load: number;
  confidence: number;
  urgency: number;
  voiceEnergy: number;
  toolActivity: number;
  memoryActivity: number;
  predictionError: number;
  userDecisionPressure: number;
  errorPressure: number;
};
```

Update rule:

```txt
state[k] = state[k] * decay(dt, tau[k]) + weighted_event_contribution[k]
```

Reducer contract:

```ts
type ReservoirReducerInput = {
  previous: ReservoirState;
  event: EdenEvent;
  elapsedSeconds: number;
};

type ReservoirReducerOutput = {
  next: ReservoirState;
  contributions: Partial<Record<keyof ReservoirState, number>>;
  decayApplied: Partial<Record<keyof ReservoirState, number>>;
};
```

Default decay constants:

| Signal | Tau | Meaning |
| --- | --- | --- |
| `routeEden` | 600s | planning/daily context should fade slowly |
| `routeJarvis` | 600s | development context should persist across command bursts |
| `routeHybrid` | 480s | cross-domain work stays active but decays |
| `arousal` | 180s | overall energy fades within minutes |
| `focus` | 300s | concentration persists across related turns |
| `load` | 240s | workload fades after tools finish |
| `confidence` | 420s | confidence changes slowly |
| `urgency` | 180s | pending decisions stay visible but decay |
| `voiceEnergy` | 20s | speech/text rhythm is short-lived |
| `toolActivity` | 90s | tool execution should fade quickly after completion |
| `memoryActivity` | 180s | memory retrieval/write remains visible briefly |
| `predictionError` | 300s | unresolved mismatch should persist |
| `userDecisionPressure` | 900s | user decisions should not vanish too quickly |
| `errorPressure` | 360s | errors remain salient until resolved |

Event contribution matrix:

| Event Type | Main Contributions |
| --- | --- |
| `user.input` | `arousal +0.12`, `focus +0.08`; route depends on intent hint |
| `intent.detected: think` | `routeEden +0.35`, `focus +0.12` |
| `intent.detected: develop` | `routeJarvis +0.35`, `toolActivity +0.08` |
| `intent.detected: hybrid` | `routeHybrid +0.35`, `load +0.12` |
| `tool.started` | `toolActivity +0.35`, `load +0.18`, `arousal +0.12` |
| `tool.finished:succeeded` | `toolActivity -0.18`, `confidence +0.12`, `load -0.08` |
| `tool.finished:failed` | `errorPressure +0.35`, `predictionError +0.22`, `confidence -0.18` |
| `claim.made:unverified` | `predictionError +0.1`, `confidence -0.08` |
| `claim.verified` | `confidence +0.18`, `predictionError -0.2` |
| `memory.candidate` | `memoryActivity +0.24`, `routeEden +0.08` |
| `memory.promoted` | `memoryActivity +0.12`, `confidence +0.1` |
| `approval.requested` | `urgency +0.32`, `userDecisionPressure +0.45`, `toolActivity -0.1` |
| `approval.resolved` | `urgency -0.28`, `userDecisionPressure -0.38`, `confidence +0.06` |
| `error.raised` | `errorPressure +0.42`, `predictionError +0.28`, `confidence -0.22` |
| `state.changed` | no direct contribution unless generated from another event |

Normalization:

- Clamp every signal to `[0, 1]`.
- Route signals are normalized so the strongest route can dominate without zeroing the others.
- Negative contributions are allowed but cannot push below 0.
- `confidence` starts at `0.6`, not `0`, because neutral confidence is not failure.
- `predictionError` and `errorPressure` must decay only after success, resolution, or time.

Replay test:

```txt
Given the same ordered EdenEvent log:
  reservoir(events[1..n]) must produce the same ReservoirState every time.

Given a duplicated command with the same idempotencyKey:
  the reducer must ignore duplicate execution contributions.

Given a failed tool followed by a successful retry:
  errorPressure and predictionError must decrease but not instantly reset to zero.
```

Use:

- Keeps recent context alive without saving everything.
- Lets the orb react to actual state.
- Helps the router know whether the user is in planning, debugging, decision, or execution flow.
- Prevents every turn from being treated as an isolated prompt.

## 10. Predictive Verification Loop

This is the main anti-hallucination and thinking-support loop.

```txt
1. Build current model:
   What does Eden/Jarvis believe about the user, project, tools, constraints, and goal?

2. Predict:
   What should be true if the planned answer/action is correct?

3. Observe:
   Read files, run tests, search sources, inspect calendar, query Obsidian, or ask user.

4. Compare:
   Calculate prediction error.

5. Act:
   Low error -> proceed.
   Medium error -> qualify answer and add verification.
   High error -> stop, red-team, ask, or run a tool.

6. Consolidate:
   Store corrected conclusions as memory candidates only when durable.
```

Example:

```txt
Claim: "This library can support the orb."
Prediction: It installs, builds, renders, and fits the lookdev direction.
Observation: npm/build/browser QA/reference comparison.
Error: build failure, visual mismatch, performance issue, or API mismatch.
Action: reject, adapt, or document residual risk.
```

## 11. Memory Architecture

Memory has three levels:

| Level | Store | Role |
| --- | --- | --- |
| Working | Reservoir state / event cache | Recent context and state |
| Episodic | Command traces / daily logs | What happened, when, why |
| Semantic | Obsidian ontology | Reviewed durable knowledge |

Obsidian promotion rule:

```txt
Raw event -> memory candidate -> reviewed canonical memory
```

Promote when:

- The user explicitly states a preference or constraint.
- A decision is made.
- A project state changes.
- A repeated pattern becomes useful.
- A verified source matters later.
- A failure reveals a durable rule.

Do not promote:

- transient emotion
- raw tool spam
- unverified web/email claims
- secrets
- one-off implementation noise

## 12. Obsidian Ontology

Core entity types:

```txt
Person, Project, Area, Goal, Interest, Skill, Tool, Decision, Preference,
Constraint, Task, OpenLoop, Source, Artifact, Event, Experiment, Outcome, Session
```

Core relations:

```txt
belongs_to, supports, conflicts_with, depends_on, blocked_by, created_from,
validated_by, invalidated_by, supersedes, related_to, decided_in, used_for
```

The ontology is not for academic neatness. It exists so Jarvis can answer:

- What matters to the user?
- What is currently active?
- What has already been decided?
- What conflicts with this new request?
- Which tool or project is relevant?
- What should be remembered versus ignored?

## 13. Tool Router

Tool routing should be explicit and policy-aware.

```txt
Obsidian:
  prefer CLI for stable local memory operations
  use MCP only when stable and useful

Calendar:
  connector for read/summarize
  approval for create/update/cancel

Gmail:
  read/summarize with sensitivity marking
  draft without approval when allowed
  send only after approval

GitHub:
  connector/gh for issues, PRs, CI
  push/PR only after scoped confirmation

Local files:
  allowed inside approved workspace
  destructive commands require approval

Browser/computer-use:
  use when no structured API exists
  treat results as observed but fragile
```

## 14. Autonomy And Permission Levels

Permission is not a single level. It is calculated from:

```txt
permission = f(actionType, scope, sensitivity, reversibility, destination, userPresence)
```

Base levels:

| Level | Meaning | Examples | Default |
| --- | --- | --- | --- |
| L0 | Read-only | summarize notes, inspect schedule, search files | unattended in trusted scopes |
| L1 | Local candidate write | create memory candidate, write draft note, append audit event | unattended in trusted scopes |
| L2a | Reversible local workspace action | run tests, format, create local docs, edit approved worktree | unattended only in approved workspace |
| L2b | Risky local workspace action | broad code edits, dependency changes, file moves | preview or explicit task approval |
| L3 | External draft | Gmail draft, calendar proposal, PR description | preview required |
| L4 | External commit/send/change | send email, update calendar, push branch | approval required |
| L5 | Sensitive/destructive | payments, secrets, deletion, public posting | explicit case-by-case approval or forbidden |

Recommended default:

- L0-L1 can be unattended if the source scope is trusted and no secret data is exposed.
- L2a can be unattended only inside approved workspaces, worktrees, or generated doc areas.
- L2b requires either task-level approval or a narrow allowlist.
- L3 requires a preview artifact before execution.
- L4 requires approval.
- L5 requires explicit case-by-case confirmation or remains forbidden.

This is the safe version of "automatic execution without asking every time."

### PermissionPolicy Matrix

| Action | Scope | Sensitivity | Reversible | Default Decision |
| --- | --- | --- | --- | --- |
| read file | approved workspace | public/personal | yes | allow |
| search Obsidian | approved vault areas | public/personal/private | yes | allow, log query summary |
| create memory candidate | approved vault inbox | public/personal/private | yes | allow |
| promote canonical memory | Obsidian canonical | any | partly | approval required |
| run tests/build | approved workspace | public/personal | yes | allow |
| edit generated docs | approved workspace | public/personal | yes | allow |
| edit source code | approved workspace | public/personal | usually | allow only under active user task |
| install dependencies | approved workspace | public/personal | partly | preview or approval |
| delete/move files | any | any | sometimes no | approval required |
| create Gmail draft | Gmail | private | yes | preview required |
| send Gmail | Gmail | private | no | approval required |
| calendar read | Calendar | private | yes | allow summary |
| calendar create/update/cancel | Calendar | private | partly | approval required |
| GitHub push/PR | GitHub | public/private repo | partly | approval required unless user requested publish |
| public post/publish | external public | any | no | approval required |
| secret access/export | any | secret | no | forbidden unless explicitly scoped |

Policy evaluation contract:

```ts
type PermissionDecision = {
  decision: "allow" | "preview" | "approval-required" | "deny";
  level: "L0" | "L1" | "L2a" | "L2b" | "L3" | "L4" | "L5";
  reasons: string[];
  requiredApprover?: "user";
  expiresAt?: string;
  auditEventId: string;
};
```

No adapter may execute an action until the policy engine has emitted a decision.

Policy input:

```ts
type PermissionPolicyInput = {
  action: ActionDescriptor;
  actor: "eden" | "jarvis" | "hybrid" | "system";
  userPresence: "active" | "away" | "scheduled";
  taskApproved: boolean;
  allowlistHit: boolean;
};
```

## 15. Front-End HCI Logic

The front should show one AI presence:

- center: orb as state instrument
- bottom: conversation / work stream / execution log / approval queue
- right: connections / memory context / active tools / current risk
- no hard Eden/Jarvis mode switch

Orb state should be driven by `ReservoirState` and `OrbSignal`:

```txt
routeEden/routeJarvis/routeHybrid -> color family
activity -> motion family
predictionError -> rim instability
toolActivity -> cilia/external field
memoryActivity -> internal lattice density
voiceEnergy -> speech/text pulse
urgency -> tension/brightness
confidence -> stability/smoothness
```

The orb should not expose private internal state as text. It should make the system feel alive and legible.

## 16. Skill-First Implementation Logic

Build skills as stable procedural modules:

```txt
memory.search
memory.propose
memory.consolidate
calendar.brief
calendar.propose_change
gmail.summarize
gmail.draft
github.triage
dev.implement
dev.review
research.verify
thinking.redteam
front.emit_state
```

Then compose them through workflows:

```txt
Weekly planning:
  calendar.brief -> memory.search -> open-loops -> plan -> approvals

Development request:
  intent -> repo inspect -> plan -> implement -> test -> review -> memory candidate

Thinking request:
  context retrieve -> assumptions -> lenses -> evidence check -> decision options

Research request:
  source search -> primary verification -> claims -> Obsidian source note
```

Use agent loops only when the next step cannot be known upfront.

## 17. Codex Thread Architecture

Thread registry:

```yaml
threads:
  eden-command:
    actor: eden
    scope: personal-context
    permissions: [read_memory, propose_memory, read_calendar, draft_external]
  jarvis-dev:
    actor: jarvis
    scope: development
    permissions: [read_workspace, edit_workspace, run_tests, inspect_git]
  hybrid:
    actor: hybrid
    scope: planning-to-implementation
    permissions: [handoff, review, summarize, propose_actions]
```

Handoff contract:

```txt
Eden -> Jarvis:
  goal, constraints, relevant memory summary, acceptance criteria, forbidden data

Jarvis -> Eden:
  changed files, validation, risks, decisions needed, memory candidates
```

This prevents personal memory from leaking into development repos.

### HandoffEnvelope

The handoff must be a sanitized envelope, not a raw memory dump.

```ts
type HandoffEnvelope = {
  id: string;
  schemaVersion: 1;
  createdAt: string;
  fromActor: "eden" | "jarvis" | "hybrid";
  toActor: "eden" | "jarvis" | "hybrid";
  commandId: string;
  purpose: "development" | "review" | "planning" | "memory-update" | "research";
  allowedEntityTypes: Array<
    "Project" | "Decision" | "Constraint" | "Preference" | "Tool" | "Task" | "Artifact" | "Source" | "Outcome"
  >;
  forbiddenEntityTypes: Array<"Person" | "PrivateEvent" | "Credential" | "RawEmail" | "RawCalendar" | "Secret">;
  maxSensitivity: "public" | "personal" | "private";
  redactionPolicy: "summary-only" | "entity-only" | "source-linked-summary";
  sourceTrace: Array<{ sourceId: string; sourceType: string; sensitivity: string; includedAs: "summary" | "link" }>;
  payload: {
    goal: string;
    constraints: string[];
    relevantMemorySummary: string[];
    acceptanceCriteria: string[];
    forbiddenData: string[];
    openQuestions: string[];
  };
  sanitizerReport: {
    removedFields: string[];
    downgradedItems: string[];
    blockedItems: string[];
  };
};
```

Sanitizer rules:

- Never include raw Gmail, raw calendar, credentials, secrets, or full personal transcripts.
- Include only summary-level memory unless raw source is explicitly needed and approved.
- Prefer project/decision/constraint/preference/tool/task entities for development handoffs.
- Strip names, contact details, private event details, and unrelated personal context by default.
- If a source is private but relevant, include the conclusion and source trace, not the raw content.
- Handoff files must live outside development repos unless intentionally copied as sanitized project artifacts.

## 18. Expected Effects

If implemented correctly, the upgraded Jarvis should produce:

- Better continuity: recent work and long-term context both matter.
- Less hallucination: answers are checked against prediction/error/evidence.
- Safer automation: actions are categorized and audited.
- Better thinking support: Eden challenges and verifies rather than just rephrasing.
- Better development flow: Jarvis can implement, test, review, and report with context.
- Cleaner Obsidian: only durable knowledge becomes canonical memory.
- More natural HCI: the orb and stream reflect real activity instead of fake status.
- Lower cognitive overhead: the user sees what is happening, what is pending, and what needs judgment.

## 19. Logical And Code Feasibility Review

### Sound Parts

- Event log + reservoir + Obsidian ontology is implementable with normal local files and TypeScript/Python scripts.
- Skill registry and workflow router are implementable without a heavy agent framework.
- Predictive verification is implementable as a claim/evidence discipline even before any machine learning.
- Orb signal mapping already aligns with the existing frontend architecture.
- Obsidian CLI is a reasonable stable memory path if MCP is unreliable.

### Fragile Assumptions

- Direct front-to-Codex thread control may not be available as a stable public interface.
- "No approval for everything" is not safe for external actions.
- Voice/motion input adds UX value but should not be the control-plane foundation.
- A full ontology can become too complex unless memory promotion is strict.
- Browser/computer-use actions are useful but less reliable than structured tools.

### Required Mitigations

- Build `CommandGatewayPort` with the file-event adapter as baseline so the front does not depend on one Codex control mechanism.
- Keep all actions auditable through `events.jsonl`, `tool-calls.jsonl`, and `approvals.jsonl`.
- Require a `PermissionDecision` before any adapter executes an action.
- Run every Eden/Jarvis handoff through `HandoffEnvelope` sanitization.
- Make reservoir state replayable from `EdenEvent` logs.
- Use source trust labels for Gmail, web, Drive, and external content.
- Keep personal memory out of development harnesses except through sanitized handoffs.
- Treat every durable memory write as candidate first unless explicitly reviewed.

## 20. Dependency Order For Real Implementation

This is not an MVP split. It is the dependency order that keeps the full architecture coherent.

1. Define contracts: `CommandGatewayPort`, `EdenEvent`, `ExecutionScope`, `ActionDescriptor`, `PermissionDecision`, `SkillDefinition`, `Claim`, `MemoryCandidate`, `ReservoirState`, `HandoffEnvelope`.
2. Build event bus and audit store.
3. Build file-event Command Gateway baseline adapter.
4. Build permission policy engine.
5. Build reservoir reducer and replay tests.
6. Build front state adapter: event stream -> reservoir -> orb/workstream/status.
7. Build skill registry and tool router.
8. Build Obsidian CLI memory search/propose/consolidate.
9. Build predictive loop over claims and evidence.
10. Build Codex thread registry and sanitized handoff files.
11. Connect development workflow through Jarvis thread.
12. Connect Calendar/Gmail/Drive/GitHub skills with permission gates.
13. Add voice/motion as input encoders, not as core logic.
14. Add scheduled consolidation and periodic review.
15. Add stronger agent loops only where workflows are insufficient.

## 21. Final Architecture Summary

```txt
Jarvis v2 =
  Skill-first personal operating layer
  + Codex execution host
  + Obsidian ontology memory
  + Reservoir working state
  + Predictive verification loop
  + Policy-aware tool router
  + Auditable action queue
  + Orb-based HCI state surface
```

The system is coherent if it is treated as an operating architecture.

It becomes incoherent if it is treated as:

- one giant autonomous agent
- a pretty front-end over mock state
- raw transcript memory
- approval-free external automation
- direct Codex control without a real bridge

## 22. Sources And References

- Artem Kirsanov, Reservoir Computing: https://www.youtube.com/watch?v=cDxtFtoQVNc
- Artem Kirsanov, RNN memory: https://www.youtube.com/watch?v=PAoe7mmmvp0
- Artem Kirsanov, Predictive Coding: https://www.youtube.com/watch?v=l-OLgbdZ3kk
- Artem Kirsanov, Modular Architecture: https://www.youtube.com/watch?v=-_OgW6KSGE4
- Artem Kirsanov, Thousand Brains: https://www.youtube.com/watch?v=Dykkubb-Qus
- Artem Kirsanov, Cognitive Maps: https://www.youtube.com/watch?v=9qOaII_PzGY
- Artem Kirsanov, Artificial Hippocampus: https://www.youtube.com/watch?v=cufOEzoVMVA
- Artem Kirsanov, Memory Selection: https://www.youtube.com/watch?v=ceFFEmkxTLg
- Anthropic, Building Effective Agents: https://www.anthropic.com/engineering/building-effective-agents
- Anthropic, Skills over agents talk: https://www.youtube.com/watch?v=CEvIs9y1uog
- TED, OpenClaw: https://www.youtube.com/watch?v=7rzYDM6vMtI
- TED, AI and critical thinking: https://www.youtube.com/watch?v=3lPnN8omdPA
