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
  add-comment:
    max: 50
  update-project:
    project: "https://github.com/orgs/my-mona-org/projects/1"
  create-project-status-update:
    project: "https://github.com/orgs/my-mona-org/projects/1"
---
# Dependabot Burner Projects (Agent-Driven Grouping)

This workflow decides how to group Dependabot PRs into bundle issues using
reasoning beyond fixed rules. Input data is provided by the regular GitHub
Actions workflow `dependabot-burner.yml`.

## Tasks

- Find the most recently updated issue titled `[dependabot-burner] Input` with
  the label `dependabot-burner-input`.
- Extract the JSON block under **Input Data**.
- Decide bundle groupings using the PR metadata and file lists. Prefer grouping
  by runtime and manifest, but split if risk or scope differs.
- For each bundle:
  - Use the title format `[dependabot-burner] <runtime> | <manifest or bundle name>`.
  - Create the bundle issue if it does not exist, and include the PR list and
    a short rationale for grouping.
  - Add a comment to each PR linking back to its bundle issue (avoid duplicates).
  - Add the bundle issue to the project and set status (see statuses below).
- Post a status update that includes:
  - Open PRs remaining (open total)
  - Opened in the last 7 days
  - Merged/closed in the last 7 days
  - Unclassified PRs (if any)
- If the input issue is missing or the JSON is malformed, exit without writing.

## Grouping guidance

- Prefer single runtime + manifest groupings when the PR touches one clear
  dependency set.
- If a PR touches multiple manifests or runtimes, choose the dominant manifest
  based on scope/impact and note the reasoning in the bundle issue.
- Split bundles if the PRs differ materially in risk, surface area, or owner.

## Project board statuses

- Todo – New, unassigned bundle issues.
- In Progress – Assigned bundle issues.
- Review Required – Bundle issues that require human action (at least one linked PR is ready, blocked, or needs a decision).
- Done – Closed bundle issues with all linked PRs merged or closed.
