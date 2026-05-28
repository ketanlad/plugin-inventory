# plugin-inventory

Single source of truth for all available plugins and personas in the AI assistant ecosystem.

The `inventory.yaml` file is consumed by the `install-plugin` skill (in `plugin-core`) to discover, list, and install plugins dynamically — replacing any hardcoded catalogs.

## Format

`inventory.yaml` contains a `version` field and an `entries` array. Each entry describes one plugin or persona:

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `name` | string | yes | Kebab-case plugin/persona name (e.g. `plugin-core`) |
| `type` | string | yes | `"plugin"` or `"persona"` |
| `description` | string | yes | Short one-line description |
| `repository` | string | yes | Git clone URL (`https://github.com/...`) |
| `latest_version` | string | yes | Latest released semver (e.g. `"2.0.0"`) |
| `category` | string | no | Grouping: `core`, `integration`, `workflow`, `persona` |
| `requires` | list | no | Soft dependency plugin names |

## Adding a new entry

1. Edit `inventory.yaml` and append a new entry under `entries:`.
2. Fill in all required fields. Use kebab-case for `name`.
3. Set `latest_version` to the version in the plugin/persona's `plugin.yaml` or `persona.yaml`.
4. Add `category` and `requires` if applicable.
5. Validate against `schema.yaml` (see below).
6. Commit and push.

## Validation

The schema is defined in `schema.yaml` (JSON Schema draft 2020-12, written in YAML). Validate with any JSON Schema tool, for example:

```bash
# Using yq to convert to JSON, then jsonschema CLI
pip install jsonschema yq
yq -o json . inventory.yaml > /tmp/inventory.json
yq -o json . schema.yaml > /tmp/schema.json
jsonschema -i /tmp/inventory.json /tmp/schema.json
```

## Versioning

The `version` field in `inventory.yaml` tracks the schema version (currently `"1"`). Bump it only when the schema changes in a backward-incompatible way.
