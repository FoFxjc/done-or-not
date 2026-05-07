---
description: Audit whether the current branch is ready to merge,
  including placeholder carryover and documentation alignment.
---

# audit-merge-readiness

## When To Use This Command

Use this command when the question is whether the current branch is
ready to merge into a target branch such as `dev`, `main`, or `master`.

## Operator Procedure

1. Gather Git context for the current branch and likely target branch.
2. Interpret branch type and strictness.
3. Determine whether the relevant feature scope is confirmed or
   inferred.
4. Assess completion evidence, placeholder carryover, and documentation
   alignment relative to the destination branch.
5. Distinguish active merge readiness from stable branch baseline review.
6. Produce a merge verdict or baseline readiness verdict without
   merging or modifying code.
7. Suggest a saved record path only when appropriate to the context.

## Required Behavior

- Distinguish `feature -> dev`, `dev -> main/master`, and stable
  baseline contexts.
- Do not merge, commit, rebase, or modify implementation.
- If feature scope is uncertain, return `Needs confirmation`.
- Evaluate placeholder carryover relative to the target branch's
  tolerance.
- If run on `main` or `master` with a clean working tree and no active
  source/target merge, enter Main Baseline Readiness Mode.
- In Main Baseline Readiness Mode, do not infer a prior or hypothetical
  feature-branch merge.
- In Main Baseline Readiness Mode, do not label the result as
  `Merge Verdict`.
- In Main Baseline Readiness Mode, state `No active merge is pending.`
- Only state `No active merge is pending.` in baseline mode.
- Never include `No active merge is pending.` when a feature-branch or
  other active merge context is detected and a merge verdict is
  produced.
- Do not suggest a `merges/` record when no merge is pending; suggest an
  `audits/YYYY-MM-DDTHHMM-main-baseline-readiness.md` record only if a
  saved record is desired.

## Strictness Guidance

- `feature/* -> dev`: focused strictness on the claimed feature
- `dev -> main/master`: high strictness, placeholders should rarely
  carry over
- `main/master` baseline: treat user-facing overclaim and
  non-operational paths as serious

## Expected Output: Active Merge Mode

```markdown
# Merge Readiness Audit

## Mode
- Mode: Feature Branch Merge Readiness / Dev Integration Readiness

## Git Context
- Current branch:
- Target branch:
- Working tree:
- Commits ahead:
- Changed files:

## Branch Interpretation
- Source branch type:
- Target branch type:
- Strictness:

## Feature Scope
- Confirmed feature:
- Inferred feature:
- Scope confidence:

## Verdict
- Merge Verdict: Ready / Ready with warnings / Blocked / Needs confirmation

## Completion Blockers
1.

## Placeholder Carryover
| Placeholder | Area | Current Status | Allowed in Target? | Required Action |
|---|---|---|---|---|

## Documentation Alignment
- README overclaim:
- Docs overclaim:
- Audit docs updated:

## Suggested Record
- If merge is pending:
  `docs/implementation-audit/merges/YYYY-MM-DDTHHMM-<topic>.md`
```

## Expected Output: Main Baseline Mode

```markdown
# Merge Readiness Audit

## Mode
- Mode: Main Baseline Readiness

## Git Context
- Current branch:
- Target branch: None
- Working tree:
- Commits ahead:
- Changed files:

## Branch Interpretation
- Source branch type:
- Target branch type: None
- Strictness:

## Feature Scope
- Confirmed feature:
- Inferred feature:
- Scope confidence:

## Verdict
- Main Baseline Verdict: Ready / Ready with warnings / Blocked / Needs confirmation
- No active merge is pending.

## Completion Blockers
1.

## Placeholder Carryover
| Placeholder | Area | Current Status | Allowed in Target? | Required Action |
|---|---|---|---|---|

## Documentation Alignment
- README overclaim:
- Docs overclaim:
- Audit docs updated:

## Suggested Record
- If reviewing `main` or `master` baseline with no active merge:
  `docs/implementation-audit/audits/YYYY-MM-DDTHHMM-main-baseline-readiness.md`
```

The mode field should select one active mode only.

In baseline mode, include the baseline verdict line and
`No active merge is pending.`

In feature-branch or other active merge mode, include the merge verdict
line and omit `No active merge is pending.`
