# Positioning

Done or Not is a lightweight single-repo completion legitimacy layer for AI-assisted feature work.

It validates whether claimed feature and project implementations inside a repository are actually real.

## Core Question

Is this claimed feature or project implementation actually real?

## What It Validates

- feature claims
- project implementation claims
- implementation evidence
- authenticity verdicts
- audit records

## What It Does Not Do

Done or Not is not:

- an Agent OS
- an orchestration engine
- a workflow platform
- a memory system
- a task tracker
- a task DAG
- a multi-agent controller
- a CI/CD engine
- an autonomous execution system

## Current Scope

Done or Not is currently single-repo and repo-local.

It focuses on:

- feature claims
- implementation evidence
- evidence-chain review
- authenticity verdicts
- audit records under `docs/implementation-audit/`

## Non-Goals

Done or Not does not try to become:

- a project management system
- a task lifecycle engine
- a workflow orchestrator
- a cross-session state layer
- a cross-project governance system
- a control plane for agent execution

## Design Principles

### Do not inherit narrative

An agent saying "done" is not evidence.

### Evidence before verdict

A feature claim should be checked against implementation evidence before being treated as real.

### No semantics, no fake verdict

Suspicious code is not enough. Done or Not first establishes what the repo claims the feature should do.

### Audit only

Done or Not may judge implementation authenticity, but it must not modify product implementation.

### Keep the scope repo-local

The goal is to verify implementation legitimacy inside a single repository, not to coordinate work across repositories or agents.

## Why It Exists

AI-assisted development can produce code that looks complete but is only UI-only, schema-only, stubbed, mock-backed, or not aligned with the claimed feature.

Done or Not turns "done" into an evidence-backed audit record.
