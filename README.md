# github-automations

## Sync forks with upstream

[![Sync forks with upstream](https://github.com/christoph-jerolimov/github-automations/actions/workflows/sync-forks.yml/badge.svg)](https://github.com/christoph-jerolimov/github-automations/actions/workflows/sync-forks.yml)

[`.github/workflows/sync-forks.yml`](.github/workflows/sync-forks.yml) fast-forwards the
default branch of a list of forks to the latest upstream commit, like the
**Sync fork** button on GitHub. It runs every Monday morning (05:57 UTC) and
Thursday evening (17:57 UTC), and can also be started manually from the Actions
tab (`workflow_dispatch`).

Forks are listed in the workflow's `matrix.include`. Each entry has the fork,
its upstream repository and the branch to sync (`main`, or `master` for backstage).

### Status

| Fork | Branch | Status |
|---|---|---|
| [backstage](https://github.com/christoph-jerolimov/backstage) | `master` | [![backstage](https://img.shields.io/github/check-runs/christoph-jerolimov/github-automations/main?nameFilter=christoph-jerolimov%2Fbackstage%20(master)&label=backstage)](https://github.com/christoph-jerolimov/github-automations/actions/workflows/sync-forks.yml) |
| [backstage-community-plugins](https://github.com/christoph-jerolimov/backstage-community-plugins) | `main` | [![backstage-community-plugins](https://img.shields.io/github/check-runs/christoph-jerolimov/github-automations/main?nameFilter=christoph-jerolimov%2Fbackstage-community-plugins%20(main)&label=backstage-community-plugins)](https://github.com/christoph-jerolimov/github-automations/actions/workflows/sync-forks.yml) |
| [rhdh](https://github.com/christoph-jerolimov/rhdh) | `main` | [![rhdh](https://img.shields.io/github/check-runs/christoph-jerolimov/github-automations/main?nameFilter=christoph-jerolimov%2Frhdh%20(main)&label=rhdh)](https://github.com/christoph-jerolimov/github-automations/actions/workflows/sync-forks.yml) |
| [rhdh-plugins](https://github.com/christoph-jerolimov/rhdh-plugins) | `main` | [![rhdh-plugins](https://img.shields.io/github/check-runs/christoph-jerolimov/github-automations/main?nameFilter=christoph-jerolimov%2Frhdh-plugins%20(main)&label=rhdh-plugins)](https://github.com/christoph-jerolimov/github-automations/actions/workflows/sync-forks.yml) |

- The workflow badge at the top reflects the latest run on the default branch.
- The per-fork badges are [shields.io check-run badges](https://shields.io/badges/git-hub-branch-check-runs)
  filtered by the matrix job name (`<fork> (<branch>)`) on the head of `main`.
  They show `passing`, `failing`, `pending`, or `no check runs` if the workflow
  has not run yet against the current `main` commit.
- Each run also sets a commit status per fork (`fork-sync/<fork>`, for example
  `fork-sync/backstage`) on the commit the workflow ran against, normally the
  head of `main`. It shows as the check mark or cross next to the latest commit
  and links to the run.
- Check runs and statuses belong to a commit, so after a new push to `main` the
  per-fork badges and statuses are empty until the next run.

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
