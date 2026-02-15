# endobit/ci

Centralized CI configuration and conventions for the endobit organization.

## Using Reusable Workflows

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
    uses: endobit/ci/.github/workflows/go-lint-test.yaml@main
    secrets:
      CODECOV_TOKEN: ${{ secrets.CODECOV_TOKEN }}
    # Optional: override defaults
    # with:
    #   go-version: '1.27'
```

See `.github/workflows/EXAMPLE.yaml` for complete examples.

## Copilot Instructions

This repo contains centralized Copilot instructions for the organization.

### Using in Other Repos

**Option 1: Copy the file**
```bash
curl -o .github/copilot-instructions.md https://raw.githubusercontent.com/endobit/ci/main/COPILOT_INSTRUCTIONS.md
```

**Option 2: Reference in your repo's instructions**

Create `.github/copilot-instructions.md` in your repo:

```markdown
# Copilot Instructions for [your-repo]

> **Note:** This repo follows org-wide conventions in [endobit/ci/COPILOT_INSTRUCTIONS.md](https://github.com/endobit/ci/blob/main/COPILOT_INSTRUCTIONS.md)

## Repository-Specific Instructions

[Add your repo-specific instructions here]
```

**Option 3: Seed a Copilot session**

When starting work, tell Copilot:

> Read the conventions at https://github.com/endobit/ci/blob/main/COPILOT_INSTRUCTIONS.md and follow them.

## Contributing

Follow conventions in `COPILOT_INSTRUCTIONS.md`, particularly:
- Use conventional commits
- Test workflows before committing
- Keep workflows focused and reusable
