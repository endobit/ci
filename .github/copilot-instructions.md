# Copilot Instructions for endobit/ci

> **Note:** This repo follows org-wide conventions documented in `/COPILOT_INSTRUCTIONS.md`

## Repository Purpose

This is a **centralized CI configuration library** for the endobit GitHub organization. It contains reusable GitHub Actions workflows that other repositories can consume.

## Architecture

### Reusable Workflows Pattern

All workflows in `.github/workflows/` use `workflow_call` triggers **only** - they never run for this repository itself. This is intentional:

- Workflows must live at `.github/workflows/` (GitHub requirement for reusable workflows)
- The `workflow_call` trigger makes them callable from other repos
- No `push` or `pull_request` triggers should be added to these workflows

### Consuming Workflows

Other repos in the endobit org reference workflows like:

```yaml
jobs:
  ci:
    uses: endobit/ci/.github/workflows/<workflow-name>.yaml@v1
    secrets: inherit
```

Use version tags (`@v1`) for stability. See `README.md` for versioning details.

## Available Workflows

### go-lint-test.yaml

Provides linting (golangci-lint) and testing with code coverage for Go projects.

**Inputs:**
- `go-version` (optional, default: '1.26') - Go version to use

**Secrets:**
- `CODECOV_TOKEN` (optional) - Token for uploading coverage to Codecov

**Jobs:**
- `lint` - Runs golangci-lint with latest version
- `test` - Runs tests with coverage and uploads to Codecov if token provided

## Workflow Conventions

### Adding New Workflows

1. Create workflow file in `.github/workflows/`
2. Use `workflow_call` trigger only (no `push`/`pull_request`)
3. Define inputs and secrets explicitly with descriptions
4. Create an EXAMPLE.yaml showing usage
5. Make secrets optional where possible
6. Use meaningful job names that describe what they do
7. Follow semantic versioning - tag releases appropriately

### Naming and Structure

- Use kebab-case for filenames (e.g., `go-lint-test.yaml`)
- Workflow names should describe their purpose
- Keep workflows focused on a single language/stack
- Provide sensible defaults for all inputs
- Document all inputs and secrets
