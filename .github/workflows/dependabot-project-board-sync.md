---
on:
  workflow_run:
    workflows:
      - Dependabot Burner
    types:
      - completed
    branches:
      - main
      - master
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

- Run only when the Dependabot Burner workflow completed successfully; otherwise write a noop message.
- Find open bundle issues created by the Dependabot Burner workflow:
  - Title starts with "Bundle:" and label is "dependencies".
  - Prefer issues created in the workflow_run time window (started_at to completed_at).
  - If none are found in the time window, fall back to all open bundle issues.
- Add each bundle issue to the project board with Status "Todo" if the item is missing; do not override an existing Status.
- Post a project status update summarizing bundle count and Dependabot PR counts (open, merged/closed, remaining). Include a short table listing runtime, manifest, and PR count per bundle issue.
