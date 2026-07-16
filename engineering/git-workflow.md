# Git Workflow

This document defines the Git workflow used throughout the **Integration Playground** project.

The goal is to keep the Git history clean, readable, and consistent throughout the project.

## Purpose

The Git workflow establishes a common convention for:

- Commit messages
- Commit granularity
- Branch usage
- Collaboration

Versioning rules are documented separately in the [Versioning Strategy](versioning-strategy.md).

## Commit Convention

The project follows the **Conventional Commits** specification.

### Commit Types

| Prefix | Purpose | When to Use | Example |
|---------|---------|-------------|---------|
| `docs:` | Documentation | Documentation changes | `docs: add business requirements` |
| `feat:` | New Feature | Introducing new functionality | `feat: implement receive donation process` |
| `fix:` | Bug Fix | Correcting incorrect behavior | `fix: correct API response mapping` |
| `refactor:` | Refactoring | Improving structure without changing behavior | `refactor: simplify process design` |
| `test:` | Testing | Adding or updating tests | `test: add donation validation scenarios` |
| `chore:` | Maintenance | Repository configuration and maintenance | `chore: update repository structure` |

## Commit Rules

Every commit should represent **one logical change**.

### Good Examples

```text
docs: add project charter

feat: implement receive donation process

fix: correct validation logic
```

### Avoid

```text
updated files

changes

final version

misc updates
```

Commit messages should:

- be written in the imperative mood
- describe one logical change
- remain short and descriptive

## Branch Strategy

During the learning phase, development is performed directly on the **main** branch.

Feature branches may be introduced later when working on larger features or experiments.

## Best Practices

- Make small, focused commits.
- Commit frequently.
- Avoid mixing documentation and implementation in the same commit whenever possible.
- Write meaningful commit messages.
- Review changes before committing.

## References

- [Conventional Commits](https://www.conventionalcommits.org/)
- [Versioning Strategy](versioning-strategy.md)