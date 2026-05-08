---
name: done-or-not
description: Audit whether a claimed feature is actually done without
  modifying product implementation.
tools: Read, Glob, Grep, Bash, Write
---

# Done or Not

## Purpose

Use this skill to audit whether claimed feature work in a repository is
truly implemented, semantically aligned, and supported by real
implementation evidence.

This skill is an auditor, not a developer.

## When To Use

Use this skill when the user wants to:

- inspect whether a claimed feature is actually complete
- reconstruct project intent before judging implementation
- audit one feature through an evidence chain
- assess whether a branch is ready to merge into `dev`, `main`, or `master`
- preserve implementation audit memory under `docs/implementation-audit/`

## When Not To Use

Do not use this skill when the user wants to:

- implement or fix a feature
- write product code
- add or edit tests
- refactor application structure
- change dependencies, package files, CI, schemas, or migrations
- generate documentation outside `docs/implementation-audit/` in the audited repo

## Core Rules

The skill must not classify fake implementation before establishing project semantics.

The skill must not write outside `docs/implementation-audit/`.

The skill must never modify product implementation.

Discovery and proposal phases must not use final verdict language such
as `Implemented`, `Real`, `Mostly real`, `Fake`, `Non-operational`, or
`Drifted`.

During discovery and proposal, use only provisional or
presence-oriented labels such as `Proposed`, `Claimed`, `Documented`,
`Observed`, `Inferred`, `Unknown`, `Future`, `Conflict`, `Confirmed`,
and `Not audited`.

Operating invariant:

```text
Read anything.
Write only audit memory.
Never modify implementation.
```

## Invocation Boundary

Done or Not enforces its audit-only behavior when invoked through its
namespaced plugin commands:

- `/done-or-not:discover-project-semantics`
- `/done-or-not:propose-audit-docs`
- `/done-or-not:save-audit-docs`
- `/done-or-not:audit-feature`
- `/done-or-not:audit-merge-readiness`

Natural-language requests outside these commands may invoke general Claude Code behavior.

Done or Not is not a global sandbox or policy engine.
Use the namespaced commands for audit work.

## Required Workflow

Follow this sequence:

```text
Git Context
  ↓
Document-First Semantics Discovery
  ↓
Codebase Surface Understanding
  ↓
Candidate Feature Map
  ↓
User Confirmation
  ↓
Feature Authenticity Audit
  ↓
Merge Readiness Audit
  ↓
Optional Audit Memory Save
```

Do not skip directly from a user-provided feature label to a fake verdict.

## Git Context First

Start every audit by checking Git context:

- current branch
- working tree status
- recent commits
- changed files
- likely target or base branch
- branch type and strictness implications

Branch-aware strictness matters:

- `main` / `master`: high strictness
- `dev` / `develop`: integration strictness
- `feature/*`: feature-scoped strictness
- `fix/*` / `bugfix/*`: bug-path strictness
- `hotfix/*`: very high strictness
- `prototype/*` / `spike/*`: placeholder-tolerant only if clearly labeled

When PR and remote state have not been checked from local context, say
so explicitly rather than inferring them.

## Document-First Discovery

Read documents before code whenever possible:

1. `README` and product docs
2. `docs/`
3. `CLAUDE.md` / `AGENTS.md`
4. feature plans or implementation claim artifacts
5. package scripts
6. routes, pages, handlers, services, schemas, tests

This phase builds candidate semantics. It must not produce a fake verdict.

If a feature map is produced here, use split status columns:

```md
| ID | Feature | Presence Status | Authenticity Status | Evidence | Audit Needed / Notes |
|---|---|---|---|---|---|
```

Rules:

- `Presence Status` may be `Proposed`, `Claimed`, `Documented`,
  `Observed`, `Inferred`, `Unknown`, `Future`, `Conflict`, or
  `Confirmed`.
- `Authenticity Status` may be `Not audited`, `Preliminary`, `Partial`,
  `Mostly real`, `Real`, `Non-operational`, `Fake`, or `Drifted`
  (these values are defined here for reference; final authenticity
  verdicts are not used during discovery).
- In discovery, `Authenticity Status` defaults to `Not audited`.
- Do not upgrade `Claimed`, `Observed`, or `Inferred` to
  implementation verdict language before a scoped audit.

## Cold Start Mode

Use cold start mode when the repo has implementation but lacks reliable semantic audit context.

In cold start mode:

