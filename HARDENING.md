<!-- markdownlint-disable -->

# Hardening Report: IAreKyleW00t--verified-bot-commit/v2.3.4

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **IAreKyleW00t--verified-bot-commit/v2.3.4** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### missing-permissions (severity: medium)

The workflow file release.yml has no top-level `permissions:` key, and the `tags` job also has no job-level `permissions:` key. Only the `release` job defines its own `permissions: contents: write`. The `tags` job runs with the default (potentially broad) GITHUB_TOKEN permissions, which violates the principle of least privilege.

Locations:

- `.github/workflows/release.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** missing-permissions

**Notes:**

Added top-level `permissions: {}` to release.yml to set a secure default, and added job-level `permissions: {}` to the `tags` job. The `release` job already had `permissions: contents: write`. The `tags` job uses a PAT (secrets.GH_RELEASE_PAT) for git push operations, so it requires no GITHUB_TOKEN permissions.

