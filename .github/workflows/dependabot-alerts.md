---
on: workflow_dispatch
permissions:
  contents: read
  issues: read
  pull-requests: read
  security-events: read
tools:
  github:
    toolsets: [dependabot]
safe-outputs:
  create-issue:
    title-prefix: '[dependabot-alerts] '
    max: 5
---
# Dependabot Alerts Reader

- Read all open Dependabot security alerts for this repository (do not use info from depedabot PRs, but read alerts directly).
- Summarize the alerts by severity (critical, high, medium, low), including the affected package, ecosystem, and CVE/GHSA identifier where available.
- Create an issue with the summary report, listing the total count per severity level and a brief description of each alert.
