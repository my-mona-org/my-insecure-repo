---
name: Dependabot Burner (with Projects)
description: Bundle open Dependabot PRs by ecosystem and create review issues, using a GitHub project board to track and visualize progress.

on:
  schedule: weekly
  workflow_dispatch:

permissions:
  contents: read
  issues: read
  pull-requests: read

tools:
  github:
    allowed: [search_pull_requests]
    toolsets: [default, projects]

safe-outputs:
  github-token: ${{ secrets.AGENT_GITHUB_TOKEN }}
  create-issue:
    title-prefix: '[dependabot-burner] '
    assignees: ['copilot']
    max: 10
  update-project:
    github-token: ${{ secrets.PROJECT_GITHUB_TOKEN }}
    project: "https://github.com/orgs/my-mona-org/projects/1"
    max: 50

---

# Dependabot Burner

- Find all open Dependabot PRs and add them to the project.
- Create bundle issues, each for exactly **one runtime + one manifest file**.
- Assign each bundle issue to Copilot.
- Project board status mapping:
  - Todo: newly created bundle issues (grouped by runtime+manifest).
  - In Progress: bundle issues actively worked.
  - Review Required: open Dependabot PRs ready for review (tied to a bundle issue).
  - Done: bundle issues closed, and their PRs merged/closed.
  - Only move cards when PRs are linked to a bundle issue.
