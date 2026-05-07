---
description: Propose draft implementation-audit docs for docs/implementation-audit without writing files.
---

# propose-audit-docs

## When To Use This Command

Use this command after semantics discovery when the repository would benefit from persistent audit memory, but the user has not yet approved writing files.

## Operator Procedure

1. Review the current semantics discovery output and Git context.
2. Reuse the most recent discovery output from the current session when available.
3. Preserve discovery unknowns, candidate feature map entries, and conservative wording from that discovery.
4. Identify which long-lived audit-memory files should be created or updated.
5. Draft the intended contents at summary level.
6. Show the proposed file set and purposes clearly.
7. Ask for explicit approval before any write action.

## Required Behavior

- Do not write files in this command.
- This command must never modify product implementation.
- Propose docs only under `docs/implementation-audit/`.
- Keep proposed content conservative and semantically grounded.
- If semantics are weak, say so and keep the proposal provisional.
- Preserve discovery unknowns unless later tracing resolved them.
- Preserve candidate feature-map presence labels from discovery unless later tracing supports a change.
- Do not upgrade `Claimed`, `Observed`, or `Inferred` features to `Implemented`.
- Keep all unaudited features at `Authenticity Status: Not audited`.
- Do not resolve unknowns unless they were actually traced.
- Do not claim that an import path, test path, or runtime linkage is broken unless it was actually resolved, traced, or tested.
- If path validity was not verified, say `Not verified`, `Needs verification`, or omit the claim.
- Use conservative language such as `derived from CLAUDE.md, project docs, and initial codebase inspection; some items remain unconfirmed until feature audit`.
- Use placeholder tags in the form `[PLACEHOLDER: short description - tracked in doc or issue]` and never emit an empty placeholder shell.

## Proposed File Set

The proposal should cover:

- `docs/implementation-audit/README.md`
- `docs/implementation-audit/feature-map.md`
- `docs/implementation-audit/implementation-semantics.md`
- `docs/implementation-audit/placeholder-policy.md`
- `docs/implementation-audit/git-context.md`

Optional future records may also reference:

- `docs/implementation-audit/audits/YYYY-MM-DDTHHMM-<topic>.md`
- `docs/implementation-audit/decisions/YYYY-MM-DDTHHMM-<topic>.md`
- `docs/implementation-audit/merges/YYYY-MM-DDTHHMM-<topic>.md`

When the proposal is based on discovery, include an append-only discovery record path by default:

- `docs/implementation-audit/audits/YYYY-MM-DDTHHMM-project-semantics-discovery.md`

Describe `audits/` as dated discovery and feature audit records.

## Expected Output

```markdown
# Proposed Implementation Audit Docs

## Proposed Files
| Path | New/Update | Purpose |
|---|---|---|

## Draft Summary
- Feature map:
- Implementation semantics:
- Placeholder policy:
- Git context:
- Open PRs: Not checked from local context
- Remote: Not confirmed
- Unknowns retained from discovery:
- Discovery record path:

## Approval Required
These files will not be written until the user explicitly approves.
```
