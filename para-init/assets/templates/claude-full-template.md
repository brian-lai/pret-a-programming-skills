# {PROJECT_NAME} – Context Guide

> **Workflow Methodology:** All workflow practices follow `~/.claude/CLAUDE.md`
> This document provides project-specific context only.

---

## Quick Reference

| Property | Value |
|----------|-------|
| **Purpose** | [One-line project description] |
| **Tech Stack** | [e.g., Node.js, React, PostgreSQL, Redis] |
| **Primary Language** | [e.g., TypeScript] |
| **Architecture** | [e.g., Microservices, Monolith, Serverless] |
| **Repository** | [GitHub/GitLab URL] |

---

## What This Project Does

[2-3 paragraphs explaining the project's purpose, key features, and user base]

---

## Architecture Overview

### System Design

[High-level architecture description or key components]

### Key Components

- **Component A** (`src/services/a/`): [Purpose]
- **Component B** (`src/services/b/`): [Purpose]

### Data Flow

[How data moves through the system]

---

## Tech Stack Details

### Runtime & Frameworks

- **Runtime:** [e.g., Node.js 20.x]
- **Framework:** [e.g., Express.js / Next.js]
- **Language:** [e.g., TypeScript 5.x]

### Data Layer

- **Database:** [e.g., PostgreSQL / MongoDB]
- **Cache:** [e.g., Redis]
- **ORM/Query Builder:** [e.g., Prisma / Drizzle]

### Infrastructure

- **Hosting:** [e.g., AWS / GCP / Vercel]
- **CI/CD:** [e.g., GitHub Actions]
- **Monitoring:** [e.g., DataDog / Sentry]

---

## Code Organization

```
src/
├── api/          # HTTP endpoints and route handlers
├── services/     # Business logic layer
├── models/       # Data models and schemas
├── lib/          # Shared utilities and helpers
├── config/       # Configuration files
└── tests/        # Test suites
```

### Key Files & Directories

| Path | Purpose |
|------|---------|
| `src/api/routes.ts` | Main API route definitions |
| `src/services/auth/` | Authentication & authorization |
| `src/lib/db.ts` | Database connection setup |
| `src/config/env.ts` | Environment configuration |

---

## Conventions & Standards

### Code Style

- **Formatting:** [e.g., Prettier]
- **Linting:** [e.g., ESLint]
- **Naming:** [e.g., camelCase for variables, PascalCase for classes]

### Git Practices

- **Branch naming:** `para/{task-name}` (PARA workflow), `feature/description`, `fix/description`
- **Commit style:** [e.g., Conventional Commits]

### Testing

- **Framework:** [e.g., Jest / Vitest / Mocha]
- **Coverage target:** 80%+
- **Test location:** [e.g., co-located `*.test.ts` or `__tests__/`]

---

## External Integrations

### APIs & Services

- **Service A:** [Purpose, auth method, docs URL]
- **Service B:** [Purpose, auth method, docs URL]

### Environment Variables

Key environment variables (see `.env.example` for full list):

- `DATABASE_URL`: [Description]
- `API_KEY_X`: [Description]

---

## Development Workflow

### Setup

```bash
# Install dependencies
npm install

# Setup environment
cp .env.example .env

# Start dev server
npm run dev
```

### Common Commands

- `npm run dev` – Start development server
- `npm run build` – Build for production
- `npm test` – Run test suite
- `npm run lint` – Lint code

---

## Domain Knowledge

### Business Logic

[Explain key business rules, domain concepts, or complex logic]

### Terminology

- **Term A:** Definition and usage
- **Term B:** Definition and usage

---

## Troubleshooting

### Issue 1: [Common problem]

**Symptoms:** [What you see]
**Solution:** [How to fix]

---

## Additional Resources

- [Team Wiki/Confluence]
- [API Documentation]
- [Architecture Decision Records (ADRs)]
