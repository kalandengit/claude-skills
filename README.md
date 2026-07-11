# kalandengit-skills

A ZCode plugin marketplace for personal, reusable skills.

## Plugins

| Plugin | Description |
| --- | --- |
| `planning-first` | Plan before code. Produces a structured plan before any implementation work begins. |
| `reverse-generation-prompt` | Reverse-engineers a project into a self-contained knowledge package (`PROJECT_BLUEPRINT.md` + `PROJECT_CONTEXT.json` + reconstruction prompt) so any LLM can rebuild it with minimal information loss. |
| `it-prompt-specialist` | Senior multidisciplinary IT expert lens across software engineering, infrastructure, cybersecurity, cloud, AI/ML, data, networking, embedded, game dev, and project management. |

## Install (in the ZCode client)

Add this marketplace:

```
/plugin marketplace add kalandengit/claude-skills
```

Install a plugin:

```
/plugin install planning-first@kalandengit-skills
```

Manage installed plugins under **Settings → Plugin Management**.

## Layout

```
claude-skills/
├── marketplace.json                          ← marketplace manifest (name + plugin list)
└── planning-first/                           ← the plugin
    ├── .zcode-plugin/plugin.json             ← plugin manifest
    └── skills/planning-first/SKILL.md        ← the skill body
```

## Adding a new plugin

1. Create `<plugin-name>/` at the repo root.
2. Add `<plugin-name>/.zcode-plugin/plugin.json` with a `name` matching `^[a-z0-9][a-z0-9._-]{0,127}$`.
3. Add the plugin's components (skills, commands, hooks, …) under `<plugin-name>/`.
4. Register it in `marketplace.json` under `plugins[]` with a relative `source`.
5. Commit and push — the client picks it up on next marketplace refresh.
