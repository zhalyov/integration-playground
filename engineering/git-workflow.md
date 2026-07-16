# Git Workflow

This document defines the Git conventions used throughout the **Integration Playground** project.

Its purpose is to ensure a clean, consistent, and understandable Git history.

> **Note**
>
> Version numbering and release management are documented separately in **Project Versioning**.

# Purpose

The Git workflow defines how changes are committed and organized during development.

It establishes conventions for:

- Commit messages
- Commit granularity
- Branch usage
- Git best practices

# Scope

This document covers **only Git usage**.

It does **not** define:

- Project versioning
- Release strategy
- Semantic Versioning

These topics are documented in **Project Versioning**.

# Commit Convention

The project follows the **Conventional Commits** specification.

## Commit Types

| Prefix | Purpose | When to Use | Example |
|---------|----------|-------------|---------|
| `docs:` | Documentation | Documentation changes | `docs: add business requirements` |
| `feat:` | New Feature | Introducing new functionality | `feat: implement receive donation process` |
| `fix:` | Bug Fix | Correcting incorrect behavior | `fix: correct API response mapping` |
| `refactor:` | Refactoring | Improving structure without changing functionality | `refactor: simplify process design` |
| `test:` | Testing | Adding or updating tests | `test: add donation validation scenarios` |
| `chore:` | Maintenance | Repository configuration or maintenance | `chore: update repository structure` |

# Commit Rules

Every commit should represent **one logical change**.

### Every commit should:

- Represent one logical unit of work.
- Be written in the imperative mood.
- Be concise and descriptive.
- Be understandable without additional context.
- Be reviewed before committing.

# Commit Examples

| ✅ Good | ❌ Avoid |
|----------|----------|
| `docs: add project charter` | `updated files` |
| `docs: add business requirements` | `changes` |
| `feat: implement receive donation process` | `final version` |
| `fix: correct validation logic` | `misc updates` |

# Branch Strategy

During the learning phase, development is performed directly on the **main** branch.

As the project grows, feature branches may be introduced to simulate collaborative development.

# Best Practices

- Keep commits small and focused.
- Commit after completing a meaningful unit of work.
- Commit frequently.
- Review changes before committing.
- Avoid committing unfinished work whenever possible.
- Separate documentation changes from implementation changes whenever practical.

# Related Documents

- [Engineering Principles](../engineering/engineering-principles.md)
- [Project Versioning](../engineering/project-versioning.md)