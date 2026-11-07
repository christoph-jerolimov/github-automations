# GitHub automations - cross repo workflows

## Sync forks with upstream

[![Sync forks with upstream](https://github.com/christoph-jerolimov/github-automations/actions/workflows/sync-forks.yml/badge.svg)](https://github.com/christoph-jerolimov/github-automations/actions/workflows/sync-forks.yml)

[`.github/workflows/sync-forks.yml`](.github/workflows/sync-forks.yml) fast-forwards the
default branch of a list of forks to the latest upstream commit, like the
**Sync fork** button on GitHub. It runs:

- every Monday morning (05:57 UTC) and Thursday evening (17:57 UTC),
- on every pull request and on every push to `main` (for example when a pull
  request is merged), so the status of the current `main` commit is always
  filled in,
- manually from the Actions tab (`workflow_dispatch`).

Forks are listed in the workflow's `matrix.include`. Each entry has the fork,
its upstream repository and the branch to sync (`main`, or `master` for backstage).

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

- The workflow badge at the top reflects the latest run on the default branch.
- The per-fork badges are [shields.io check-run badges](https://shields.io/badges/git-hub-branch-check-runs)
  filtered by the matrix job name (`<fork> (<branch>)`) on the head of `main`.
  They show `passing`, `failing`, `pending`, or `no check runs` if the workflow
  has not run yet against the current `main` commit.
- Each run also sets a commit status per fork (`fork-sync/<fork>`, for example
  `fork-sync/backstage`) on the commit the workflow ran against: the head of
  `main` for scheduled, push and manual runs, and the pull request's head
  commit for pull request runs. It shows as the check mark or cross next to the
  commit and links to the run.
- Check runs and statuses belong to a commit. Because every push to `main`
  triggers a run, the per-fork badges and statuses of the current `main` commit
  are only briefly empty until that run has finished.

### Setup

The default `GITHUB_TOKEN` can only write to this repository, so the workflow
needs a repository secret named `FORK_SYNC_TOKEN`:

1. Create a [fine-grained personal access token](https://github.com/settings/personal-access-tokens/new)
   with access to the forks listed in the workflow and the permission
   **Contents: Read and write**.
2. Add it under *Settings → Secrets and variables → Actions* as an
   **Actions repository secret** named `FORK_SYNC_TOKEN`.

The sync never force-pushes: if a fork's branch has diverged from upstream the
job for that fork fails and the other forks are still synced.
