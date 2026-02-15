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
  go-ci:
    uses: endobit/ci/.github/workflows/go-lint-test.yaml@v1
    secrets:
      CODECOV_TOKEN: ${{ secrets.CODECOV_TOKEN }}
    # Optional: override defaults
    # with:
    #   go-version: '1.27'
```

### Versioning

Workflows are versioned using Git tags following semantic versioning:

- `@v1` - Floating tag for latest v1.x.x (recommended - gets bug fixes automatically)
- `@v1.0.0` - Pinned to specific version
- `@main` - Latest development version (not recommended for production)

**Breaking changes** increment the major version (v1 → v2).

See `.github/workflows/EXAMPLE.yaml` for complete examples.

## Copilot Instructions

This repo contains centralized Copilot instructions for the organization. When
starting work, tell Copilot:

> Read the conventions at
> https://github.com/endobit/ci/blob/main/COPILOT_INSTRUCTIONS.md and follow
> them.
