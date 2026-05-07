# Feature Map

## Status Metadata

- Last updated:
- Updated by:
- Repository:
- Mode:
- Semantics confidence:

## Status Legend

### Presence Status

| Status | Meaning |
|---|---|
| Proposed | Mentioned intent, not yet confirmed |
| Claimed | Claimed in UI, feature plans, docs, or adjacent code, but not yet confirmed |
| Documented | Stated in official project docs |
| Observed | Directly observed in repository artifacts |
| Inferred | Inferred from evidence, needs confirmation |
| Unknown | Evidence is unclear or conflicting |
| Future | Explicitly not in current scope |
| Conflict | Sources disagree about scope or behavior |
| Confirmed | Accepted scope from user or official docs |

### Authenticity Status

| Status | Meaning |
|---|---|
| Not audited | No scoped authenticity audit has been completed yet |
| Preliminary | Early audit signal before confirmed scope |
| Partial | Some evidence exists but the chain is incomplete |
| Mostly real | Core behavior exists with limited gaps |
| Real | Evidence chain supports the feature claim |
| Non-operational | Presented as behavior but cannot execute meaningfully |
| Fake | Claimed complete without required core evidence |
| Drifted | Implementation diverges from intended behavior |

## Features

| ID | Feature | Presence Status | Authenticity Status | Evidence | Audit Needed / Notes |
|---|---|---|---|---|---|
| F-001 | | | Not audited | | |

## Rules

- During discovery, `Authenticity Status` defaults to `Not audited`.
- Audited features may later update `Authenticity Status`.
- Do not combine these into strings such as `Confirmed Real`.

## Examples

| ID | Feature | Presence Status | Authenticity Status | Evidence | Audit Needed / Notes |
|---|---|---|---|---|---|
| F4 | Triggers | Confirmed | Real | F4 audit record | Audited 2026-05-06 - no blockers; one low UX risk |
| F3 | DCA plans | Claimed | Not audited | src/app/dca/, schema | Confirm execution event emission |

## Changelog

| Date | Change | Notes |
|---|---|---|
| YYYY-MM-DD | Initial record | |
