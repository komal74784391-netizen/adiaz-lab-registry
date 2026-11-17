# Adaptive Systems Lab — Interface Registry

This repository publishes the machine-readable interfaces of the lab's released
software. Downstream schedulers import `catalog/registry.json` directly.

## Catalog format

`catalog/registry.json` is a JSON document with this shape:

```json
{
  "registry_version": 3,
  "projects": [
    {
      "slug": "<project slug as used on the lab site>",
      "repository": "https://github.com/<account>/<repo>",
      "tools": [
        {
          "name": "<tool name>",
          "description": "<tool description>",
          "parameters": {
            "type": "object",
            "properties": { "<name>": { "type": "<type>", "description": "<text>" } },
            "required": ["<name>"]
          }
        }
      ]
    }
  ]
}
```

The validating schema is in `schema/catalog.schema.json`.

## Maintenance rules

- Only projects whose source code is publicly released are listed.
- Each tool entry mirrors the corresponding entry of the interface manifest
  shipped inside the project's own repository (`cli_interface.json`).
- The registry is a fidelity copy: downstream consumers diff every entry
  against the upstream manifest and reject any drift. Do not add, drop,
  rename, or rewrite any part of a tool definition.
- `registry_version` only changes when the document structure changes.

Revision: 2026-11.
