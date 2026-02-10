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
  update-project:
    project: "https://github.com/orgs/my-mona-org/projects/1"
  create-project-status-update:
    project: "https://github.com/orgs/my-mona-org/projects/1"
---
# Dependabot Burner Projects

- Find all open Dependabot PRs and add them to the project.
- Create bundle issues, each for exactly **one runtime + one manifest file**.
- Project board status mapping:
  - **Todo**: newly created bundle issues (grouped by runtime+manifest).
  - **In Progress**: bundle issues assigned.
  - **Review Required**: open Dependabot PRs ready for review (tied to a bundle issue).
  - **Done**: bundle issues closed, and their PRs merged/closed.
  - Only move cards when PRs are linked to a bundle issue.
- Post a project status update with PR counts: opened, merged/closed, remaining.
