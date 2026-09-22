# HUMAN-OS — Policy Engine v0.1

## Purpose
The Policy Engine is the deterministic authorization layer between intent/model output and execution.

## Rule

```text
MODEL OUTPUT
    ↓
NORMALIZE
    ↓
RISK CLASSIFY
    ↓
POLICY EVALUATE
    ↓
AUTHORIZE / DENY / BLOCK / EXPIRE
    ↓
EXECUTION GATE
```

## Policy inputs

- actor identity
- device trust state
- session state
- requested capability
- target resource
- action type
- data classification
- risk level
- current policy version
- authorization evidence
- temporal constraints
- rate/quantity limits

## Decision states

`ALLOW`, `DENY`, `BLOCKED`, `REQUIRES_HUMAN`, `EXPIRED`, `ERROR`.

`ALLOW` is valid only when all mandatory predicates evaluate positively.

## Capability model

Capabilities are explicit and scoped. Example:

```text
calendar.read
calendar.create
calendar.update
calendar.delete
```

A capability does not imply access to every resource. Resource scope, actor, session and policy still apply.

## High-impact classes

Financial transactions, destructive infrastructure operations, identity/credential changes, legal commitments and material physical-world actions require explicit human authorization unless a separately validated policy says otherwise.

## Fail-closed conditions

Sensitive execution is blocked when:

- authorization is missing or expired;
- identity is revoked;
- device trust is insufficient;
- policy evaluation is unavailable;
- policy versions conflict;
- target scope is ambiguous;
- required post-condition verification cannot be defined.

## Decision record

Every policy decision produces an auditable record containing:

```text
request_id
actor
session
capability
target
risk
policy_version
decision
reason_codes
authorization_evidence
timestamp
```

## Separation of duties
The model may propose. The Policy Engine decides authorization. The Execution Gateway enforces the decision. The Audit layer records the evidence.

No model output, prompt, tool description or external document can directly grant a capability.
