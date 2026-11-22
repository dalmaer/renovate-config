# renovate-config

Shared Renovate preset with four lanes (at most one open PR per lane) and a 3-day release cooldown:

- **`renovate/patch-minor` (daily, automerge):** all patch, minor, digest, and pin updates grouped into one PR; merges itself once CI checks pass.
- **`renovate/lock-file-maintenance` (Mondays, automerge):** weekly lockfile refresh.
- **`renovate/major-weekly` (Mondays, human review):** all major updates and git submodules together.
- **`renovate/node` (Mondays, human review):** `.nvmrc`, `Dockerfile` `FROM node:`, and `@types/node` in one PR (leaving `engines.node` `>=` floors untouched).

## Usage

Add a 4-line `renovate.json` to any repository:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>dalmaer/renovate-config"]
}
```

### Optional per-repo overrides

Set a local timezone (defaults to UTC) or ignore internal workspace packages in monorepos:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>dalmaer/renovate-config"],
  "timezone": "America/Denver",
  "packageRules": [
    {
      "matchPackageNames": ["@my-scope/**"],
      "enabled": false
    }
  ]
}
```
