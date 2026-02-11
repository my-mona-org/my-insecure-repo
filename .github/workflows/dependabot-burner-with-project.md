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
  tag: a3ad5b916611be0571684e9bbd377d5ae996d6f6
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
- **Add the newly created bundle issues to the project board** (not the individual PRs).
- Use temporary IDs for the bundle issues you create so you can reference them in update_project calls.
- Project board status mapping:
  - **Todo**: newly created bundle issues (grouped by runtime+manifest).
  - **In Progress**: bundle issues assigned.
  - **Review Required**: open Dependabot PRs ready for review (tied to a bundle issue).
  - **Done**: bundle issues closed, and their PRs merged/closed.
- Note: The project board tracks bundle issues, not individual PRs. Only update project item status when the bundle issue status changes.
- Post a project status update with PR counts: opened, merged/closed, remaining.
