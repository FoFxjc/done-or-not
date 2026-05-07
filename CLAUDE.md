# CLAUDE.md

This repository defines a Claude Code plugin named **Done or Not**.

## Repo Intent

- Keep this repository markdown-first.
- Prefer commands, skills, and templates over runtime code.
- Do not add runtime complexity unless the user explicitly asks for it.

## Hard Boundaries

- Never modify product implementation as part of this plugin's intended
  behavior.
- The audited repository write boundary is `docs/implementation-audit/` only.
- Do not rename the project or the generated audit folder without user
  approval.
- Do not add package dependencies, CI workflows, servers, databases,
  background tasks, or automation layers in v1.

## Authoring Guidance

- Commands should be explicit, conservative, and usable through direct Claude Code invocation.
- Skills should enforce Git-context-first discovery and semantics-before-judgment.
- Templates should produce clean, future-automation-friendly markdown
  records.
- Prefer clear audit language over dramatic language.
- Avoid false positive fake findings.
- Confirm or strongly evidence semantics before authenticity judgment.

## Decision Rule

Use this rule everywhere:

```text
No semantics -> no fake verdict.
Draft semantics -> preliminary audit only.
Confirmed semantics -> real authenticity gate.
```
