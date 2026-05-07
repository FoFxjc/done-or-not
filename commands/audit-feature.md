---
description: Audit a confirmed feature through an implementation
  evidence chain without modifying product code.
---

# audit-feature

## When To Use This Command

Use this command to audit one confirmed feature, or to produce a
preliminary audit when feature scope is still inferred and not yet
confirmed.

If invoked without a feature ID or feature name, this command should
enter Feature Selection Mode instead of treating the invocation as an
error.

## Operator Procedure

1. Check whether project semantics and feature scope are already confirmed.
2. If no feature ID or feature name was provided, enter Feature
   Selection Mode and stop before auditing.
3. If not confirmed, run or request semantics discovery first and keep
   the result preliminary.
4. Restate the feature, branch context, strictness, and out-of-scope areas.
5. Define expected behavior from confirmed docs and user decisions, then
   separate inferred expectations.
6. Trace the evidence chain from UI through documentation alignment.
7. Classify findings conservatively.
8. Produce a verdict, blockers, risk highlights, placeholders, and next step.

## Required Behavior

- Do not classify a feature as fake without confirmed or strongly evidenced semantics.
- This command must never modify product implementation.
- If scope is not confirmed, output `Preliminary` scope status and `Preliminary only` verdict.
- Recommend fixes if helpful, but never implement them.
- Focus on the selected feature, not unrelated repository issues.
- If no feature was specified, do not run an audit and do not classify any feature.
- In Feature Selection Mode, read
  `docs/implementation-audit/feature-map.md` if available and present
  candidate features for scope confirmation.
- State explicitly that no authenticity verdict will be issued until the
  feature scope is confirmed.

## Evidence Chain

Trace:

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

## Finding Classifications

Allowed classifications:

- Completion Blocker
- Risk Highlight
- Existing Placeholder
- Future Work
- Documentation Drift
- Non-Issue

## Verdict Rule

Apply this rule strictly:

```text
No semantics -> no fake verdict.
Draft semantics -> preliminary audit only.
Confirmed semantics -> real authenticity gate.
```

## Expected Output

If no feature ID or feature name was provided:

```markdown
# Feature Audit: Select Scope

## Status

No feature specified. Scope confirmation required.

## Candidate Features

| ID | Feature | Presence Status | Authenticity Status | Audit Needed / Notes |
|---|---|---|---|---|

## How to Continue

Reply with a feature ID or feature name, for example:

- F3
- DCA plans
- F4 Triggers
- Audit F4: Triggers

No authenticity verdict will be issued until the feature scope is confirmed.
```

Otherwise:

```markdown
# Feature Authenticity Audit: <Feature>

## Audit Scope
- Feature:
- Scope status: Confirmed / Inferred / Preliminary
- Current branch:
- Strictness:
- Out of scope:

## Expected Behavior
- Based on confirmed docs/user decisions:
- Based on inferred evidence:

## Evidence Chain
| Layer | Evidence | Status | Notes |
|---|---|---|---|
| UI | | Present/Missing/Partial | |
| Handler/Action | | Present/Missing/Partial | |
| API/Service | | Present/Missing/Partial | |
| Schema/State | | Present/Missing/Partial | |
| Persistence | | Present/Missing/Partial | |
| Business Behavior | | Present/Missing/Partial | |
| Failure Path | | Present/Missing/Partial | |
| Tests | | Present/Missing/Partial | |
| Documentation Alignment | | Present/Missing/Partial | |

## Findings
### Finding 1: <Title>
- Classification: Completion Blocker / Risk Highlight / Existing
  Placeholder / Future Work / Documentation Drift / Non-Issue
- Severity:
- Evidence:
- Why it matters:
- Required fix before claiming complete:
- Suggested verification test:

## Verdict
- Real / Mostly real / Partial / Non-operational / Fake / Drifted / Preliminary only

## Completion Blockers
1.

## Risk Highlights
1.

## Existing Placeholders
1.

## Suggested Next Step
```
