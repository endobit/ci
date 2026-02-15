# Release Process

This repo uses semantic versioning with Git tags for workflow releases.

## Version Format

- **Major** (v1 → v2): Breaking changes to workflow inputs/outputs/behavior
- **Minor** (v1.0 → v1.1): New features, backwards compatible
- **Patch** (v1.0.0 → v1.0.1): Bug fixes, backwards compatible

## Creating a Release

### 1. Create annotated tag for specific version

```bash
git tag -a v1.0.0 -m "Release v1.0.0

- Initial release of go-lint-test workflow"
git push origin v1.0.0
```

### 2. Update/create floating major version tag

```bash
# Delete old tag locally and remotely
git tag -d v1
git push origin :refs/tags/v1

# Create new annotated tag pointing to latest
git tag -a v1 -m "Update v1 to v1.0.0"
git push origin v1
```

Or use force push (simpler):

```bash
git tag -fa v1 -m "Update v1 to v1.0.0"
git push origin v1 --force
```

## Examples

**Patch release (bug fix):**
```bash
git tag -a v1.0.1 -m "fix: correct codecov token handling"
git tag -fa v1 -m "Update v1 to v1.0.1"
git push origin v1.0.1 v1 --force
```

**Minor release (new feature):**
```bash
git tag -a v1.1.0 -m "feat: add support for custom test flags"
git tag -fa v1 -m "Update v1 to v1.1.0"
git push origin v1.1.0 v1 --force
```

**Major release (breaking change):**
```bash
git tag -a v2.0.0 -m "feat!: rename go-version input to golang-version

BREAKING CHANGE: go-version input renamed to golang-version"
git tag -a v2 -m "Create v2 major version"
git push origin v2.0.0 v2
```

## Notes

- Always use annotated tags (`-a`) for releases
- Floating tags (v1, v2) should be force-pushed as they move
- Specific version tags (v1.0.0) are immutable - never force push
- Include release notes in tag message
