# Implementation Semantics

Derived from `CLAUDE.md`, project docs, and initial codebase
inspection; some items remain unconfirmed until feature audit.

## Default Completion Standard

A feature should not be considered complete unless the required behavior
is supported by an evidence chain appropriate to the repository and
branch context.

## Evidence Chain Definition

Expected chain:

```text
UI
  ↓
handler/action
  ↓
API/service
  ↓
schema/state
  ↓
persistence
  ↓
business behavior
  ↓
failure path
  ↓
tests
  ↓
documentation claim alignment
```

Not every feature uses every layer identically, but the audit should
explain what equivalent evidence exists or why a layer is not
applicable.

## Fake Implementation Rule

A fake implementation finding requires all three:

1. A confirmed or strongly evidenced feature claim
2. A completion expectation visible to users, feature claims, or documentation
3. Missing or contradictory implementation evidence

Rule:

```text
No semantics -> no fake verdict.
Draft semantics -> preliminary audit only.
Confirmed semantics -> real authenticity gate.
```

## Preliminary Vs Confirmed Audits

- Preliminary audit: semantics are inferred, disputed, or incomplete
- Confirmed audit: semantics are anchored by explicit user confirmation
  or official project documentation

Preliminary audits should not be treated as final claims of falseness or
merge blockage unless the user explicitly accepts the inferred scope.

## Interpretation Notes

- Confirmed docs and decisions outrank inferred implementation shape.
- Documentation drift should be separated from implementation falseness.
- Missing tests matter, but test absence alone does not prove a feature
  is fake.

## Implementation Artifact Status

| Artifact | Presence | Behavior Audit | Notes |
|---|---|---|---|
| `resolveAppMode()` | Observed | Not audited | Function exists; usage not traced |
| `trigger_marked_triggered` event | Documented | Not audited | Confirm emission path during scoped feature audit |

## Changelog

| Date | Change | Notes |
|---|---|---|
| YYYY-MM-DD | Initial record | |
