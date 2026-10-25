# renovate-config

The Renovate config every repository in `stackables`, `stackables-cloud` and `youropinion-is` extends. Change the shared behaviour here, once; a repository's own `renovate.json` keeps only what is specific to it.

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>stackables/renovate-config"]
}
```

## What it does

- **One weekly PR** for all minor and patch updates, Mondays 10–17 Europe/Berlin, office hours, when the self-hosted CI runners are up.
- **Lock file maintenance** in the same window: one PR that refreshes the lockfile, so transitive dependencies (where most security alerts sit) move to the newest version their parents allow. Renovate's release age does not apply to it, so pnpm repositories set `minimumReleaseAge: 10080` in `pnpm-workspace.yaml` as well.
- **7-day release age** for every update.
- **Majors wait for approval** on each repository's Dependency Dashboard.
- **Security fixes** (`[SECURITY]` PRs) skip the schedule, the release age and the approval. Renovate finds them through GitHub's vulnerability alerts, so keep those on.
- **pnpm overrides with a version selector** (`undici@>=7.0.0 <7.24.0`) are left alone: they are security floors for one version line.

This repository is public because Renovate's hosted app reads a preset across organisations only from a public repository.

## Where to look

- [Open Renovate PRs](https://github.com/pulls?q=is%3Apr+is%3Aopen+author%3Aapp%2Frenovate+archived%3Afalse+%28org%3Astackables+OR+org%3Astackables-cloud+OR+org%3Ayouropinion-is%29)
- [Dependency Dashboards](https://github.com/issues?q=is%3Aissue+is%3Aopen+author%3Aapp%2Frenovate+archived%3Afalse+in%3Atitle+%22Dependency+Dashboard%22+%28org%3Astackables+OR+org%3Astackables-cloud+OR+org%3Ayouropinion-is%29), where majors wait
