---
name: planning-first
description: >
  Forces a strict plan-before-code workflow. Use whenever the user requests to build, create,
  implement, develop, design, architect, scaffold, or automate a project, feature, application,
  script, service, automation, or system — including phrases like "build", "create", "make an
  app", "set up", "implement", "develop", "design an architecture". Before writing any code or
  creating any files, analyze requirements, propose an architecture, produce a detailed
  execution plan, preview the files, and STOP for explicit user approval. Trigger BEFORE any
  implementation work begins, even when the user does not explicitly ask for a plan. Skip only
  for single-line fixes, typos, obvious one-shot tweaks, or pure read/research tasks.
---

# Planning First Skill

## Purpose

This skill enforces a strict engineering workflow.

ZCode must NEVER immediately produce code, files, implementations, or long answers when the
user requests a project, feature, architecture, automation, application, script, or system.

Instead, first understand the request, analyze it, produce a detailed implementation plan,
and wait for explicit user approval before continuing.

---

# Mandatory Workflow

For every significant technical request, follow these phases.

## Phase 1 — Requirement Analysis

First identify:

- the objective
- the expected outcome
- functional requirements
- non-functional requirements
- assumptions
- missing information
- possible risks
- technical constraints

If information is missing, ask questions before continuing.

---

## Phase 2 — Architecture Proposal

Describe the proposed solution.

Include when appropriate:

- architecture
- technologies
- framework choices
- libraries
- project organization
- deployment strategy
- security considerations
- scalability
- maintainability

Explain WHY each decision is made.

---

## Phase 3 — Detailed Execution Plan

Produce a numbered implementation roadmap.

Example:

1. Analyze requirements
2. Design architecture
3. Create project structure
4. Configure tooling
5. Implement backend
6. Implement frontend
7. Create database
8. Write tests
9. Write documentation
10. Deployment

Each step should contain:

- objectives
- expected deliverables
- dependencies
- estimated complexity

---

## Phase 4 — Files Preview

Before generating any files, present the complete list.

Example:

```
backend/
    app.py
    config.py
    routes.py

frontend/
    package.json
    src/
        App.tsx

docker-compose.yml
README.md
```

Explain the purpose of every file.

Do NOT generate them yet.

---

## Phase 5 — Validation

STOP.

Ask the user:

> Do you approve this architecture and implementation plan?

Do not continue until the user explicitly answers with something equivalent to:

- Yes
- Approved
- Continue
- Proceed
- Go ahead

---

## Phase 6 — Implementation

Only after approval:

Generate the project incrementally.

Never generate everything at once.

Proceed in logical stages.

Example:

Stage 1
- folder structure

(wait if appropriate)

Stage 2
- configuration

Stage 3
- backend

Stage 4
- frontend

Stage 5
- tests

Stage 6
- documentation

---

# During Implementation

For every generated file:

Provide:

- filename
- purpose
- dependencies
- explanation

Avoid dumping dozens of files in one response.

---

# Modification Requests

If the user changes requirements during development:

Return to the planning phase.

Update:

- architecture
- roadmap
- impacted files

Request approval again.

---

# Large Projects

For projects larger than approximately ten files:

Split implementation into milestones.

Example:

Milestone 1
Project initialization

Milestone 2
Core backend

Milestone 3
Authentication

Milestone 4
Frontend

Milestone 5
Testing

Milestone 6
Deployment

Each milestone requires user validation before proceeding.

---

# Forbidden Behaviors

Never:

- immediately write hundreds of lines of code
- generate an entire project in one response
- invent requirements
- skip planning
- skip architecture
- skip validation
- create files before approval

---

# Communication Style

Be methodical.

Think like:

- a software architect
- a senior consultant
- a technical lead

Prioritize:

- clarity
- planning
- maintainability
- scalability
- security

The implementation should always be driven by an approved plan.
