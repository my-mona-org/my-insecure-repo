---
on: weekly
permissions:
  contents: read
  issues: read
  pull-requests: read
tools:
  github:
safe-outputs:
  create-issue:
    title-prefix: '[dependabot-burner] '
    max: 10
---
# Dependabot Burner

- Find all open Dependabot PRs and add them to the project.
- Create bundle issues, each for exactly **one runtime + one manifest file**.
