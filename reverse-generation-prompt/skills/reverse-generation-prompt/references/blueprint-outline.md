# PROJECT_BLUEPRINT.md — 22-section outline

This is the analysis checklist the skill follows when drafting `PROJECT_BLUEPRINT.md`.

For each section: include it if it applies to the project; if it does not apply, record the
omission in one line so the reader knows it was considered. Use hierarchical headings
(`##`, `###`) to keep the document navigable.

---

## 1. Vision générale (Overview)

Describe:
- Objective of the project
- Problem it solves
- Users / audience
- Main features
- Secondary features

## 2. Architecture globale (Overall architecture)

Describe each layer present:
- Frontend
- Backend
- Database
- Cache
- Queue / message broker
- Storage (object / file)
- Authentication
- Notification
- Monitoring
- Infrastructure
- Communication between services (sync/async, protocols)

## 3. Arborescence du projet (Directory tree)

Describe the full tree. For each folder:
- Role
- Responsibility
- Contents

## 4. Description de chaque module (Module descriptions)

For each module:
- Name
- Objective
- Responsibilities
- Inputs
- Outputs
- Dependencies

## 5. Base de données (Database)

Describe:
- Tables / collections
- Relations
- Keys (primary / foreign)
- Constraints
- Indexes
- Migrations

## 6. API

List every API. For each:
- Endpoint (method + path)
- Payload (request)
- Response
- Authentication
- Validation
- Errors

## 7. Flux métier (Business workflows)

Describe all workflows. Examples: login, user creation, intrusion detection, alert
creation, notification, logging. Show the step-by-step flow for each.

## 8. Règles métier (Business rules)

Document every important rule. Use a clear form, e.g.:

```
WHEN <condition>
THEN <action>
```

## 9. Intelligence du projet (Patterns & architecture style)

Identify the patterns in use:
- DDD, CQRS, Clean Architecture, MVC, Hexagonal, Event-Driven, Microservices
- Repository, Factory, Dependency Injection
- Any other structural or design pattern

## 10. Décisions d'architecture (Architecture decisions)

Explain *why* key decisions were made. For each: the decision, the rationale, and the
alternatives that were considered (and why they were rejected).

## 11. Dépendances (Dependencies)

List:
- Frameworks
- Libraries
- SDKs
- External services
- External APIs

## 12. Configuration

Describe:
- Environment variables
- Secrets (names + purpose only — never values)
- Docker / container config
- Compose
- CI/CD
- Build
- Scripts

## 13. Sécurité (Security)

Describe:
- Authentication (JWT, OAuth, session, etc.)
- Permissions / RBAC
- Validation (input sanitization, schema validation)
- Protections (CORS, CSRF, rate limiting, encryption at rest/in transit)

## 14. Performances (Performance)

Describe:
- Cache layers + invalidation strategy
- Optimizations
- Indexes
- Async / background processing
- Bottlenecks or known slow paths

## 15. Logs & observabilité (Logs & observability)

Describe:
- Logging (levels, format, destinations)
- Audit trail
- Monitoring
- Tracing

## 16. Tests

Describe:
- Unit tests
- Integration tests
- End-to-end tests
- Coverage (tools + approximate level)

## 17. Conventions (Conventions)

Describe:
- Naming (files, functions, variables, DB tables)
- Organization
- Patterns enforced across the codebase
- Standards
- Lint
- Formatting

## 18. Dette technique (Technical debt)

Identify:
- Limitations
- Known problems
- Code to improve
- Fragile zones

## 19. Roadmap

Describe:
- Planned features
- Evolutions
- Planned refactors

## 20. Reconstruction (Reconstruction guide)

Produce a step-by-step guide allowing someone to rebuild the project:

1. ...
2. ...
3. ...

## 21. Résumé pour LLM (LLM-optimized summary)

Produce a synthesis optimized to be re-read by another LLM. It must contain:
architecture, components, conventions, rules, dependencies, models, workflows. The format
should minimize context loss — prefer dense, structured bullet lists over prose.

## 22. Prompt de reconstruction (Reconstruction prompt)

At the end of the document, produce a complete, copy-pasteable prompt that another LLM
can use to reconstruct the project. It must contain:
- Context
- Objectives
- Architecture
- Constraints
- Technologies
- Conventions
- Modules
- Workflows
- Database
- API
- Features
- Roadmap
