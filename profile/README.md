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
| Client-Facing Apps       | Frontend interfaces for clients and internal teams (Next.js)         | `dp-app`, `ka-app`                            |
| Internal Tools & Utilities | Developer tools, monitoring, and repo templates                   | `...`       |

> To browse all repositories, see the [Repositories tab »](https://github.com/orgs/Nacion-AIP/repositories)

---

## Getting Started

To contribute or set up a local environment:

1. **Clone the repository**
2. **Install dependencies**
   - For Python projects, use [`uv`](https://github.com/astral-sh/uv)
   - For Node.js projects, use [`pnpm`](https://pnpm.io/)
3. Follow setup instructions in the repo’s `README.md`
4. Review our [Contribution Guide](https://github.com/Nacion-AIP/.github/blob/main/CONTRIBUTING.md)

---

## Documentation & Internal Resources

- **Confluence (Internal Docs):** [link]
- **API Reference:** [link to Swagger/Postman or repo path]
- **Data Dictionary:** [link or repo]
- **Infrastructure Diagrams:** [link or diagrams in `core-terraform`]

---

## Standards & Best Practices

- Python and Node project templates available in `repo-template-*`
- CI/CD configured with GitHub Actions (`.github/workflows`)
- Secrets managed using GitHub Encrypted Secrets
- Infrastructure managed with Terraform (`core-terraform`)
- Style guides for [Python](https://link-to-python-style-guide) and [TypeScript](https://link-to-ts-style-guide)

---

## Tooling Summary

| Area              | Tool / Stack                      |
|-------------------|-----------------------------------|
| Package Management| `uv` (Python), `pnpm` (Node.js)   |
| ML Lifecycle      | MLflow                            |
| Infra Provisioning| Terraform                         |
| Monitoring & Logs | TBD / in development              |

---

## Contact & Support

- Bug or issue? Open a GitHub Issue or Discussion in the relevant repository.
- DevOps or infrastructure support: `#devops-internal` on Slack
