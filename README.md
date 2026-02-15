# ci

Centralized CI configuration and conventions for the endobit organization.

## Reusable Workflows

### Available Workflows

- **go-lint-test.yaml** - Linting and testing for Go projects

### Usage in Other Repos

In your repo's `.github/workflows/ci.yaml`:

```yaml
name: CI
on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main
jobs:
  lint-test:
    uses: endobit/ci/.github/workflows/go-lint-test.yaml@main
```

See `.github/workflows/EXAMPLE.yaml` for complete examples.

## Copilot Instructions

This repo contains centralized Copilot instructions for the organization. When
starting work, tell Copilot:

> Read the conventions at
> https://github.com/endobit/ci/blob/main/COPILOT_INSTRUCTIONS.md and follow
> them.
