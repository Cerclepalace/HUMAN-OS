# HUMAN-OS — Reasoning Engine v0.1

## Purpose

Provide model-assisted reasoning over bounded, provenance-bearing context while preserving uncertainty, contradiction and strict separation from authorization.

## Core rule

```text
REASONING = ANALYSIS
REASONING != AUTHORIZATION
```

## Pipeline

```text
CONTEXT PACKAGE
   ↓
PROBLEM / OBJECTIVE NORMALIZATION
   ↓
EVIDENCE EXTRACTION
   ↓
MULTI-PATH REASONING
   ↓
CONTRADICTION CHECK
   ↓
UNCERTAINTY ASSESSMENT
   ↓
CANDIDATE CONCLUSION / PLAN
   ↓
POLICY HANDOFF
```

## Inputs

Reasoning receives only a policy-approved context package containing source references, temporal metadata, uncertainty state and relevant constraints.

## Outputs

```text
reasoning_id
question/objective
claims_used
assumptions
candidate_conclusion
candidate_actions
uncertainties
conflicts
model_metadata
policy_dependencies
created_at
```

## Evidence discipline

The engine must distinguish:

```text
OBSERVED
DERIVED
ASSUMED
UNKNOWN
CONFLICTING
```

Assumptions are never silently converted into observations.

## Multi-model verification

For material reasoning tasks, independent models MAY produce:

```text
ANALYSIS_A
ANALYSIS_B
CRITIQUE_A
CRITIQUE_B
```

A disagreement creates an explicit conflict/uncertainty state. Model consensus is supporting evidence, not authorization.

## Contradiction pass

Before producing a material conclusion, the engine SHOULD ask:

- What evidence contradicts the conclusion?
- Which assumptions are unsupported?
- Which data may be stale?
- Which source has weaker provenance?
- What information is missing?
- What alternative explanation remains plausible?

## Planning

Plans are decomposed into typed candidate steps:

```text
OBSERVE
RETRIEVE
CALCULATE
ASK
PROPOSE
EXECUTE
VERIFY
```

Execution steps are handed to Policy/Authorization and never executed by the reasoning layer itself.

## Model failure

If the model is unavailable, reasoning may degrade to deterministic rules or return `UNKNOWN`. A model failure must not be converted into a fabricated conclusion.

## Prompt injection

Instructions found inside retrieved documents, messages, websites or tool outputs are treated as untrusted content unless independently authorized by system policy.

## Required invariants

1. Reasoning receives bounded context.
2. Every material claim has evidence references.
3. Assumptions are explicit.
4. Contradictions remain visible.
5. Unknown remains unknown.
6. Model consensus does not grant authority.
7. Reasoning cannot directly invoke sensitive execution.
8. Model failure does not create fabricated state.
9. Model identity/version is recorded for reproducibility.
10. Every material reasoning result is auditable.

## Acceptance gate

Fixtures must demonstrate evidence traceability, contradiction detection, model disagreement, prompt-injection resistance, bounded context, model failure and separation from execution.

Status: `SPECIFICATION / NOT YET IMPLEMENTED`.
