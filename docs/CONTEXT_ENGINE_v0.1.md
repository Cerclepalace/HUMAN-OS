# HUMAN-OS — Context Engine v0.1

## Purpose

Construct a bounded, current representation of the human's operating state from events, memory, active session state and environmental signals.

The Context Engine does not create authority. It creates a controlled context package for downstream reasoning and attention decisions.

## Position

```text
EVENT BUS ─┐
MEMORY ────┼→ CONTEXT ENGINE → CONTEXT SNAPSHOT → REASONING / ATTENTION
SESSION ───┤
DEVICE ────┘
```

## Context layers

```text
L0 IDENTITY / SESSION
L1 CURRENT ENVIRONMENT
L2 ACTIVE TASK
L3 OPEN LOOPS
L4 ACTIVE GOALS / PROJECTS
L5 RECENT EVENTS
L6 RELEVANT MEMORY
L7 CONSTRAINTS / POLICIES
L8 UNCERTAINTY / CONFLICTS
L9 ATTENTION STATE
```

Higher layers must not silently override identity, policy or security state.

## Context snapshot

```text
context_id
session_id
created_at
expires_at
subject
active_goal_refs
active_project_refs
task_refs
open_loop_refs
relevant_memory_refs
environment_refs
constraint_refs
uncertainty_refs
attention_budget
provenance
classification
integrity_status
schema_version
```

Prefer references to sensitive underlying records instead of duplicating sensitive payloads.

## Construction pipeline

```text
INGEST EVENTS
   ↓
LOAD CURRENT STATE
   ↓
RETRIEVE RELEVANT MEMORY
   ↓
APPLY TEMPORAL FILTERS
   ↓
APPLY POLICY / PRIVACY FILTERS
   ↓
DETECT CONFLICTS / STALE STATE
   ↓
BUILD SNAPSHOT
   ↓
VALIDATE PROVENANCE + INTEGRITY
   ↓
PUBLISH CONTEXT UPDATED
```

## Lifecycle

```text
EMPTY
  ↓
BUILDING
  ↓
READY
  ├→ DEGRADED
  ├→ EXPIRED
  └→ INVALIDATED
```

`DEGRADED` means the system can operate with known missing context. Sensitive decisions must fail closed when required context is unavailable.

## Refresh triggers

Context SHOULD be rebuilt or incrementally updated after:

- session start;
- material new event;
- active task change;
- goal/project state change;
- relevant memory change;
- policy/security change;
- significant environment change;
- freshness expiry.

## Relevance

Relevance may use deterministic and model-assisted signals, but every selected item retains provenance and uncertainty state.

Suggested signals:

```text
TASK_MATCH
GOAL_MATCH
TEMPORAL_PROXIMITY
RECENCY
DEPENDENCY
ACTOR_RELATION
FRESHNESS
CLASSIFICATION
```

Relevance is not truth and must never erase uncertainty labels.

## Bounded context

The Context Engine MUST NOT expose unrestricted memory to a reasoning model by default.

```text
FULL DATA
   ↓ authorization + purpose + relevance
MINIMAL CONTEXT
   ↓
MODEL
```

This reduces privacy exposure, prompt-injection surface and accidental model dependence.

## Context poisoning resistance

External content can propose context but cannot directly mutate trusted state.

```text
EXTERNAL INPUT
 → RAW EVENT
 → EVALUATION
 → ACCEPTED STATE / QUARANTINE / REJECTION
```

## Context conflicts

The snapshot must preserve unresolved conflicts rather than collapse them into a single assertion.

```text
CONFLICT = TRUE
```

A reasoning component must be able to distinguish:

```text
KNOWN
INFERRED
HYPOTHESIZED
UNKNOWN
CONFLICTING
STALE
```

## Privacy

Context construction is purpose-bounded. Data not needed for the active purpose is excluded or represented by a protected reference.

## Failure semantics

If the context cannot be safely constructed:

- mark it `DEGRADED` or `INVALIDATED`;
- expose missing dependencies explicitly;
- prevent sensitive downstream execution where required context is absent;
- never fabricate missing context.

## Required invariants

1. Every context item has provenance.
2. Context is time-bounded.
3. Stale state is explicitly marked.
4. Conflicts remain visible.
5. Context is policy-filtered.
6. Sensitive data is minimized.
7. Missing information is never fabricated.
8. Model output cannot directly mutate trusted context.
9. Context snapshots are reconstructible from source state.
10. Sensitive execution fails closed when required context is unavailable.

## Acceptance gate

Fixtures must prove session reconstruction, relevance filtering, temporal expiry, conflict visibility, privacy minimization, degraded operation and provenance preservation.

Status: `SPECIFICATION / NOT YET IMPLEMENTED`.
