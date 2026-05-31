# plugin-inventory

Data-only repository containing the installable-component inventory manifest for
the AI assistant ecosystem. Entries span all four component types from the
unified contract (`workspace-core`'s `ComponentManifest`, AI-414): `plugin`,
`persona`, `gateway`, `service`.

## Purpose

`inventory.yaml` is the single source of truth for all available plugins and personas. It is fetched at runtime by ai-assistant's `InventoryClient` (configured via `config.agent.plugin_registries`) and used by the built-in `install-plugin` skill and dashboard to discover and install plugins dynamically.

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
- **Component types** — `type` is one of `plugin`, `persona`, `gateway`, `service`. `plugin`/`persona` are static; `gateway`/`service` are managed processes (their `component.yaml` carries a `process:` descriptor registered in the supervisor process table on install). `ai-assistant` is the foundational `service` (WS bus on :8767).
- **`recommended_first`** — optional boolean (default `false`). Flags the foundational components the dashboard first-run flow highlights ahead of optional add-ons (Story AI-424 / AI-427): `ai-assistant` + `plugin-core`. Advisory metadata only.
- **Repository URLs** — follow the pattern `https://github.com/ketanlad/<name>`.

## When to update

- A new plugin or persona repo is created — add an entry.
- A plugin/persona releases a new version — update `latest_version`.
- A plugin's dependencies change — update `requires`.
- A plugin/persona is archived — remove its entry.
