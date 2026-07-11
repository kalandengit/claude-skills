# PROJECT_CONTEXT.json — schema & field notes

This is the schema the skill follows when drafting `PROJECT_CONTEXT.json`. The JSON is the
project's structured long-term memory — another LLM or automation tool should be able to
consume it almost directly to regenerate or continue the project.

## Schema

```json
{
  "project": {
    "name": "string — project name",
    "goal": "string — one- or two-sentence statement of what the project does and why",
    "stack": {
      "frontend": "string | null — framework/language, version if known",
      "backend": "string | null — framework/language, version if known",
      "database": "string | null — engine + version if known",
      "cache": "string | null",
      "queue": "string | null",
      "storage": "string | null",
      "auth": "string | null",
      "infrastructure": "string | null"
    },
    "architecture": "string — short description of the architectural style (e.g. 'modular monolith, Clean Architecture, CQRS')",
    "modules": [
      {
        "name": "string",
        "objective": "string",
        "responsibilities": ["string"],
        "inputs": ["string"],
        "outputs": ["string"],
        "dependencies": ["string — names of other modules or external packages"]
      }
    ],
    "entities": [
      {
        "name": "string — table/collection or domain entity name",
        "fields": [
          { "name": "string", "type": "string", "constraints": "string | null" }
        ],
        "relations": ["string — e.g. 'belongs_to User', 'has_many Order'"],
        "indexes": ["string"]
      }
    ],
    "apis": [
      {
        "endpoint": "string — METHOD /path",
        "description": "string",
        "request": "string — payload shape or schema ref",
        "response": "string — response shape",
        "auth": "string | null",
        "validation": ["string"],
        "errors": ["string — error codes / shapes"]
      }
    ],
    "workflows": [
      {
        "name": "string",
        "trigger": "string — what starts it",
        "steps": ["string — ordered"],
        "outcome": "string"
      }
    ],
    "business_rules": [
      "string — each rule in 'WHEN ... THEN ...' form"
    ],
    "patterns": ["string — DDD, CQRS, Repository, Factory, ..."],
    "decisions": [
      {
        "decision": "string",
        "rationale": "string",
        "alternatives": ["string"]
      }
    ],
    "dependencies": [
      { "name": "string", "version": "string | null", "purpose": "string" }
    ],
    "configuration": {
      "env_variables": [
        { "name": "string", "purpose": "string", "required": "boolean" }
      ],
      "secrets": ["string — names only, never values"],
      "build": "string | null",
      "scripts": ["string"]
    },
    "security": {
      "authentication": "string | null",
      "authorization": "string | null — e.g. RBAC roles",
      "validation": ["string"],
      "protections": ["string — CORS, CSRF, rate limiting, encryption, ..."]
    },
    "performance": {
      "cache": ["string — layers + invalidation"],
      "optimizations": ["string"],
      "async": ["string — background jobs, queues"]
    },
    "observability": {
      "logging": "string | null",
      "audit": "string | null",
      "monitoring": "string | null",
      "tracing": "string | null"
    },
    "tests": {
      "unit": "string | null",
      "integration": "string | null",
      "e2e": "string | null",
      "coverage": "string | null"
    },
    "conventions": {
      "naming": "string | null",
      "organization": "string | null",
      "lint": "string | null",
      "formatting": "string | null"
    },
    "tech_debt": ["string — each item a limitation, problem, or fragile zone"],
    "roadmap": ["string — planned features / evolutions / refactors"]
  }
}
```

## Rules

- **Valid JSON only.** No comments, no trailing commas. Parse it mentally before writing.
- **Every top-level key under `project` is required.** Use `null` for a single-value field
  that doesn't apply, and an empty array `[]` for a list field with no entries. Never omit
  a required key — an absent key means "I didn't check", whereas `[]` means "I checked,
  there are none".
- **Ground everything.** Only populate a field with something the project actually
  contains. If you cannot verify a dependency, pattern, or rule, either omit the array
  entry or mark it `"unverified"` — do not invent.
- **No secret values.** The `secrets` array holds *names* only (`DATABASE_URL`,
  `JWT_SECRET`), never the values themselves.
- **Strings for free text, arrays for lists.** Keep free-text strings concise — this is
  the structured memory, not the narrative; the narrative lives in `PROJECT_BLUEPRINT.md`.
- **Match the project's language** for human-readable strings (descriptions, rationale).
  Field names and keys stay in English.
