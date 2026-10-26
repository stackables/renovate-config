# renovate-config

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>stackables/renovate-config"]
}
```

## What it does

- **One weekly PR** for all minor and patch updates, Mondays 10–17 Europe/Berlin, office hours, when the self-hosted CI runners are up.
- **Lock file maintenance** in the same window: one PR that refreshes the lockfile, so transitive dependencies (where most security alerts sit) move to the newest version their parents allow. Renovate cannot age a lock file refresh (pnpm picks the versions), so its own 7-day check is off for it (`minimumReleaseAge: null`): every pnpm repository sets `minimumReleaseAge: 10080` in `pnpm-workspace.yaml` instead, and pnpm keeps out anything younger. Without this the check never passes and lock file PRs never merge.
- **7-day release age** for every update.
- **Majors wait for approval** on each repository's Dependency Dashboard.
- **Security fixes** (`[SECURITY]` PRs) skip the schedule, the release age and the approval. Renovate finds them through GitHub's vulnerability alerts, so keep those on.
- **Auto-merge, where a repository turns it on, is Renovate's own merge** (`platformAutomerge: false`): it merges once every check on the PR has passed, the 7-day check included. GitHub's auto-merge waits only for the checks branch protection requires, and a private repository on this plan can require none, so it could merge a PR whose tests failed.
- **pnpm overrides with a version selector** (`undici@>=7.0.0 <7.24.0`) are left alone: they are security floors for one version line.

This repository is public because Renovate's hosted app reads a preset across organisations only from a public repository.
