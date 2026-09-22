# HUMAN-OS — Attention Governor v0.1

## Purpose

Manage the human's attention budget by deciding how system events are surfaced, grouped, deferred or suppressed.

The Governor controls interruption, not truth or authorization.

## Core objective

```text
MAXIMIZE USEFUL ATTENTION
MINIMIZE UNNECESSARY INTERRUPTION
```

## Decision pipeline

```text
EVENT
 ↓
CONTEXT
 ↓
RELEVANCE
 ↓
URGENCY
 ↓
IMPACT
 ↓
CONFIDENCE
 ↓
DUPLICATION / GROUPING
 ↓
ATTENTION POLICY
 ↓
SURFACE DECISION
```

## Surface states

```text
SILENT
GROUPED
DIGEST
SUGGESTION
CONFIRMATION
INTERRUPT
```

`INTERRUPT` is exceptional and must satisfy explicit criteria.

## Decision factors

```text
relevance
urgency
consequence_of_delay
confidence
freshness
user_attention_state
active_task
quiet_period
relationship_priority
security_criticality
```

These factors produce a routing decision, not a truth score.

## Zero-bombardement rule

Repeated or correlated events SHOULD be collapsed into a single attention object when doing so does not hide material information.

```text
20 related notifications
        ↓
1 attention group
```

Material security or safety signals may bypass normal grouping according to policy.

## Interruption contract

An interrupt candidate MUST contain:

```text
reason
source
context
urgency_basis
confidence
expected_user_action
expiry
policy_basis
```

The user must be able to understand why the interruption occurred.

## Prediction integration

Predicted intent can create an attention candidate but cannot directly force an interrupt.

```text
PREDICTION → CANDIDATE
              ↓
       ATTENTION POLICY
              ↓
       SURFACE DECISION
```

## Attention budget

The system SHOULD track short-term attention load and avoid unnecessary context switching.

Budget state is operational metadata, not a judgment about the human.

## Quiet periods

Quiet periods suppress non-critical surfaces. Security-critical events and explicitly authorized exceptions follow policy-defined handling.

## Failure semantics

If relevance or urgency cannot be safely determined, default behavior for ordinary events should favor deferral/grouping rather than speculative interruption. Security-critical events follow their dedicated policy.

## Required invariants

1. Attention routing does not alter source truth.
2. Prediction does not directly create interruption authority.
3. Every interrupt has a reason and provenance.
4. Duplicate events can be grouped without losing material evidence.
5. Quiet periods are policy-aware.
6. Security-critical handling remains policy-controlled.
7. Missing context cannot be fabricated to justify interruption.
8. The user can inspect the basis of a material interrupt.
9. Attention decisions are auditable.
10. The Governor cannot authorize external actions.

## Acceptance gate

Fixtures must prove grouping, quiet periods, urgent routing, prediction separation, explanation/provenance, attention budget behavior and security exception handling.

Status: `SPECIFICATION / NOT YET IMPLEMENTED`.
