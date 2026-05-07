# Done or Not

> Check whether "done" is actually done.

Done or Not is a Claude Code plugin for auditing whether claimed
AI-assisted feature work is actually implemented.

It is markdown-first and audit-only: it reads a repository, compares
claims against implementation evidence, and can save audit memory under
`docs/implementation-audit/` in the target repo.

Current version: `v0.1.2`

## What It Does

- discovers project semantics before judging implementation
- builds a candidate feature map
- separates feature presence from implementation authenticity
- audits one confirmed feature through an evidence chain
- checks merge readiness or main-baseline readiness
- proposes or saves audit memory under `docs/implementation-audit/` with approval

## What It Does Not Do

- does not modify product code
- does not add tests
- does not fix bugs
- does not change schemas
- does not change CI
- does not commit, merge, or deploy
- does not act as a global sandbox

## Requirements

- Claude Code CLI

## Installation

From the CLI:

```bash
claude plugin marketplace add FoFxjc/done-or-not
claude plugin install done-or-not@fofxjc
```

From within a Claude Code session:

```text
/plugin marketplace add FoFxjc/done-or-not
/plugin install done-or-not@fofxjc
```

## Updating

From the CLI:

```bash
claude plugin marketplace update fofxjc
claude plugin update done-or-not@fofxjc
```

From within a Claude Code session:

```text
/plugin marketplace update fofxjc
/plugin update done-or-not@fofxjc
```

## Usage

Primary commands:

```text
/done-or-not:discover-project-semantics
/done-or-not:propose-audit-docs
/done-or-not:save-audit-docs
/done-or-not:audit-feature
/done-or-not:audit-merge-readiness
```

Typical flow:

```text
Discover project semantics
  -> propose audit docs
  -> save audit baseline
  -> audit one feature
  -> audit merge readiness when needed
```

## How It Works

Done or Not is a lightweight single-repo completion legitimacy layer
for AI-assisted feature work.

It validates whether claimed feature and project implementations inside
a repository are actually real.

It does not call a feature fake just because a code path looks
suspicious. It first establishes project semantics, then allows
stronger authenticity judgments only after scope is confirmed or
strongly evidenced.

Core rule:

```text
No semantics -> no fake verdict.
Draft semantics -> preliminary audit only.
Confirmed semantics -> real authenticity gate.
```

## Generated Audit Folder

```text
docs/implementation-audit/
├── README.md
├── feature-map.md
├── implementation-semantics.md
├── placeholder-policy.md
├── git-context.md
├── audits/
├── decisions/
└── merges/
```

This folder is the project audit trail. It does not replace official
product docs.

## Feature Status Model

Done or Not uses a split status model:

| Model Part | Allowed Values |
|---|---|
| Presence Status | `Claimed`, `Observed`, `Inferred`, `Confirmed` |
| Authenticity Status | `Not audited`, `Preliminary`, `Partial`, `Real`, `Non-operational`, `Fake`, `Drifted` |

Discovery and proposal phases never use final verdict language. During
discovery, features keep `Authenticity Status: Not audited`.

## Local Development

Validate the plugin manifest:

```bash
claude plugin validate .claude-plugin/plugin.json
```

Validate the marketplace manifest:

```bash
claude plugin validate .claude-plugin/marketplace.json
```

Load the plugin directly for local dogfooding:

```bash
claude --plugin-dir /path/to/done-or-not
```

If `/plugin` opens the generic plugin management UI and does not clearly
list commands in your terminal, inspect the [`commands/`](commands/)
directory or run a known namespaced command directly.

If `claude --plugin-dir` fails with an `EPERM` error involving
`~/.claude.json`, that is a local Claude CLI config or permission
issue, not a plugin validation failure. Some sandboxed runners also
cannot write under `~/.claude*`, which can block local plugin loading
even when the plugin itself is valid.

## File Structure

```text
done-or-not/
├── .claude-plugin/
│   ├── plugin.json
│   └── marketplace.json
├── commands/
├── skills/
├── templates/
├── docs/
│   └── positioning.md
├── CLAUDE.md
├── README.md
└── LICENSE
```

## Positioning

Done or Not is a lightweight single-repo completion legitimacy layer
for AI-assisted feature work.

It validates whether claimed feature and project implementations inside
a repository are actually real.

It is not an Agent OS, orchestration engine, workflow platform, memory
system, task tracker, or multi-agent controller.

It focuses on repo-local feature claims, implementation evidence,
authenticity verdicts, and audit records.

## License

Apache-2.0
