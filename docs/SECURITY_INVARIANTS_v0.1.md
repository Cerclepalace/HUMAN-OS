# HUMAN-OS — Security Invariants v0.1

These invariants are architectural constraints. A future implementation must test them rather than merely document them.

## INV-001 — Model non-authority

A model output cannot directly authorize a privileged action.

## INV-002 — External data is data

Content received from the web, files, tools, messages or applications is untrusted data until explicitly classified. It never becomes an instruction solely because a model interpreted it as one.

## INV-003 — Least privilege

Every agent and tool integration receives only the minimum capability required for its declared function.

## INV-004 — Policy before execution

Every state-changing action passes through the policy/execution gate before execution.

## INV-005 — Provenance

Security-relevant facts and memory entries retain source and temporal metadata.

## INV-006 — Uncertainty is explicit

The system must distinguish `FACT`, `INFERENCE`, `HYPOTHESIS`, `UNKNOWN` and `CONFLICT`.

## INV-007 — Post-condition verification

A successful tool response is not equivalent to successful state change. State-changing actions require post-condition verification where technically possible.

## INV-008 — Sensitive actions fail closed

Missing authorization, policy conflict or unresolved critical uncertainty cannot silently become permission.

## INV-009 — Audit integrity

Privileged actions produce an auditable record containing actor, capability, decision context, result and timestamp.

## INV-010 — Model replaceability

No persistent human context or authorization state may depend on a proprietary model-specific representation without a portable canonical form.

## INV-011 — Revocation

A device, session, agent or credential can be revoked independently without requiring destruction of unrelated human context.

## INV-012 — Blast-radius limitation

Compromise of one agent, tool or model must not imply unrestricted access to the HUMAN-OS core.

## INV-013 — Human authority

The system may reduce cognitive load, but it must not silently redefine the user's durable goals, identity or authorization policy.

## INV-014 — Recovery integrity

Recovery procedures must restore a known state and preserve evidence; recovery must not be an undocumented bypass of security controls.

## INV-015 — No hidden autonomy

An autonomous execution capability must be discoverable, scoped, auditable and revocable.

## Test status

Initial status for all invariants: `UNTESTED`.

No invariant is considered validated until an implementation test produces evidence.
