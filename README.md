# GitHub automations - cross repo workflows

## Sync forks with upstream

[![Sync forks with upstream](https://github.com/christoph-jerolimov/github-automations/actions/workflows/sync-forks.yml/badge.svg)](https://github.com/christoph-jerolimov/github-automations/actions/workflows/sync-forks.yml)

[`.github/workflows/sync-forks.yml`](.github/workflows/sync-forks.yml) fast-forwards
the default branches of the forks below to the latest upstream commit, like the
**Sync fork** button on GitHub, so they can be used with
[claude.ai](https://claude.ai) or other cloud AI tools. It never force-pushes,
so a fork that has diverged from upstream fails on its own while the others are
still synced. It runs twice a week.

### Status

| Fork | Upstream | Status |
|---|---|---|
| [backstage](https://github.com/christoph-jerolimov/backstage) | [backstage/backstage](https://github.com/backstage/backstage) | [![backstage](https://img.shields.io/github/check-runs/christoph-jerolimov/github-automations/main?nameFilter=christoph-jerolimov%2Fbackstage%20%28master%29&label=backstage)](https://github.com/christoph-jerolimov/github-automations/actions/workflows/sync-forks.yml) |
| [backstage-community-plugins](https://github.com/christoph-jerolimov/backstage-community-plugins) | [backstage/community-plugins](https://github.com/backstage/community-plugins) | [![backstage-community-plugins](https://img.shields.io/github/check-runs/christoph-jerolimov/github-automations/main?nameFilter=christoph-jerolimov%2Fbackstage-community-plugins%20%28main%29&label=backstage-community-plugins)](https://github.com/christoph-jerolimov/github-automations/actions/workflows/sync-forks.yml) |
| [rhdh](https://github.com/christoph-jerolimov/rhdh) | [redhat-developer/rhdh](https://github.com/redhat-developer/rhdh) | [![rhdh](https://img.shields.io/github/check-runs/christoph-jerolimov/github-automations/main?nameFilter=christoph-jerolimov%2Frhdh%20%28main%29&label=rhdh)](https://github.com/christoph-jerolimov/github-automations/actions/workflows/sync-forks.yml) |
| [rhdh-plugins](https://github.com/christoph-jerolimov/rhdh-plugins) | [redhat-developer/rhdh-plugins](https://github.com/redhat-developer/rhdh-plugins) | [![rhdh-plugins](https://img.shields.io/github/check-runs/christoph-jerolimov/github-automations/main?nameFilter=christoph-jerolimov%2Frhdh-plugins%20%28main%29&label=rhdh-plugins)](https://github.com/christoph-jerolimov/github-automations/actions/workflows/sync-forks.yml) |
| [rhdh-skills](https://github.com/christoph-jerolimov/rhdh-skills) | [redhat-developer/rhdh-skills](https://github.com/redhat-developer/rhdh-skills) | [![rhdh-skills](https://img.shields.io/github/check-runs/christoph-jerolimov/github-automations/main?nameFilter=christoph-jerolimov%2Frhdh-skills%20%28main%29&label=rhdh-skills)](https://github.com/christoph-jerolimov/github-automations/actions/workflows/sync-forks.yml) |
| [rhdh-plugin-export-overlays](https://github.com/christoph-jerolimov/rhdh-plugin-export-overlays) | [redhat-developer/rhdh-plugin-export-overlays](https://github.com/redhat-developer/rhdh-plugin-export-overlays) | [![rhdh-plugin-export-overlays](https://img.shields.io/github/check-runs/christoph-jerolimov/github-automations/main?nameFilter=christoph-jerolimov%2Frhdh-plugin-export-overlays%20%28main%29&label=rhdh-plugin-export-overlays)](https://github.com/christoph-jerolimov/github-automations/actions/workflows/sync-forks.yml) |
| [rhdh-loadtest](https://github.com/christoph-jerolimov/rhdh-loadtest) | [redhat-developer/rhdh-loadtest](https://github.com/redhat-developer/rhdh-loadtest) | [![rhdh-loadtest](https://img.shields.io/github/check-runs/christoph-jerolimov/github-automations/main?nameFilter=christoph-jerolimov%2Frhdh-loadtest%20%28main%29&label=rhdh-loadtest)](https://github.com/christoph-jerolimov/github-automations/actions/workflows/sync-forks.yml) |
| [rhdh-local](https://github.com/christoph-jerolimov/rhdh-local) | [redhat-developer/rhdh-local](https://github.com/redhat-developer/rhdh-local) | [![rhdh-local](https://img.shields.io/github/check-runs/christoph-jerolimov/github-automations/main?nameFilter=christoph-jerolimov%2Frhdh-local%20%28main%29&label=rhdh-local)](https://github.com/christoph-jerolimov/github-automations/actions/workflows/sync-forks.yml) |
| [rhdh-e2e-test-utils](https://github.com/christoph-jerolimov/rhdh-e2e-test-utils) | [redhat-developer/rhdh-e2e-test-utils](https://github.com/redhat-developer/rhdh-e2e-test-utils) | [![rhdh-e2e-test-utils](https://img.shields.io/github/check-runs/christoph-jerolimov/github-automations/main?nameFilter=christoph-jerolimov%2Frhdh-e2e-test-utils%20%28main%29&label=rhdh-e2e-test-utils)](https://github.com/christoph-jerolimov/github-automations/actions/workflows/sync-forks.yml) |

### Setup

The default `GITHUB_TOKEN` can only write to this repository, so the workflow
needs a repository secret named `FORK_SYNC_TOKEN`:

1. Create a [fine-grained personal access token](https://github.com/settings/personal-access-tokens/new)
   with access to the forks listed in the workflow and the permission
   **Contents: Read and write**.
2. Add it under *Settings → Secrets and variables → Actions* as an
   **Actions repository secret** named `FORK_SYNC_TOKEN`.
