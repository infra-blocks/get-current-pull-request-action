# composite-action-template
[![Release](https://github.com/infrastructure-blocks/composite-action-template/actions/workflows/git-tag-semver-from-label.yml/badge.svg)](https://github.com/infrastructure-blocks/composite-action-template/actions/workflows/git-tag-semver-from-label.yml)
[![Self Test](https://github.com/infrastructure-blocks/composite-action-template/actions/workflows/self-test.yml/badge.svg)](https://github.com/infrastructure-blocks/composite-action-template/actions/workflows/self-test.yml)
[![Update From Template](https://github.com/infrastructure-blocks/get-current-pull-request-action/actions/workflows/update-from-template.yml/badge.svg)](https://github.com/infrastructure-blocks/get-current-pull-request-action/actions/workflows/update-from-template.yml)

This GitHub Action gets the current pull request from the context. It returns the `${{ github.event.pull_request }}` field
when it is defined. Otherwise, it uses the [GitHub API](https://docs.github.com/en/rest/commits/commits?apiVersion=2022-11-28#list-pull-requests-associated-with-a-commit)
to list the pull requests associated with `${{ github.sha }}`. In the event that more than one pull request is returned,
this action will return the one that was updated most recently.

## Inputs

|     Name      | Required | Description       |
|:-------------:|:--------:|-------------------|
| example-input |   true   | An example input. |

## Outputs

|      Name      | Description        |
|:--------------:|--------------------|
| example-output | An example output. |

## Permissions

|     Scope     | Level | Reason   |
|:-------------:|:-----:|----------|
| pull-requests | read  | Because. |

## Usage

```yaml
name: Template Usage

on:
  push: ~

# The required permissions.
permissions:
  pull-requests: read

# The suggested concurrency controls.
concurrency:
  group: ${{ github.workflow }}-${{ github.ref }}
  cancel-in-progress: true

jobs:
  example-job:
    runs-on: ubuntu-22.04
    steps:
      - uses: infrastructure-blocks/composite-action-template@v1
```

## Development

### Releasing

The releasing is handled at git level with semantic versioning tags. Those are automatically generated and managed
by the [git-tag-semver-from-label-workflow](https://github.com/infrastructure-blocks/git-tag-semver-from-label-workflow).
