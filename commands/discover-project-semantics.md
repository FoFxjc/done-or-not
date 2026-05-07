---
description: Discover Git context, project semantics, candidate features, and unknowns before any authenticity judgment.
---

# discover-project-semantics

## When To Use This Command

Use this command when you need to reconstruct project intent before judging implementation. This command is read-only and should be the default starting point for any serious audit.

## Operator Procedure

1. Inspect Git context before reading implementation details.
2. Detect whether the repository is a new repo, cold start, existing audited project, feature branch, dev baseline, or main baseline.
3. Read documents before code.
4. Inspect the repository shape and implementation surface conservatively.
5. Build a candidate feature map with presence labels and audit follow-ups.
6. List unknowns, conflicts, and follow-up questions.
7. Propose audit-memory documents, but do not write them.
8. End with an audit-memory handoff section explaining how to save the discovery.

## Required Behavior

- This command is read-only.
- This command must never modify product implementation.
- Do not classify fake implementations here.
- Do not write any files.
- A user-provided feature name is only a scope hint until semantics are confirmed.
- Prefer documented intent over inferred code semantics when the two conflict.
- Do not use final authenticity verdict language here, including `Implemented`, `Real`, `Mostly real`, `Fake`, `Non-operational`, or `Drifted`.
- If a feature map is produced here, `Authenticity Status` must default to `Not audited`.

## Suggested Inspection Order

1. Git state and branch context
2. README and official docs
3. `docs/`
4. `CLAUDE.md` / `AGENTS.md`
5. feature plans or implementation claim artifacts
6. top-level repo shape
7. routes, pages, handlers, services, schemas, tests

## Git Context Checklist

Inspect:

- current branch
- working tree status
- recent commits
- changed files
- likely base branch
- branch naming cues
- whether `docs/implementation-audit/` already exists

Interpret strictness conservatively:

- `main` / `master`: stable baseline
- `dev` / `develop`: integration baseline
- `feature/*`: active feature scope
- `fix/*` / `bugfix/*`: bug path scope
- `prototype/*` / `spike/*`: placeholder-tolerant, but still evidence-aware

## New Repo / Cold Start Rules

If the repo is new or nearly empty:

- enter new repo mode
- do not infer a roadmap from thin evidence
- propose semantic scaffolding only

If the repo has code but no stable semantic audit context:

- enter cold start mode
- build a candidate feature map
- avoid fake verdicts
- require user confirmation before authenticity auditing

## Expected Output

```markdown
# Project Semantics Discovery

## Mode
- Mode: New Repo
- Mode: Cold Start
- Mode: Existing Project
- Mode: Feature Branch
- Mode: Dev Baseline
- Mode: Main Baseline

## Git Context
- Current branch
- Working tree status
- Recent commits
- Changed files
- Likely base branch
- Branch interpretation
- Audit strictness implication
- Open PRs: Not checked from local context
- Remote: Not confirmed

## Documentation Sources
| Source | Found | Notes |
|---|---:|---|

## Repository Shape
| Area | Evidence | Interpretation |
|---|---|---|

## Candidate Feature Map
| ID | Feature | Presence Status | Authenticity Status | Evidence | Audit Needed / Notes |
|---|---|---|---|---|---|

## Unknowns
1.
2.
3.

## Recommended Next Step
- These unknowns are recommended entry points for scoped feature audits.
- You do not need to resolve all unknowns before auditing one feature.
- Pick one unknown or one feature and run `/done-or-not:audit-feature`.

## Audit Memory Status

- `docs/implementation-audit/`: Found / Not found
- Files written by this command: None
- Reason: discovery is read-only

## To Save This Discovery

Run:

1. `/done-or-not:propose-audit-docs`
2. Review the proposed docs
3. `/done-or-not:save-audit-docs`

Suggested append-only record path:

`docs/implementation-audit/audits/YYYY-MM-DDTHHMM-project-semantics-discovery.md`
```

The mode field must print exactly one selected mode, not a mixed menu. A short explanation may follow the selected mode.
