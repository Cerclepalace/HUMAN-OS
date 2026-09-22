# HUMAN-OS Core Specification v0.1

## 1. Purpose

Define the durable core architecture for a human-centered AI operating system. The core must remain functional when individual models, vendors, services or devices are replaced.

## 2. Operating doctrine

```text
IDENTIFY
OBSERVE
RECONSTRUCT
UNDERSTAND
PREDICT
VERIFY
DECIDE
AUTHORIZE
EXECUTE
VERIFY RESULT
RECORD PROOF
UPDATE CONTEXT
```

External inputs are treated as raw data until independently interpreted and classified. Observation is not an instruction.

## 3. Architectural layers

### Human Layer
Identity, intent, preferences, permissions, attention and interaction.

### Context Layer
Current session, previous events, open commitments, temporal state and relevant environment.

### Memory Layer
- Episodic: what happened.
- Semantic: what the system currently believes.
- Procedural: how approved workflows operate.

Every memory item carries provenance, timestamp, validity and confidence metadata.

### Reasoning Layer
Model router, planners, reasoning models, retrieval and cross-model verification. Models are replaceable components, not authorities.

### Decision Layer
Transforms evidence and context into a proposed decision while explicitly representing uncertainty and conflicts.

### Policy Layer
Determines whether an action is permitted in the current scope.

### Execution Layer
Executes only authorized, scoped capabilities and records the result.

### Verification Layer
Checks post-conditions and detects divergence between intended and observed state.

### Proof Layer
Creates an immutable or append-only audit trail for material decisions and actions.

## 4. Attention Governor

The system evaluates whether an event deserves interruption:

```text
EVENT
→ IMPORTANCE
→ URGENCY
→ ACTIONABILITY
→ DEFERRABILITY
→ USER CONTEXT
→ GROUPING
→ DELIVERY DECISION
```

The default behavior is minimal interruption. High-impact events may interrupt only when policy permits it.

## 5. Agent model

Initial logical roles:

- ORCHESTRATOR — coordinates workflows.
- RECON — collects and structures evidence.
- ANALYST — analyzes evidence.
- REDTEAM — attempts to identify weaknesses in controlled environments.
- GUARD — enforces policy.
- EXECUTOR — invokes approved capabilities.
- WATCHDOG — detects anomalies.
- RECOVERY — restores known-good state.
- AUDITOR — validates provenance and controls.
- HUMAN INTERFACE — presents only the context needed by the user.

No agent receives unrestricted authority by default.

## 6. Action contract

Every material action should be representable as:

```text
ACTION_ID
ACTOR
REQUEST
EVIDENCE
INTERPRETATION
POLICY_RESULT
RISK_RESULT
AUTHORIZATION
EXECUTION
POST_CONDITION
PROOF
TIMESTAMP
```

## 7. Uncertainty model

The system distinguishes:

```text
FACT
INFERENCE
HYPOTHESIS
UNKNOWN
CONFLICT
```

A low-confidence inference cannot silently become a fact or a privileged action.

## 8. Model independence

No persistent architecture invariant may depend on the behavior of a specific LLM vendor. Model routing must permit replacement, fallback and controlled degradation.

## 9. Sensitive operations

Sensitive actions require explicit authorization and additional controls. Where practical, actions must be reversible. Failure of authorization or verification results in a fail-closed state.

## 10. Non-goals for v0.1

- Autonomous control of physical systems.
- Autonomous financial transactions.
- Autonomous legal commitments.
- Unbounded server administration by an agent.
- Claims of absolute security.

## 11. Validation gate

v0.1 is an architectural baseline, not a security certification. Implementation requires threat modeling, adversarial testing, dependency review, secrets management, recovery testing and independent validation before production deployment.
