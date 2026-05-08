# Feature Authenticity Audit: <Feature>

## Audit Scope

- Recorded at:
- Source branch:
- Audit scope status:
- Report type:
- Feature:
- Scope status:
- Current branch:
- Strictness:
- Out of scope:

## Record Note

- This template may also be used for dated discovery records and baseline readiness records.
- A discovery record must state:
  `This is a discovery record, not a feature authenticity verdict.`
- A main baseline readiness record should avoid merge wording when no
  active merge is pending.

## Expected Behavior

- Based on confirmed docs or user decisions:
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

- Classification:
- Severity:
- Evidence:
- Why it matters:
- Required fix before claiming complete:
- Suggested verification test:

## Verdict

- Real / Mostly real / Partial / Non-operational / Fake / Drifted / Preliminary only

## Namespace Alignment Notes

- Different identifiers across namespaces are not automatically drift.
- Example mappings such as persistence status `<PersistenceState>`,
  event type `<event-name>`, internal label `<InternalState>`, and
  product copy `<UserVisibleState>` may all be acceptable when
  namespace boundaries are clear, the mapping is consistent, and tests
  cover user-visible behavior.

## Completion Blockers

1.

## Risk Highlights

1.

## Existing Placeholders

1.

## Suggested Next Step

- These unknowns are recommended entry points for scoped feature audits.
- You do not need to resolve all unknowns before auditing one feature.
- Pick one unknown or one feature and run `/done-or-not:audit-feature`.
