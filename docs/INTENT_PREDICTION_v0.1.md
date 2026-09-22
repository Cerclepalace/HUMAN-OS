# HUMAN-OS — Intent Prediction v0.1

## Purpose

Transform contextual evidence into explicit, bounded candidate intents without confusing prediction with human authorization.

## Pipeline

```text
CONTEXT SNAPSHOT
      ↓
SIGNAL EXTRACTION
      ↓
CANDIDATE INTENTS
      ↓
EVIDENCE + CONFIDENCE
      ↓
CONSTRAINT CHECK
      ↓
TEMPORAL / EXPIRY CHECK
      ↓
INTENT STATUS
```

## Intent object

```text
intent_id
actor
objective
target
source_evidence
context_id
constraints
confidence
uncertainty_state
created_at
expires_at
status
model_metadata
```

## Candidate generation

Intent candidates MAY be generated from:

- explicit user instructions;
- observed interaction patterns;
- active tasks;
- open loops;
- project dependencies;
- calendar/time context;
- previously validated procedures.

Predicted intent must always remain distinguishable from explicit human intent.

## Intent classes

```text
EXPLICIT
DERIVED
PREDICTED
UNKNOWN
CONFLICTED
```

`EXPLICIT` means the actor directly expressed the objective. `PREDICTED` means the system inferred a likely objective from evidence.

## Confidence

Confidence measures prediction support. It is not authorization and not truth.

Every prediction must be reproducible from its evidence references and model/policy version.

## Verification

Where an intent could cause external effects, verification is required before execution.

```text
PREDICTED
   ↓
LOW IMPACT → MAY SURFACE AS SUGGESTION
   ↓
MATERIAL IMPACT → REQUIRE HUMAN CONFIRMATION / POLICY PATH
```

## Temporal behavior

Predicted intents expire quickly unless renewed by fresh evidence. Old predictions must not remain active indefinitely.

## Contradiction

If evidence supports incompatible objectives:

```text
INTENT_A ─┐
          ├→ CONFLICTED
INTENT_B ─┘
```

The system surfaces uncertainty instead of selecting an arbitrary intent.

## Model ensemble

Multiple models MAY independently generate or critique intent candidates. Agreement increases evidentiary support but does not grant authority.

Disagreement is a first-class signal:

```text
MODEL_A → intent A
MODEL_B → intent B
MODEL_C → uncertain

RESULT → MODEL_CONFLICT
```

## Prompt/data injection defense

Instructions contained in untrusted content are treated as observations/data. They cannot redefine the system's objective, policy, identity or capability scope.

## Required invariants

1. Predicted intent is never equivalent to explicit human intent.
2. Every intent has evidence references.
3. Every prediction expires or is refreshed.
4. Confidence never grants authorization.
5. Model disagreement remains visible.
6. Conflicting intent candidates remain explicit.
7. Untrusted content cannot redefine system authority.
8. Material external actions require verification and policy authorization.
9. Intent generation is model-independent at the durable schema level.
10. Every accepted intent is auditable.

## Acceptance gate

Fixtures must demonstrate explicit vs predicted intent, expiry, contradiction, model disagreement, prompt injection resistance and authorization separation.

Status: `SPECIFICATION / NOT YET IMPLEMENTED`.
