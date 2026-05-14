# counterpart-inc/.github

Organization-level shared GitHub configuration for all Counterpart repos.

## Reusable Workflows

### `.github/workflows/release-automation.yml`

Consolidated post-deploy release automation. Called by consumer repos after a successful deploy.

**What it does (in order):**
1. **Linear release sync** — scans commits for Linear ticket IDs (e.g. `TEC-1234`) and creates a Linear release, moving linked issues to Done. Uses `linear/linear-release-action` in continuous pipeline mode.
2. **Sentry release** — creates a Sentry release tagged with the version and environment. Conditional on `sentry_projects` input.
3. **AI release notes** — generates release notes from Linear tickets and posts to Slack. Conditional on `release_url` input (production deploys only).

All steps use `continue-on-error: true` so notifications never block deploys.

**Inputs:**
- `version` (required) — git tag for production, SHA for QA
- `environment` (required) — `production`, `qa`, etc.
- `release_url` (optional) — GitHub release URL; triggers AI release notes + Slack
- `sentry_projects` (optional) — space-separated Sentry project slugs; triggers Sentry release
- `slack_channel` (optional) — Slack channel for AI release notes, defaults to `#engineering-releases`

**Required secrets:** `LINEAR_API_KEY`. Optional: `SENTRY_AUTH_TOKEN`, `SENTRY_ORG`, `CLAUDE_LINEAR_AI_RELEASE_NOTES_API_KEY`, `SLACK_AI_RELEASE_NOTES_TOKEN`.

**Example usage (production):**
```yaml
release-automation:
  needs: deploy
  uses: counterpart-inc/.github/.github/workflows/release-automation.yml@main
  with:
    version: ${{ needs.deploy.outputs.version }}
    environment: production
    release_url: ${{ github.event.release.html_url }}
    sentry_projects: "backend-project frontend-project"
  secrets:
    LINEAR_API_KEY: ${{ secrets.LINEAR_API_KEY }}
    SENTRY_AUTH_TOKEN: ${{ secrets.SENTRY_AUTH_TOKEN }}
    SENTRY_ORG: ${{ secrets.SENTRY_ORG }}
    CLAUDE_LINEAR_AI_RELEASE_NOTES_API_KEY: ${{ secrets.CLAUDE_LINEAR_AI_RELEASE_NOTES_API_KEY }}
    SLACK_AI_RELEASE_NOTES_TOKEN: ${{ secrets.SLACK_AI_RELEASE_NOTES_TOKEN }}
```

**Example usage (QA — no release notes):**
```yaml
release-automation:
  needs: deploy
  if: github.ref == 'refs/heads/main'
  uses: counterpart-inc/.github/.github/workflows/release-automation.yml@main
  with:
    version: ${{ needs.deploy.outputs.version }}
    environment: qa
  secrets:
    LINEAR_API_KEY: ${{ secrets.LINEAR_API_KEY }}
```
