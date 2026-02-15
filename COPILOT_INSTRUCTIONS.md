# Endobit Organization - Copilot Instructions

This file contains common conventions and practices for all endobit repositories. Individual repos may have their own `.github/copilot-instructions.md` with repo-specific details.

## Git Commits

Use [Conventional Commits](https://www.conventionalcommits.org/) format:

```
<type>: <description>

[optional body]
```

**Common types:**
- `feat` - New feature
- `fix` - Bug fix
- `chore` - Maintenance tasks (deps, config)
- `docs` - Documentation changes
- `refactor` - Code restructuring without behavior change
- `test` - Adding or updating tests
- `ci` - CI/CD changes
- `perf` - Performance improvements

**Examples:**
- `feat: add user authentication`
- `fix: correct validation logic for email`
- `docs: update README installation steps`
- `chore: update dependencies`
- `refactor: extract helper functions`

## Code Review and Pull Requests

- Keep PRs focused on a single concern
- Write descriptive PR titles using conventional commits format
- Link related issues in PR description
- Respond to review comments promptly

## Testing

- Write tests for new features
- Ensure existing tests pass before committing
- Include both happy path and edge cases
