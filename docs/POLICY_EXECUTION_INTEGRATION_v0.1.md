# HUMAN-OS — Policy & Execution Integration v0.1

## Purpose

Define the complete control path from a proposed action to authorized execution and verified result.

## End-to-end path

```text
REASONING
   ↓
ACTION PROPOSAL
   ↓
RISK CLASSIFICATION
   ↓
POLICY ENGINE
   ↓
AUTHORIZATION
   ↓
EXECUTION GATEWAY
   ↓
TOOL / SERVICE
   ↓
POST-CONDITION VERIFICATION
   ↓
PROOF LOG
   ↓
CONTEXT UPDATE
```

## Action proposal

An action proposal contains:

```text
action_id
actor
session
intent_ref
reasoning_ref
capability
resource
parameters
risk_class
expected_post_condition
expires_at
provenance
```

The proposal is inert until authorization.

## Risk classification

Risk considers:

- reversibility;
- data sensitivity;
- external side effects;
- financial impact;
- identity/security impact;
- legal impact;
- physical-world impact;
- blast radius;
- uncertainty;
- target ambiguity.

Risk classification is recorded and versioned.

## Authorization boundary

Policy evaluates the complete action proposal and current security state. Authorization is explicit and scoped to:

```text
ACTOR
SESSION
CAPABILITY
RESOURCE
ACTION
PARAMETERS
TIME WINDOW
QUANTITY / RATE LIMIT
POLICY VERSION
```

Authorization cannot be inferred from model confidence, conversation context or previous unrelated authorization.

## Execution Gateway

The Execution Gateway is the only normal path to privileged tools/services.

It verifies:

```text
identity
session
capability
policy decision
authorization expiry
resource scope
parameter constraints
integrity
```

A failed check prevents execution.

## Capability isolation

Agents and tools receive the minimum capability required for the operation.

```text
agent
  ↓ capability token
execution gateway
  ↓ scoped operation
resource
```

Capability tokens must be bounded by actor, resource, operation and lifetime.

## Idempotency

Actions with external side effects require an idempotency strategy where supported.

Repeated requests must not silently create repeated side effects.

## Post-condition verification

Execution returning successfully is insufficient.

```text
TOOL RESPONSE
     ↓
OBSERVE ACTUAL STATE
     ↓
COMPARE EXPECTED POST-CONDITION
     ↓
VERIFIED / FAILED / UNKNOWN
```

`SUCCESS` is not recorded unless the post-condition is verified.

## Failure states

```text
DENIED
BLOCKED
EXPIRED
EXECUTION_FAILED
POST_CONDITION_FAILED
VERIFICATION_UNKNOWN
```

Partial external effects must be recorded as unresolved/partial state rather than represented as clean failure or success.

## Rollback

Where technically possible, reversible operations SHOULD define a rollback procedure before execution.

Rollback is itself an authorized action and must not bypass policy.

## High-impact actions

Financial transactions, destructive infrastructure changes, credential/identity changes, legal commitments and material physical-world actions require explicit human authorization or a separately validated policy path.

## Proof record

Every executed action produces:

```text
action_id
proposal
policy_decision
authorization_evidence
execution_start
execution_result
post_condition
verification_result
actor/session
capability
timestamps
errors
```

## Context feedback

Verified outcomes become events. The Context and Memory layers decide whether and how those outcomes become durable state.

```text
RESULT
 ↓
EVENT
 ↓
CONTEXT / MEMORY POLICY
```

Execution must never directly rewrite human state.

## Fail-closed conditions

Sensitive execution is blocked when required identity, authorization, scope, policy, integrity or post-condition verification is unavailable.

## Required invariants

1. No proposal executes without authorization.
2. Execution Gateway is the privileged boundary.
3. Capabilities are scoped and time-bounded.
4. Authorization is independent from model output.
5. External side effects use idempotency controls where possible.
6. Success requires verified post-condition.
7. Partial effects remain explicit.
8. Rollback cannot bypass policy.
9. Execution results feed the event/proof system.
10. Execution cannot directly rewrite trusted human state.

## Acceptance gate

Fixtures must prove authorization enforcement, scope isolation, expiry, idempotency, post-condition verification, partial failure, rollback authorization and proof generation.

Status: `SPECIFICATION / NOT YET IMPLEMENTED`.
