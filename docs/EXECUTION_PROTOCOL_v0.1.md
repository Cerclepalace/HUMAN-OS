# HUMAN-OS — Execution Protocol v0.1

## Objective

Separate observation, reasoning, authorization and execution so that an AI model cannot convert untrusted input into an uncontrolled action.

## Canonical flow

```text
EVENT
  -> INGEST
  -> CLASSIFY
  -> CONTEXT
  -> REASON
  -> PLAN
  -> RISK
  -> POLICY
  -> AUTHORIZE
  -> EXECUTE
  -> VERIFY
  -> AUDIT
```

## Action envelope

Every executable operation should resolve to a canonical action envelope containing at minimum:

```text
action_id
actor
session_id
capability
resource
operation
arguments
source_context
risk_level
authorization
expiry
expected_postcondition
```

## Capability model

Capabilities should be narrow and explicit. Example:

```text
capability: calendar.read
resource: user.calendar
operation: READ
scope: current-user
expiry: session
```

A capability must not implicitly grant adjacent permissions.

## Authorization

Authorization is evaluated by the policy layer, independently of model-generated prose. A model may propose an action; it cannot grant itself the capability required to execute it.

## Verification

For state-changing operations, the executor should verify the expected post-condition. If verification fails, the action status is not `SUCCESS` even if the remote API returned a successful transport response.

## Audit record

The system records:

```text
REQUESTED
AUTHORIZED / DENIED
EXECUTED / NOT_EXECUTED
POSTCONDITION_VERIFIED / FAILED / UNKNOWN
FINAL_STATUS
```

## Sensitive action policy

Financial transactions, destructive infrastructure operations, credential changes, legal commitments and materially safety-relevant physical actions require explicit policy controls and must not be exposed through unrestricted autonomous execution.

## Security principle

```text
MODEL OUTPUT != AUTHORIZATION
API SUCCESS != VERIFIED STATE
DATA != INSTRUCTION
```
