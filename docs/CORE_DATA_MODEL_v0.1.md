# HUMAN-OS — Core Data Model v0.1

## Purpose
Define the canonical entities and invariants used by Context, Memory, Policy, Execution and Audit.

## Entity model

```text
TENANT
 └── HUMAN
      ├── IDENTITY
      ├── DEVICE
      ├── SESSION
      ├── CONTEXT
      ├── MEMORY
      │    ├── EPISODIC
      │    ├── SEMANTIC
      │    └── PROCEDURAL
      ├── INTENT
      ├── POLICY
      ├── CAPABILITY
      ├── ACTION
      └── PROOF
```

## Required metadata
Every persistent security-relevant object carries:

- `id`
- `created_at`
- `updated_at`
- `source`
- `provenance`
- `classification`
- `integrity_status`

Memory records additionally carry `confidence` and `valid_from` / `valid_until` when applicable.

## State separation

```text
OBSERVED_DATA
    !=
INFERENCE
    !=
HYPOTHESIS
    !=
DECISION
    !=
AUTHORIZATION
    !=
ACTION_RESULT
```

External content is never promoted to authority merely by ingestion.

## Core invariants

1. Every action references an actor, session and authorization context.
2. Every sensitive action has a policy decision before execution.
3. Memory writes retain provenance.
4. Revoked identities cannot authorize new actions.
5. An action cannot claim `SUCCESS` without a post-condition result.
6. Audit records cannot be altered through the normal application write path.
7. A model output is never itself an authorization.
8. Unknown or conflicting policy state fails closed for sensitive actions.
9. Tenant boundaries are explicit and enforced at persistence and execution layers.
10. Deletion or retention operations are themselves auditable actions.

## Canonical action lifecycle

```text
PROPOSED -> POLICY_CHECK -> AUTHORIZED -> EXECUTING -> VERIFIED
                         \-> DENIED
                         \-> BLOCKED
                         \-> EXPIRED
```

## Versioning
Schema changes must be versioned and backward compatibility must be evaluated before migration.
