---
on: weekly
permissions:
  contents: read
  issues: read
  pull-requests: read
tools:
  github:
    toolsets: [default, projects]
safe-outputs:
  create-issue:
    title-prefix: '[dependabot-burner] '
    max: 10
---
# Dependabot Burner

- Add all open Dependabot PRs.
- Create bundle issues grouped by runtime + manifest (max 5 PRs each, security separate, no duplicates); explain the grouping briefly and list PRs in merge order (patch/minor → major).
