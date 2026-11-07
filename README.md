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

- The badge above reflects the latest run on the default branch.
- Each run also sets a commit status per fork (`fork-sync/<fork>`, for example
  `fork-sync/backstage`) on the commit the workflow ran against, normally the
  head of `main`. It shows as the check mark or cross next to the latest commit
  and links to the run. A status belongs to a commit, so after a new push to
  `main` it is empty until the next run.

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
