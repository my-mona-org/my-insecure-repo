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
  action-tag: a261dd75678900737175cdd920f8022023aeb444
safe-outputs:
  create-issue:
    title-prefix: '[dependabot-burner] '
    max: 10
  update-project:
    project: "https://github.com/orgs/my-mona-org/projects/1"
    max: 50
  create-project-status-update:
    project: "https://github.com/orgs/my-mona-org/projects/1"
    max: 1
---
# Dependabot Burner (with Projects)

- Find all open Dependabot PRs and all them to the project board under "Todo".
- Create bundle issues, each for exactly **one runtime + one manifest file**.
- Add them to the project board under "Review Required".
- Post a project status update with PR counts: opened, merged/closed, remaining.
