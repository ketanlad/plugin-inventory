# plugin-inventory

Data-only repository containing the plugin/persona inventory manifest for the AI assistant ecosystem.

## Purpose

`inventory.yaml` is the single source of truth for all available plugins and personas. It is fetched at runtime by `plugin-core`'s `install-plugin` skill to discover and install plugins dynamically.

## Files

| File | Purpose |
|------|---------|
| `inventory.yaml` | The inventory manifest — all plugin/persona entries |
| `schema.yaml` | JSON Schema (draft 2020-12) for validating `inventory.yaml` |
| `README.md` | Format documentation and instructions for adding entries |
| `CLAUDE.md` | This file — AI assistant instructions |

## Conventions

- **No code, no tests** — this is a data-only repo. Changes are limited to YAML edits.
- **Versions must match source** — `latest_version` must reflect the actual version in each plugin/persona's own `plugin.yaml` or `persona.yaml`.
- **Kebab-case names** — all entry names use kebab-case (e.g. `plugin-core`, `persona-pa`).
- **Schema validation** — after editing `inventory.yaml`, validate it against `schema.yaml`.
- **Required fields** — every entry must have: `name`, `type`, `description`, `repository`, `latest_version`.
- **Repository URLs** — follow the pattern `https://github.com/ketanlad/<name>`.

## When to update

- A new plugin or persona repo is created — add an entry.
- A plugin/persona releases a new version — update `latest_version`.
- A plugin's dependencies change — update `requires`.
- A plugin/persona is archived — remove its entry.
