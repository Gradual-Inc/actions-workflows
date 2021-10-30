# Collection of reusable Github actions

## Prepare Release

* Bump release version
* Generate release note

### Setup

copy `.github/release-note-configuration.json` to your repo `.github/release-note-configuration.json`

```yaml
name: Prepare Release
on:
  workflow_dispatch:
    inputs:
      previous_tag:
        description: 'Previous Tag used to generate change log'
        required: false
      target_branch:
        description: 'Target branch use for release, default development'
        required: false
        default: 'development'
jobs:
  prepare_release:
    uses: gradual-inc/actions-workflows/.github/workflows/prepare-release.yml@main
    secrets:
      token: ${{ secrets.PAT_CODE_PUSH }}
    with:
      previous_tag: ${{ github.event.inputs.previous_tag}}
      target_branch: ${{ github.event.inputs.target_branch }}
      deploy_workflow_name: 'Deploy EKS'
```


## PR Updator

* Extract Shotcut number and put it in front of PR title
* Add label to PR according to branch name

### Setup

```yaml
name: PR Updator
on:
  pull_request:
    types: [opened]
jobs:
  pr-updator:
    uses: gradual-inc/actions-workflows/.github/workflows/pr-updator.yml@main
    secrets:
      token: ${{ secrets.GITHUB_TOKEN }}
```

