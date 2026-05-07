# Implementation Audit Memory

This folder stores implementation audit records for the repository.

It does not replace official product documentation. It preserves audit
context that helps future reviewers understand what was believed, what
was confirmed, what remained uncertain, and what evidence supported
merge or completion claims.

## What Belongs Here

- feature semantics and feature map history
- implementation semantics and completion standards
- placeholder policy and branch-aware exceptions
- dated discovery and feature audit records
- explicit audit decisions
- merge readiness records
- Git context snapshots

## Interpretation Rules

- Confirmed documentation and explicit user decisions take precedence over inferred findings.
- Inferred semantics should be marked clearly.
- Preliminary audits should not be treated as final authenticity verdicts.
- Discovery records are not feature authenticity verdicts.

## Write Boundary Reminder

This folder is the only permitted write target for Done or Not in the audited repository:

```text
docs/implementation-audit/
```

## Folder Conventions

- `feature-map.md`: long-lived feature inventory
- `implementation-semantics.md`: completion and evidence-chain policy
- `placeholder-policy.md`: placeholder interpretation rules
- `git-context.md`: latest Git snapshot for audit context
- `audits/`: dated discovery and feature audit records named `YYYY-MM-DDTHHMM-<topic>.md`
- `decisions/`: durable semantic or policy decisions named `YYYY-MM-DDTHHMM-<topic>.md`
- `merges/`: merge readiness records named `YYYY-MM-DDTHHMM-<topic>.md`
