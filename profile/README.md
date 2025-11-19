# Nación-AIP

This document provides a brief overview of the repository structure, naming conventions, and essential information required to work within the Nación-AIP organization. For detailed documentation, refer to the team's Confluence space:

[Confluence - Team Space](https://entropia-team.atlassian.net/wiki/x/7wC7Aw)

---

## Team Playbook

The complete documentation for development culture, workflows, standards, processes, deployment, onboarding, and engineering practices is maintained in the team's knowledge base.

Contents include:
- Development culture and weekly rhythm
- PR review and approval guidelines
- Deployment procedures
- Development environment setup
- Architecture and design patterns
- Runbooks and troubleshooting
- Onboarding resources

[Confluence - Team Handbook](https://entropia-team.atlassian.net/wiki/spaces/naip/folder/358449153?atlOrigin=eyJpIjoiMTBjMzJlM2E0ZTY1NGI1ZWJkZDk2MDA0N2QxNWE2MzMiLCJwIjoiYyJ9)

---

## Repository Naming Convention

Repositories follow a domain-oriented naming structure:

| Prefix | Domain |
|--------|----------------------|
| `dp-` | Demand Planning |
| `ka-` | Knowledge Agents |
| `core-` | Shared Infrastructure |
| `av-` | Legacy Avis Project |

This ensures scalable organization across product areas.

---

## Getting Started

1. Clone the repository.

2. Install dependencies:
   - Python projects use `uv` for environment and package management.
   - Node.js projects use `pnpm`.

3. (Python) Install pre-commit hooks:
   ```bash
   uv run pre-commit install
   ```

4. Follow any additional setup steps described in the repository's internal README.

5. Consult the Confluence documentation for process and workflow details.

---

## Code Quality Standards

### Python Projects

Python repositories use automated checks through pre-commit. These include:
- Black for formatting
- Ruff for linting and fixes
- MyPy for static typing
- Bandit for security scanning
- Pytest for test execution
- Import sorting and cleanup

Run checks manually:

```bash
uv run pre-commit run --all-files
```

### Node/TypeScript Projects

Use the ESLint configuration and Prettier rules included in each repository. Additional language-specific guidelines are available in the documentation.

---

## Contributing Guidelines

Before submitting a pull request:

### Python Projects

- Install pre-commit hooks.
- Run all checks:
  ```bash
  uv run pre-commit run --all-files
  ```
- Resolve any reported issues.
- Ensure all tests pass.

### All Projects

- Follow the repository's setup and style guidelines.
- Ensure code builds successfully.
- Include tests for new functionality.
- Update documentation where appropriate.

Refer to the team documentation for complete contribution and review guidelines.

---

## Branching and Review Process

- The `staging` branch deploys to the staging environment.
- The `main` branch deploys to production.

**Approval requirements:**
- Staging: one approval from a senior engineer.
- Main: one approval from the code owners.

**Review expectations:**
- Staging pull requests are reviewed within 4 hours.
- Main pull requests are reviewed within 1 day.

---

## Deprecation Notice

| Deprecated Repository | Replacement | Notes |
|----------------------|-------------|---------------------------|
| `dp-app-legacy` | `dp-api` and `dp-app` | Retained for reference |

---
