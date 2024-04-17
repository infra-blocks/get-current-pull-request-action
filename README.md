# get-current-pull-request-action
[![Release](https://github.com/infrastructure-blocks/composite-action-template/actions/workflows/git-tag-semver-from-label.yml/badge.svg)](https://github.com/infrastructure-blocks/composite-action-template/actions/workflows/git-tag-semver-from-label.yml)
[![Self Test](https://github.com/infrastructure-blocks/composite-action-template/actions/workflows/self-test.yml/badge.svg)](https://github.com/infrastructure-blocks/composite-action-template/actions/workflows/self-test.yml)
[![Update From Template](https://github.com/infrastructure-blocks/get-current-pull-request-action/actions/workflows/update-from-template.yml/badge.svg)](https://github.com/infrastructure-blocks/get-current-pull-request-action/actions/workflows/update-from-template.yml)

This GitHub Action gets the current pull request from the context. It returns the `${{ github.event.pull_request }}`
field when it is defined. Otherwise, it uses the [GitHub API](https://docs.github.com/en/rest/commits/commits?apiVersion=2022-11-28#list-pull-requests-associated-with-a-commit)
to list the pull requests associated with `${{ github.sha }}`. In the event that more than one pull request is returned,
this action will return the one that was updated most recently.

If no pull request could be found matching the commit, then this action fails.

## Inputs

N/A

## Outputs

|  Name  | Description                           |
|:------:|---------------------------------------|
|   id   | The pull request ID.                  |
|  json  | The JSON payload of the pull request. |
| number | The pull request number.              |
|  url   | The pull request URL.                 |

## Permissions

|     Scope     | Level | Reason                                       |
|:-------------:|:-----:|----------------------------------------------|
| pull-requests | read  | To list the pull requests matching a commit. |

## Usage

```yaml
name: My Workflow

on:
  push: ~

permissions:
  pull-requests: read

jobs:
  my-job:
    runs-on: ubuntu-22.04
    steps:
      - id: current-pr
        uses: infrastructure-blocks/get-current-pull-request-action@v1
      - run: |
          echo "Hello from PR #${{ steps.current-pr.outputs.number }}"
```
