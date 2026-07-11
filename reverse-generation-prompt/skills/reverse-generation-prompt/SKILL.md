---
name: reverse-generation-prompt
description: >
  Reverse-engineers the current project into a self-contained knowledge package so any
  LLM (ChatGPT, Claude, Gemini, DeepSeek, Cursor, Windsurf, etc.) can reconstruct it
  with minimal information loss. Produces two deliverables — a human+LLM-readable
  PROJECT_BLUEPRINT.md and a machine-readable PROJECT_CONTEXT.json — plus a final
  reconstruction prompt. Use whenever the user asks to "export", "snapshot", "reverse-
  engineer", "extract knowledge from", "document for another LLM", "hand off", "transfer
  context", or "reconstruct" the project, or mentions building a project blueprint / context
  export / long-term memory / knowledge transfer / reverse-generation prompt. Also use when
  the user wants to migrate a project to another AI tool, or asks "what would another LLM
  need to rebuild this?". Trigger even if the word "skill" or "export" is not used.
---

# Skill: reverse-generation-prompt

## Role

You are acting as a **Software Architect, Tech Lead, and Knowledge Engineer**.

Your mission: analyze the currently open project *in full* and produce a knowledge-transfer
document rich enough that another LLM can **reconstruct the project with maximum fidelity** —
even without access to the Git repository or source files.

You are not writing a summary. You are producing a **representation of the project's
knowledge** — its long-term memory. The output must be **self-standing**: comprehensible
without access to the source code.

## What to produce

Two complementary deliverables, written into the project root:

### 1. `PROJECT_BLUEPRINT.md` — exhaustive narrative documentation

For humans *and* LLMs. Covers architecture, decisions, business rules, workflows,
conventions, etc. Structured with hierarchical headings.

**Read `references/blueprint-outline.md` before writing this file.** It contains the
full 22-section analysis checklist (vision, architecture, tree, modules, database,
APIs, workflows, business rules, patterns, decisions, dependencies, configuration,
security, performance, logs, tests, conventions, tech debt, roadmap, reconstruction
guide, LLM summary, reconstruction prompt). Apply every section that is relevant to
the project; omit a section only if it genuinely does not apply, and say so briefly.

### 2. `PROJECT_CONTEXT.json` — structured machine-readable memory

A normalized, schema-conformant representation another LLM or automation tool can reuse
almost directly to regenerate or continue the project.

**Read `references/context-schema.md` before writing this file.** It defines the JSON
schema and the meaning of each field. Validate your output against it mentally before
finalizing.

The two deliverables are complementary: the Markdown preserves reasoning and context,
the JSON provides structured memory. Producing only one is incomplete.

## Workflow

1. **Map the project.** Read the root files (`README`, `package.json` / `pyproject.toml` /
   `go.mod` / `Cargo.toml` / equivalent), config files, the directory tree, and entry
   points. Use search and read tools broadly — fan out, then converge. Do not skip this
   step; surface-level reading produces surface-level output.

2. **Decide what applies.** Not every project has a database, a queue, or auth. For each
   of the 22 blueprint sections, decide *relevant / not applicable*. Omit non-applicable
   sections, but record the omission in one line so the reader knows it was considered.

3. **Draft `PROJECT_BLUEPRINT.md`** following the 22-section outline. Aim for precision
   over volume — every claim should be grounded in something you actually read in the
   project. Where you infer, mark it as inference.

4. **Draft `PROJECT_CONTEXT.json`** following the schema. Keep it valid JSON. Strings for
   free text; arrays for lists; nested objects for structured items (modules, entities,
   APIs, workflows). Empty arrays when there's nothing — never omit required keys.

5. **Write the reconstruction prompt** as the final section of the blueprint (section 22).
   It must be a complete, copy-pasteable prompt another LLM could use to rebuild the
   project. Include: context, objectives, architecture, constraints, technologies,
   conventions, modules, workflows, database, API, features, roadmap.

6. **Sanity-check.** Re-read both files. Does the blueprint let a stranger rebuild the
   project? Does the JSON parse? Is every required schema key present? Fix gaps before
   declaring done.

## Constraints

The output must be:

- **Extremely detailed and precise.**
- **Structured** with hierarchical headings (blueprint) and valid JSON (context).
- **Self-standing** — comprehensible without access to the source.
- **Knowledge-transfer oriented** — written for reconstruction by another LLM.
- **Grounded** — do not invent features, dependencies, or decisions that the project
  does not contain. When something is ambiguous, say so rather than fabricating.

**Do not copy source code wholesale.** Describe its structure, its logic, interface
contracts, algorithms, conventions, and design decisions. When a short code excerpt is
genuinely necessary to convey an interface or algorithm, keep it illustrative and short.

## Output language

Write the deliverables in the **same language the project itself uses** for its docs and
comments (detect from `README`, code comments, commit messages). If the project is
multilingual or has no clear doc language, match the language the user used to invoke this
skill. The skill instructions (this file) are in English for model-adherence reasons; the
*output* need not be.

## Scope

Analyze the entire project directory currently open. If the user points to a subdirectory
or a specific module, focus there but note the scope explicitly at the top of both
deliverables.
