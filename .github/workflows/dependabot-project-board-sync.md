---
on:
  workflow_run:
    workflows:
      - Dependabot Burner
    types:
      - completed
    branches:
      - main
  issues:
    types:
      - assigned
      - unassigned
  pull_request:
    types:
      - review_requested
permissions:
  contents: read
  issues: read
  pull-requests: read
tools:
  github:
    toolsets: [default, projects]
safe-outputs:
  update-project:
    project: "https://github.com/orgs/my-mona-org/projects/1"
  create-project-status-update:
    project: "https://github.com/orgs/my-mona-org/projects/1"
---
# Dependabot Project Board Sync

- **Always**:
  - **Bundle issue** = open issue with title starting "Bundle:" and label "dependencies".
  - Ensure bundle is on project; if missing, add with **Status "Todo"** (do not override existing **Status**).
  - Post **status update**: bundle count, Dependabot PR counts, short table (runtime, manifest, PR count).
- **workflow_run**:
  - Only proceed when Dependabot Burner succeeded; else noop.
  - Prefer bundles created between started_at and completed_at; fallback to all open bundles.
- **issues** (assigned/unassigned):
  - Only act on bundle issues; else noop.
  - assigned => **Status "In Progress"** unless already **"Review Required"** or **"Done"**.
  - unassigned => **Status "Todo"** only if current Status is **"In Progress"**.
- **pull_request** (review_requested):
  - Only act on PRs linked to an open bundle issue; else noop.
  - Set linked bundle **Status "Review Required"** unless already **"Done"**.
