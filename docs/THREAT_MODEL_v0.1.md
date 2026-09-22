# HUMAN-OS — Threat Model v0.1

## 1. Purpose

Define the security boundary for HUMAN-OS before autonomous execution is introduced.

## 2. Security objectives

- Protect human identity, context, memory, credentials and private data.
- Prevent unauthorized actions by models, agents, services or compromised devices.
- Minimize blast radius when a component fails or is compromised.
- Preserve provenance for security-relevant decisions and actions.
- Support recovery without silently weakening security controls.

## 3. Assets

| Asset | Examples | Required property |
|---|---|---|
| Identity | account, device identity, session | authenticity |
| Human Context | goals, commitments, preferences | confidentiality + integrity |
| Memory | episodic, semantic, procedural | integrity + provenance |
| Credentials | API keys, tokens, signing keys | confidentiality |
| Policies | permissions, safety rules | integrity |
| Actions | tool calls, external mutations | authorization + audit |
| Audit | evidence, decisions, results | integrity + retention |
| Models | local/cloud inference endpoints | isolation + replaceability |

## 4. Primary threat classes

### T01 — Credential compromise
A stolen credential is used to access HUMAN-OS or connected services.

Control direction: short-lived credentials, least privilege, isolated secrets, rotation and audit.

### T02 — Prompt/data injection
Untrusted content attempts to influence an agent as if it were an instruction.

Control direction: provenance labels, instruction/data separation, policy evaluation outside the model, tool-call validation.

### T03 — Model failure
A model produces an incorrect conclusion, unsafe plan or hallucinated fact.

Control direction: uncertainty states, deterministic policy checks, multi-model verification where justified, post-condition checks.

### T04 — Agent privilege escalation
An agent attempts an action outside its declared scope.

Control direction: capability-based permissions and an execution gateway that does not trust agent intent.

### T05 — Compromised device
A client device is partially or fully compromised.

Control direction: device identity, session limits, revocation, minimal local secrets and server-side authorization.

### T06 — Data poisoning
Incorrect or malicious information is persisted into long-term memory.

Control direction: source provenance, confidence, temporal validity, conflict states and memory write policies.

### T07 — Supply-chain compromise
A dependency, model, package or build artifact is malicious or compromised.

Control direction: pinned dependencies, provenance, signed artifacts where available, reproducible builds and dependency review.

### T08 — Audit tampering
An actor attempts to modify or erase evidence.

Control direction: append-oriented audit records, integrity protection, restricted write paths and independent retention.

## 5. Trust boundaries

```text
UNTRUSTED WORLD
      |
      v
EDGE / INPUT
      |
      v
CONTEXT INGESTION
      |
      v
HUMANOS CORE
      |
      +---- MEMORY
      +---- REASONING
      +---- POLICY
      +---- SECURITY
      |
      v
EXECUTION GATE
      |
      v
AUTHORIZED TOOLS
```

Data crossing a boundary must be classified and validated. External content is data, not authority.

## 6. High-impact action rule

The following classes require explicit policy treatment and must not be delegated to unrestricted autonomous execution:

- financial transactions;
- destructive infrastructure operations;
- credential or identity changes;
- legal commitments;
- physical-world actions with material safety implications.

## 7. Failure posture

For sensitive operations, uncertainty, policy conflict, missing authorization or failed verification should produce a fail-closed result rather than implicit permission.

## 8. Validation gate

HUMANOS v0.1 is not considered security-validated until each critical control has:

```text
CONTROL
  -> TEST
  -> OBSERVED RESULT
  -> EVIDENCE
  -> REVIEW
  -> STATUS
```

Status values: `PASS`, `FAIL`, `BLOCKED`, `UNKNOWN`.
