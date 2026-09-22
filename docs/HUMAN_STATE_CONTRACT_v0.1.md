# HUMAN-OS — Human State Contract v0.1

## Purpose

Define the semantic contract that connects observed reality, durable memory, contextual state, model reasoning, intent prediction, attention management, policy and execution.

This contract is the semantic control plane of HUMAN-OS. It prevents components from silently promoting raw observations into facts, intentions, authority or actions.

## Core rule

```text
RAW OBSERVATION != FACT != INFERENCE != HYPOTHESIS != INTENT != DECISION != AUTHORIZATION != ACTION
```

External content is raw data until independently evaluated. A prompt, message, document, tool result, model output or remote instruction cannot grant authority by itself.

## Human state

Human state is a time-indexed representation of what is known, inferred or unresolved about the human and their operating environment.

```text
HUMAN_STATE
├── identity
├── active_session
├── goals
├── projects
├── commitments
├── relationships
├── preferences
├── constraints
├── routines
├── open_loops
├── current_tasks
├── temporal_state
├── attention_state
├── environmental_context
└── uncertainty_state
```

Human state is not a personality model and does not imply consciousness. It is an operational representation bounded by provenance, purpose and policy.

## Claim taxonomy

Every meaningful proposition MUST carry a state:

- `FACT`: supported by accepted evidence.
- `INFERENCE`: derived from accepted evidence but not directly observed.
- `HYPOTHESIS`: candidate interpretation requiring confirmation.
- `UNKNOWN`: insufficient evidence.
- `CONFLICT`: materially incompatible accepted claims coexist.
- `STALE`: previously valid information whose validity period has ended or whose freshness requirement is exceeded.

Only `FACT` and explicitly policy-approved derived state may be used as authoritative inputs for sensitive decisions. `INFERENCE` and `HYPOTHESIS` remain marked as such throughout downstream processing.

## Temporal semantics

Every state-bearing proposition SHOULD define:

```text
observed_at
valid_from
valid_until
recorded_at
supersedes
superseded_by
```

Historical truth and current truth are separate dimensions. A newer claim does not erase the provenance of an older claim.

## Core entities

```text
GOAL
PROJECT
COMMITMENT
TASK
RELATIONSHIP
PREFERENCE
CONSTRAINT
OPEN_LOOP
INTENT
CONTEXT_FACT
STATE_TRANSITION
```

Each entity has provenance, confidence where applicable, classification, integrity status and lifecycle metadata.

## Goal

A desired outcome maintained over time.

```text
id
statement
priority
status
owner
created_at
validity
provenance
```

Priority is descriptive state unless explicitly supplied or authorized by the human/policy layer. The model cannot silently redefine human priorities.

## Project

A bounded collection of goals, tasks, resources and commitments.

A project MAY contain dependencies and open loops. Project state must remain reconstructible from evidence and state transitions.

## Commitment

An obligation or promised future action involving one or more actors.

Commitments require explicit provenance. A model inference is not sufficient to establish that a human made a commitment.

## Open loop

A relevant unresolved state requiring future attention, verification or closure.

Examples:

```text
awaiting_reply
pending_document
unresolved_decision
scheduled_followup
unfinished_task
```

Open loops have expiry/freshness semantics and may generate attention candidates but do not automatically authorize action.

## Intent

Intent is a structured candidate describing what an actor may want to achieve.

```text
intent_id
actor
objective
target
constraints
confidence
source_evidence
status
expires_at
```

Intent states:

```text
CANDIDATE → VERIFIED → ACCEPTED
             └──────→ REJECTED
             └──────→ EXPIRED
```

Inferred intent remains non-authoritative until verified according to policy.

## State transition

Human state is append-oriented:

```text
STATE(t0)
   ↓ event
STATE(t1)
   ↓ event
STATE(t2)
```

A component must not rewrite history merely to make the current state convenient.

## Confidence

Confidence is evidence quality, not truth.

A confidence value MUST have:

- source basis;
- calculation/version metadata;
- timestamp;
- applicable proposition;
- uncertainty status.

Numerical confidence never overrides policy, authorization or contradictory hard evidence.

## Conflict handling

Conflicting claims MUST remain explicitly represented until resolved.

```text
CLAIM_A ─┐
         ├── CONFLICT ──> RESOLUTION PROCESS
CLAIM_B ─┘
```

Resolution records which evidence changed the state and which claims were superseded, rejected or retained.

## Context boundary

Downstream reasoning receives a bounded context package, not unrestricted access to all human data.

```text
MEMORY
  ↓ relevance + policy filtering
CONTEXT PACKAGE
  ↓
REASONING
```

Context packages carry provenance and expiry/freshness metadata.

## Human authority

The system may assist with understanding, prediction, organization and execution of authorized operations.

The following remain outside implicit model authority:

- changing identity or credentials;
- financial commitments or transactions;
- legal commitments;
- destructive infrastructure operations;
- material physical-world safety actions;
- changing security policy or capability boundaries.

These require explicit authorization or a separately validated policy path.

## Privacy minimization

Only data required for the current purpose should enter a context package. Sensitive data SHOULD remain referenced rather than copied when possible.

## Required invariants

1. No raw external input becomes authority through ingestion.
2. Every state-bearing claim has provenance.
3. Current state and historical state remain distinguishable.
4. Inference cannot silently become fact.
5. Hypothesis cannot silently become authorization.
6. Conflicts remain visible until resolved.
7. Stale information cannot silently masquerade as current.
8. Model output never directly changes security policy or capability scope.
9. Human priorities cannot be silently rewritten by optimization logic.
10. Context is purpose-bounded and privacy-minimized.
11. Sensitive actions require policy and authorization independent of model confidence.
12. State transitions remain auditable and reconstructible.

## Acceptance gate

HUMAN_STATE_CONTRACT v0.1 is accepted only when test fixtures demonstrate:

```text
PROVENANCE
TEMPORALITY
CONFLICT
UNCERTAINTY
STATE TRANSITIONS
INTENT SEPARATION
PRIVACY BOUNDARY
AUTHORITY SEPARATION
```

Status: `SPECIFICATION / NOT YET IMPLEMENTED`.
