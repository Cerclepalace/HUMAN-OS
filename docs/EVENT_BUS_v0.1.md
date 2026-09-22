# HUMAN-OS — Event Bus v0.1

## Purpose
Provide a durable event contract between device input, context ingestion, memory, reasoning, policy and execution without coupling those components to a specific model.

## Event envelope

```json
{
  "event_id": "evt_<unique>",
  "event_type": "<namespace.action>",
  "occurred_at": "<RFC3339>",
  "producer": "<trusted component>",
  "subject": "<tenant/human/resource>",
  "session_id": "<session>",
  "correlation_id": "<trace>",
  "classification": "public|private|sensitive|restricted",
  "provenance": "<source reference>",
  "payload": {},
  "schema_version": "0.1",
  "integrity": "<verification metadata>"
}
```

## Event classes

```text
input.received
context.updated
memory.proposed
memory.accepted
memory.rejected
intent.proposed
reasoning.completed
policy.requested
policy.decided
action.proposed
action.authorized
action.denied
action.started
action.completed
action.failed
security.alert
identity.revoked
recovery.started
recovery.completed
```

## Bus guarantees

- Events have unique identifiers.
- Ordering is guaranteed only within an explicit stream/aggregate where required.
- Consumers must be idempotent.
- Retries use bounded backoff and dead-letter handling.
- Sensitive payloads are minimized; references are preferred over copying secrets.
- Authorization is evaluated at the execution boundary, not inferred from event content.
- Event retention follows classification and policy.

## Failure semantics

A consumer failure must not silently convert an action into success. Execution state remains unresolved until a verified post-condition or explicit failure state is recorded.

## Model independence
The event contract contains semantic state, not model-specific hidden state. Models can therefore be replaced without changing the durable event protocol.
