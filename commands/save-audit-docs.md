---
description: Save approved audit-memory docs under
  docs/implementation-audit only.
---

# save-audit-docs

## When To Use This Command

Use this command only after the user has explicitly approved writing
audit-memory documents in the audited repository.

## Operator Procedure

1. Restate the allowed write boundary.
2. List the target paths and whether each file is new or existing.
3. Distinguish long-lived files from append-only records.
4. Update long-lived files carefully and avoid destructive overwrites.
5. Preserve changelog sections where the templates expect them.
6. When saving baseline docs after discovery, include an append-only
   discovery record by default unless the user declines it.
7. Write only under `docs/implementation-audit/`.
8. Report the exact write scope and safety check after completion.

## Required Behavior

- Never write outside `docs/implementation-audit/`.
- Never modify product implementation.
- Never touch tests, schemas, configs, package files, CI, or official
  docs outside the audit folder.
- Avoid overwriting append-only records in `audits/`, `decisions/`, and
  `merges/`.
- If any requested path would fall outside the write boundary,
  explicitly refuse each requested out-of-bound path verbatim before
  offering any replacement.
- For each refused path, state whether it is disallowed because it is
  outside `docs/implementation-audit/` or because it would modify
  product code, tests, or other protected areas.
- After refusing the out-of-bound paths, separately offer allowed
  replacements only under `docs/implementation-audit/`.
- Default baseline save flow may include
  `docs/implementation-audit/audits/YYYY-MM-DDTHHMM-project-semantics-discovery.md`.
- Any saved discovery record must clearly state:
  `This is a discovery record, not a feature authenticity verdict.`

## Allowed Write Targets

Examples:

- `docs/implementation-audit/README.md`
- `docs/implementation-audit/feature-map.md`
- `docs/implementation-audit/implementation-semantics.md`
- `docs/implementation-audit/placeholder-policy.md`
- `docs/implementation-audit/git-context.md`
- `docs/implementation-audit/audits/YYYY-MM-DDTHHMM-<topic>.md`
- `docs/implementation-audit/decisions/YYYY-MM-DDTHHMM-<topic>.md`
- `docs/implementation-audit/merges/YYYY-MM-DDTHHMM-<topic>.md`

Use timestamped filenames for append-only records so audit history remains durable and sortable.

## Expected Output

```markdown
# Save Audit Docs

## Write Scope
Only `docs/implementation-audit/` is writable.

## Requested Paths Review
| Requested Path | Requested Action | Allowed? | Reason |
|---|---|---|---|

## Files to Write
| Path | Action | Notes |
|---|---|---|

Default append-only discovery record when applicable:

`docs/implementation-audit/audits/YYYY-MM-DDTHHMM-project-semantics-discovery.md`

## Safety Check
- Product code modified: No
- Tests modified: No
- Schemas modified: No
- Config modified: No
- Outside audit folder modified: No

## Result
```
