---
name: Dependabot Burner
description: Bundle open Dependabot PRs by ecosystem and create issues for review

on:
  schedule: weekly
  workflow_dispatch:

permissions:
  contents: read
  pull-requests: read

tools:
  github:
    allowed: [search_pull_requests]

safe-outputs:
  create-issue:
    title-prefix: '[dependabot-burner] '
    assignees: ['copilot']
    max: 10
---

# Dependabot Burner

- Find all open Dependabot PRs and add them to the project.
- Create bundle issues, each for exactly **one runtime + one manifest file**.
- Assign each bundle issue to Copilot.
