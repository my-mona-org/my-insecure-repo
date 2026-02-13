---
on: weekly
permissions:
  contents: read
  issues: read
  pull-requests: read
tools:
  github:
    toolsets: [default, projects]
features:
  action-tag: ec99734fbadefe28647f8a53c3ec638a63324e53
safe-outputs:
  create-issue:
    title-prefix: '[dependabot-burner] '
    max: 10
  update-project:
    project: "https://github.com/orgs/my-mona-org/projects/1"
  create-project-status-update:
    project: "https://github.com/orgs/my-mona-org/projects/1"
---
# Dependabot Burner Projects

- Find all open Dependabot PRs.
- Create bundle issues, each for exactly **one runtime + one manifest file**.
- Link PRs to their bundle issue.
- Resolve temporary idsof the newly created bundle issues and add them to the project board.
- Post a status update with PR counts: opened, merged/closed, remaining.

## Project board statuses:

- Todo – New, unassigned bundle issues.
- In Progress – Assigned bundle issues.
- Review Required – Bundle issues that require human action (at least one linked PR is ready, blocked, or needs a decision).
- Done – Closed bundle issues with all linked PRs merged or closed.
