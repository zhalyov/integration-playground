# Project Versioning

This document defines the versioning strategy used throughout the **Integration Playground** project.

The project follows a simplified Semantic Versioning approach adapted for an educational portfolio project.

## Purpose

The version number reflects the maturity of the project rather than individual commits.

A new version is created only after completing a significant project milestone.

## Version Format

The project uses the following format:

```
MAJOR.MINOR.PATCH
```

Example:

```
v0.1.0
```

## Version Components

| Component | Meaning |
|-----------|---------|
| MAJOR | Major project milestone |
| MINOR | Completed sprint or learning phase |
| PATCH | Small improvements or corrections |

## Version Roadmap

| Version | Milestone |
|----------|-----------|
| v0.1.0 | Repository & Project Foundation |
| v0.2.0 | Business Analysis |
| v0.3.0 | System Architecture |
| v0.4.0 | API Contracts |
| v0.5.0 | First Frends Process |
| v0.6.0 | Process Development |
| v0.7.0 | Integrations |
| v0.8.0 | Monitoring & Deployment |
| v0.9.0 | Certification Ready |
| v1.0.0 | Completed Portfolio Project |

## Versioning Rules

- Every major learning milestone increments the MINOR version.
- PATCH versions are reserved for small corrections or improvements.
- Version numbers represent project maturity, not the number of commits.

## Examples

| Scenario | Version |
|----------|---------|
| Initial repository setup | v0.1.0 |
| Completed Business Analysis | v0.2.0 |
| Finished System Architecture | v0.3.0 |
| Small documentation correction | v0.3.1 |

## Release Checklist

Before creating a new release:

- [ ] Sprint completed
- [ ] Documentation updated
- [ ] Repository committed
- [ ] Version tag created
- [ ] GitHub Release published

## Related Documents

- [Git Workflow](../engineering/git-workflow.md)