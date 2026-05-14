# .github

Shared GitHub configuration for the Counterpart organization.

## PR Template

[`pull_request_template.md`](pull_request_template.md) is applied automatically to all new PRs across the org.

## Reusable Workflows

### `validate-pr-template`

Fails CI if the PR description has unfilled placeholders, empty sections, or missing QA evidence.

**Checks:**
- Linear ticket placeholder (`ENG-XXX`) not replaced
- No Type of Change selected
- Manual Testing Steps left empty
- No QA Evidence checked (Loom / trace / screenshots)
- Greptile score not filled in (`___/5`)

**Add to a repo** by creating `.github/workflows/validate-pr.yml`:

```yaml
name: Validate PR

on:
  pull_request:
    types: [review_requested]

jobs:
  validate:
    uses: counterpart-inc/.github/.github/workflows/validate-pr-template.yml@main
```

Then set `validate / Validate PR description` as a required status check in the repo's branch protection rules.

### `release-notes-reusable`

Generates AI-powered release notes from Linear tickets and posts them to Slack. See the workflow file for inputs and required secrets.
