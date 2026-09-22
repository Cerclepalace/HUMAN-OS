# HUMAN-OS — Memory Engine v0.1

## Purpose

Provide durable, provenance-preserving memory without turning storage into authority. The Memory Engine stores evidence-backed state, history, derived knowledge and procedures while preserving uncertainty, conflicts, temporal validity and deletion policy.

## Position in the system

```text
EVENT BUS
   ↓
MEMORY INGESTION
   ↓
CLASSIFY → VALIDATE → DEDUPE → RESOLVE/RETAIN CONFLICT
   ↓
MEMORY STORE
   ↓
INDEX / RETRIEVAL
   ↓
CONTEXT ENGINE
```

## Memory classes

### Episodic
Time-bound events and interactions.

### Semantic
Durable knowledge derived from accepted evidence.

### Procedural
Validated methods, routines and operating procedures.

Each class retains provenance and lifecycle metadata.

## Memory record

```text
memory_id
memory_type
subject
content_or_reference
classification
source
provenance
observed_at
valid_from
valid_until
confidence
uncertainty_state
integrity_status
schema_version
created_at
updated_at
supersedes
status
```

## Write pipeline

```text
RAW EVENT
  ↓
SOURCE VALIDATION
  ↓
CLASSIFICATION
  ↓
NORMALIZATION
  ↓
DEDUPLICATION
  ↓
TEMPORAL CHECK
  ↓
CONFLICT CHECK
  ↓
PROMOTION POLICY
  ↓
PERSIST
  ↓
INDEX
  ↓
AUDIT
```

## Promotion model

Raw observations do not automatically become semantic memory.

```text
OBSERVED
   ↓ evidence evaluation
CANDIDATE
   ↓ validation/policy
ACCEPTED MEMORY
```

A model may propose a memory record. It cannot grant itself authority to promote that record.

## Conflict model

Memory conflicts are first-class state:

```text
MEMORY_A ─┐
          ├─ CONFLICT_SET
MEMORY_B ─┘
```

Resolution MUST retain the original records and produce a traceable resolution event.

## Temporal model

Memory supports:

```text
recorded_at
observed_at
valid_from
valid_until
supersedes
```

Expired or superseded information remains available for historical reconstruction subject to retention policy.

## Retrieval

Retrieval is relevance-bounded and policy-aware.

The engine SHOULD rank candidates using explicit signals such as:

- temporal relevance;
- task relevance;
- source quality;
- freshness;
- confidence;
- relationship to active goals/projects;
- classification permissions.

Retrieval ranking is not truth ranking. A highly relevant item may still be uncertain or conflicting.

## Memory writes

Normal writes are append/version oriented. Silent destructive overwrite is prohibited by the data model.

Correction uses:

```text
NEW_RECORD
  → supersedes OLD_RECORD
  → preserve OLD_RECORD
  → record reason/evidence
```

## Retention and deletion

Retention is policy-driven. Deletion must itself be auditable and must distinguish:

```text
logical deletion
retention expiry
privacy deletion
cryptographic destruction
archival
```

Security/audit records may have separate retention requirements from user content.

## Poisoning resistance

Potentially untrusted sources are never treated as authoritative merely because they are stored.

The engine records source quality and provenance and supports quarantine/review for suspicious or contradictory data.

## Model independence

No model-specific hidden state is required for durable memory. Model outputs are converted into explicit structured propositions with provenance and uncertainty before persistence.

## Failure semantics

If validation, provenance, integrity or policy checks fail, the record is rejected or quarantined rather than silently accepted.

If indexing fails after durable persistence, the memory remains persisted and is retried; indexing failure cannot imply data loss.

## Required invariants

1. Every persistent memory has provenance.
2. Raw data and derived knowledge remain distinguishable.
3. Memory conflicts are explicit.
4. Historical records are not silently overwritten.
5. Confidence cannot override policy or hard contradictory evidence.
6. Sensitive memory is subject to classification and access control.
7. Retention/deletion is auditable.
8. Memory retrieval cannot bypass authorization boundaries.
9. Model outputs never directly become authoritative memory.
10. Memory remains portable and model-independent.

## Acceptance gate

Fixtures must prove provenance, temporal validity, deduplication, conflict preservation, supersession, retention behavior, access control and poisoning resistance.

Status: `SPECIFICATION / NOT YET IMPLEMENTED`.
