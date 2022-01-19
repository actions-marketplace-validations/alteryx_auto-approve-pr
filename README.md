# GitHub Action - Auto Approve Pull Request

A GitHub Action to auto approve, and merge pull requests.

## Usage

This GitHub Action provides a task to find a pull request, approve it if, and merge in the pull request

```yaml
steps:
  - name: Run Auto Approve Action
    id: auto-approve-pr
    uses: alteryx/auto-approve-pr@v1
    with:
      repository: ${{ github.repository }}
      assignee: "machineFL"
      github-token: ${{ secrets.AUTO_APPROVE_TOKEN }}
```
## Example

```yaml
# auto_approve_dependency_PRs.yml
name: Auto Approve Dependency PRs
on:
  workflow_dispatch:
  workflow_run:
    workflows: ["Tests"]
    branches:    
      - 'latest-dep-update-[a-f0-9]+'
      - 'min-dep-update-[a-f0-9]+'
    types:
      - completed
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Run Auto Approve Action
        id: auto-approve-pr
        uses: alteryx/auto-approve-pr@v1
        with:
          repository: ${{ github.repository }}
          assignee: "machineFL"
          github-token: ${{ secrets.AUTO_APPROVE_TOKEN }}
```

To install this workflow, add the file above to the following location in your repository.

```
.github
└── workflows
    └── auto_approve_dependency_PRs.yml
```
