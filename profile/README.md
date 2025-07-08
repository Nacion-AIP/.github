# Nación-AIP

We build custom AI solutions for small and medium businesses in Mexico.  
From machine learning pipelines to production-ready APIs and infrastructure.

---

## Repository Overview

We manage multiple repositories across several domains:

| Domain                   | Purpose                                                              | Example Repos                                 |
|--------------------------|----------------------------------------------------------------------|-----------------------------------------------|
| Core Infrastructure      | Terraform blueprints, CI/CD workflows, authentication, shared tooling| `core-terraform`, `auth-infra`                |
| AI/ML Engines            | Data ingestion, forecasting, and optimization pipelines              | `dp-forecast-engine`, `dp-etl-pipelines`, `dp-order-optimizer` |
| Client-Facing Apps       | Frontend interfaces for clients and internal teams (Next.js)         | `dp-app`, `dp-app-legacy`, `ka-app`                            |
| API Backends             | REST APIs with auth logic and data services                          | `dp-api`                                      |
| Internal Tools & Utilities | Developer tools, monitoring, and repo templates                   | `...`       |

> To browse all repositories, see the [Repositories tab »](https://github.com/orgs/Nacion-AIP/repositories)

---

## Repository Naming Convention

We follow a **domain-based naming convention** to keep the repository structure scalable and clear:

| Prefix   | Domain               | Example Repositories               |
|----------|----------------------|------------------------------------|
| `dp-`    | Demand Planning       | `dp-app`, `dp-api`, `dp-app-legacy`, `dp-etl-pipelines`       |
| `ka-`    | Knowledge Agents      | `ka-app`                           |
| `core-`  | Shared Infra/Tooling  | `core-terraform`, `auth-infra`     |

---

## Getting Started

To contribute or set up a local environment:

1. **Clone the repository**
2. **Install dependencies**
   - For Python projects, use [`uv`](https://github.com/astral-sh/uv)
   - For Node.js projects, use [`pnpm`](https://pnpm.io/)
3. **Set up pre-commit hooks** (Python projects only)
   ```bash
   uv run pre-commit install
   ```
4. Follow setup instructions in the repo's `README.md`
5. Review our [Contribution Guide](https://github.com/Nacion-AIP/.github/blob/main/CONTRIBUTING.md)

---

## Code Quality Standards

### Python Projects

All Python repositories use automated code quality checks that run before each commit. These checks ensure consistent code style, security, and quality across the team.

**Pre-commit hooks include:**
- **Black**: Code formatting
- **Ruff**: Linting and code fixes
- **MyPy**: Static type checking
- **Bandit**: Security scanning
- **Pytest**: Test execution
- **Import organization**: Automatic import sorting and cleanup

**Setup (required for Python contributors):**
```bash
# Install pre-commit hooks (one-time setup)
uv run pre-commit install

# Run all checks manually (recommended before PR)
uv run pre-commit run --all-files
```

**What happens during commits:**
- Pre-commit automatically runs on staged files
- If checks fail, the commit is blocked until issues are fixed
- Most formatting issues are auto-fixed - just re-stage and commit

> **Note**: Pre-commit hooks are already configured in Python repositories with `.pre-commit-config.yaml` and `bandit.yaml` files.

---

## Style Guides

Style guides for [Python](https://link-to-python-style-guide) and [TypeScript](https://link-to-ts-style-guide)

---

## Contributing Guidelines

### Before submitting a PR:

**For Python projects:**
1. Ensure pre-commit hooks are installed: `uv run pre-commit install`
2. Run all quality checks: `uv run pre-commit run --all-files`
3. Fix any issues reported by the checks
4. All tests must pass

**For all projects:**
- Follow the repository's specific setup instructions
- Write tests for new functionality
- Update documentation as needed

### PR Review Process:
- All PRs require at least 1 codeowner review before merging
- Address all feedback before requesting re-review
- Ensure CI/CD checks pass

---

## Deprecation Notice

| Deprecated Repo | Replaced by                   | Notes                                     |
|------------------|-------------------------------|-------------------------------------------|
| `dp-app-legacy`  | `dp-api` + `dp-app`           | Split into backend and frontend repos     |
|                  |                               | Retained as `dp-app-legacy` for reference |

