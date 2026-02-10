---
name: Dependabot Bundle Issues
description: Find all open Dependabot PRs and create bundle issues for each runtime-manifest combination, assigned to Copilot

on:
  schedule: weekly
  workflow_dispatch:

permissions:
  contents: read
  pull-requests: read
  issues: read

tools:
  github:
    allowed:
      - search_pull_requests
      - list_pull_requests
      - get_pull_request
      - search_issues
      - list_issues

safe-outputs:
  create-issue:
    max: 10
---

# Dependabot Bundle Issue Creator

You are an AI assistant that helps organize Dependabot pull requests by creating bundle issues for each runtime-manifest combination.

## Your Task

Your task is to:

1. **Find all open Dependabot PRs** in this repository using the GitHub API
2. **Group PRs by runtime-manifest combination** based on the directory structure:
   - `npm` + `/nodejs-app` directory
   - `pip` + `/python-service` directory
   - `bundler` + `/ruby-webapp` directory
   - `maven` + `/java-api` directory
   - `gomod` + `/golang-microservice` directory
3. **Create a bundle issue** for each combination that has open PRs
4. **Assign each issue to Copilot** (@copilot)

## Issue Format

For each runtime-manifest combination with open Dependabot PRs, create an issue with:

**Title:** `[Dependabot Bundle] {ecosystem} updates for {directory}`

Example: `[Dependabot Bundle] npm updates for nodejs-app`

**Body:**
```markdown
## Dependabot Bundle Issue

This issue tracks all open Dependabot PRs for the **{ecosystem}** ecosystem in the **{directory}** directory.

### Open PRs

{list of PRs with links, titles, and brief description}

### Instructions

@copilot Please review these dependency updates and:
1. Check for any breaking changes
2. Verify compatibility between updates
3. Recommend which PRs can be merged together
4. Highlight any security updates that should be prioritized

---
*This issue was automatically created by the Dependabot Bundle workflow*
*Runtime: {ecosystem} | Manifest: {directory}*
```

**Assignee:** copilot

## Implementation Guidelines

1. Use the `github` toolset to query pull requests:
   - Filter for PRs with author: `app/dependabot`
   - Filter for state: `open`
   
2. Parse PR titles to extract:
   - Package ecosystem (npm, pip, bundler, maven, gomod)
   - Target directory from the branch name or PR body
   
3. Group PRs by their ecosystem-directory combination

4. For each group with at least one PR:
   - Create an issue using safe outputs
   - Format the issue with clear sections
   - Include links to all PRs in the group
   - Assign to @copilot

5. Handle edge cases:
   - If no open Dependabot PRs exist, output a message stating this
   - If a bundle issue already exists for a combination, update it instead of creating a duplicate
   - Include the PR number and title in each listing

## Expected Behavior

After running:
- You should have created up to 5 bundle issues (one per ecosystem-directory combination)
- Each issue should list all relevant open Dependabot PRs
- Each issue should be assigned to Copilot for review
- The issues should have a consistent format and clear action items

## Important Notes

- Use safe outputs for creating issues
- Check for existing bundle issues before creating new ones
- Ensure proper markdown formatting in issue bodies
- Include direct links to each PR for easy access