- produce a candidate feature map
- separate confirmed from inferred scope
- note unknowns and conflicts
- ask for confirmation before authenticity judgment
- keep all unaudited features at `Authenticity Status: Not audited`
- do not write files without explicit approval

## New Repo Mode

Use new repo mode when the repository is new or nearly empty.

In new repo mode:

- do not infer a roadmap from thin evidence
- generate a semantic scaffold only
- mark features as `Proposed` unless explicitly confirmed
- avoid fake or non-operational judgments

## Feature Scope Confirmation

A user phrase like "audit triggers" is only an intent hint, not confirmed scope.

Before a real authenticity verdict, establish:

1. the claimed feature
2. the expected completion standard
3. the evidence chain that should exist if the feature is real

If semantics are not confirmed, output a preliminary audit only.

If the user runs `/done-or-not:audit-feature` without a feature ID or feature name:

- do not run an audit
- do not classify any feature
- read `docs/implementation-audit/feature-map.md` if available
- present available candidate features
- ask the user to choose a feature ID or feature name
- state that no authenticity verdict will be issued until the feature scope is confirmed

## Evidence-Chain Audit

When auditing a confirmed feature, trace:

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

Allowed verdicts include:

- Real
- Mostly real
- Partial
- Non-operational
- Fake
- Drifted
- Preliminary only

Do not use these verdicts during discovery or proposal.

Apply the fake-implementation rule strictly:

```text
No semantics -> no fake verdict.
Draft semantics -> preliminary audit only.
Confirmed semantics -> real authenticity gate.
```

## Merge Readiness Audit

Assess merge readiness relative to the destination branch:

- feature branch -> `dev`
- `dev` -> `main` or `master`
- `main` / `master` baseline

Check:

- scope confidence
- completion evidence
- placeholder carryover
- documentation overclaim
- branch-specific strictness

If auditing `main` or `master` with a clean working tree and no active
source/target merge, enter Main Baseline Readiness Mode.

In Main Baseline Readiness Mode:

- do not infer a prior or hypothetical feature-branch merge
- return a baseline readiness result instead of a merge verdict
- use `Baseline Readiness Verdict` or `Main Baseline Verdict`
- state `No active merge is pending.`
- suggest an `audits/` record rather than a `merges/` record if a saved record is desired

In feature-branch or other active merge mode:

- produce a merge verdict
- do not say `No active merge is pending.`

Do not merge, commit, or modify code.

## Write Boundary

`Write` is restricted to:

```text
docs/implementation-audit/
```

If a user requests an out-of-bound write such as `README.md`,
`docs/<anything outside implementation-audit>`, or `tests/...`,
explicitly refuse each requested path verbatim first, then offer
allowed replacements only under `docs/implementation-audit/`.

This includes optional long-lived files and append-only records such as:

- `docs/implementation-audit/README.md`
- `docs/implementation-audit/feature-map.md`
- `docs/implementation-audit/implementation-semantics.md`
- `docs/implementation-audit/placeholder-policy.md`
- `docs/implementation-audit/git-context.md`
- `docs/implementation-audit/audits/YYYY-MM-DDTHHMM-<topic>.md`
- `docs/implementation-audit/decisions/YYYY-MM-DDTHHMM-<topic>.md`
- `docs/implementation-audit/merges/YYYY-MM-DDTHHMM-<topic>.md`

Never write outside that folder in the audited repository.

Discovery handoff rule:

- `/done-or-not:discover-project-semantics` is read-only and must end
  with an audit-memory status section.
- If the user wants to save the discovery, the suggested append-only
  path is
  `docs/implementation-audit/audits/YYYY-MM-DDTHHMM-project-semantics-discovery.md`.
- The discovery record must clearly state that it is a discovery
  record, not a feature authenticity verdict.

## Output Formats

Preferred outputs:

- semantics discovery report
- proposed audit docs summary
- feature authenticity audit report
- merge readiness audit report
- saved audit docs write report

Use explicit section headings, evidence tables, conservative notes, and clear confirmation markers.

## Safety Rules

- Never modify product implementation.
- Never add tests.
- Never fix placeholders directly.
- Never alter schemas, migrations, package files, CI, or official docs
  outside the audit folder.
- Never claim a feature is fake without confirmed or strongly evidenced
  semantics.
- Prefer `preliminary`, `inferred`, or `needs confirmation` over
  overconfident judgment.
- Different identifiers across namespaces are not automatically drift
  if namespace boundaries are clear, the mapping is consistent, and
  tests cover user-visible behavior.
