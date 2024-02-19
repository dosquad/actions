# actions

GitHub Reusable Actions

## Usage

## Unit Testing

```yaml
name: CI

on:
  push:
  pull_request:
  workflow_dispatch:

jobs:
  unit-test:
    name: "Unit Test"
    uses: dosquad/actions/.github/workflows/unit-test.yml@main
    secrets: inherit
```

### Docker Release

```yaml
name: "Docker Release"

on:
  pull_request:
  push:
    branches:
      - main

jobs:
  docker:
    name: "Docker"
    uses: dosquad/actions/.github/workflows/docker-release.yml@main
    with:
      image: ghcr.io/dosquad/database-operator
      platforms: 'linux/amd64,linux/arm64'
      latest-on-branch: '{{is_default_branch}}'
    secrets: inherit

```

### Docker PR Cleanup

```yaml
name: Cleanup on Closed Pull Request

on:
  pull_request:
    types: 
      - closed

jobs:
  docker:
    name: "Docker Cleanup"
    uses: dosquad/actions/.github/workflows/docker-pr-cleanup.yml@main
    with:
      package-name: database-operator
      owner: "${{github.repository_owner}}"
      pull-request-merged: "${{github.event.inputs.pull-request-merged}}"
      pull-request-number: "${{github.event.pull_request.number}}"
    secrets: inherit
```
