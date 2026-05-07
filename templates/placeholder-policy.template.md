# Placeholder Policy

## Placeholder Allowed Conditions

A placeholder may be tolerated when all relevant conditions hold:

- the branch context allows it
- the placeholder is clearly labeled
- the current feature claim does not overstate what exists
- the missing behavior is outside confirmed completion scope
- the placeholder does not create false user-facing confidence

## Placeholder Tag Convention

Use:

`[PLACEHOLDER: short description - tracked in doc or issue]`

Do not emit empty tags such as:

`[PLACEHOLDER:  - tracked in ]`

## Placeholder Blocker Conditions

A placeholder becomes a blocker when it appears inside:

1. confirmed current feature scope
2. the current branch's expected merge responsibility
3. directly changed files that imply completed user-facing behavior
4. code paths required by the feature's completion standard

## Placeholder Lifecycle Statuses

| Status | Meaning |
|---|---|
| allowed-in-feature | Acceptable on a feature branch for now |
| allowed-in-dev | Temporarily tolerated in integration, but tracked |
| blocked-for-main | Must not reach stable release |
| future-work | Explicitly out of current scope |
| expired-placeholder | Previously tolerated but now overdue |
| untracked-placeholder | Found but not yet classified |

## Branch-Aware Placeholder Rules

| Branch Type | Rule |
|---|---|
| `feature/*` | Allow limited placeholders outside confirmed feature completion claims |
| `dev` / `develop` | Allow only tracked placeholders with clear ownership and low user-facing risk |
| `main` / `master` | Do not allow placeholders that undermine claimed user-facing behavior |
| `prototype/*` / `spike/*` | More tolerance, but no overclaiming |
| `hotfix/*` | Minimal tolerance; real behavior is expected |

## Changelog

| Date | Change | Notes |
|---|---|---|
| YYYY-MM-DD | Initial record | |
