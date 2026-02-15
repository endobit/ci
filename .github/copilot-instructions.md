# Copilot Instructions for endobit/ci

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
    uses: endobit/ci/.github/workflows/<workflow-name>.yaml@main
    secrets: inherit
```

See `EXAMPLE.yaml` in each workflow directory for usage patterns.

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

## Conventions

### Git Commits

Use [Conventional Commits](https://www.conventionalcommits.org/) format:

```
<type>: <description>

[optional body]
```

Common types: `feat`, `fix`, `chore`, `docs`, `refactor`, `test`, `ci`

Examples:
- `feat: add python-lint-test workflow`
- `fix: correct go-version input handling`
- `docs: update EXAMPLE.yaml usage`
- `chore: update golangci-lint to v9`

### Adding New Workflows

1. Create workflow file in `.github/workflows/`
2. Use `workflow_call` trigger only
3. Define inputs and secrets explicitly
4. Create an EXAMPLE.yaml showing usage
5. Make secrets optional where possible (use conditionals)
6. Use meaningful job names that describe what they do

### Workflow Naming

- Use kebab-case for filenames (e.g., `go-lint-test.yaml`)
- Workflow names should be descriptive of their purpose
- Keep workflows focused on a single language/stack when possible

### Inputs and Secrets

- Provide sensible defaults for inputs
- Make inputs optional where reasonable
- Document all inputs and secrets with descriptions
- Use conditional logic to handle missing secrets gracefully
