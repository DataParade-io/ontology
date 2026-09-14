# catalog/

Public seed aliases for rollup: packages, SDK import fragments, hostnames, and match keys → canonical `ExternalSystem` ids (`dp:external/...`).

Customer-specific aliases stay in closed intelligence — not in this public repo.

## Files

| File | Role |
|------|------|
| `external_systems.yaml` | Seed catalog aligned with DataParade-io/scanner `third-party.classifier.yaml` and `third-party.patterns.yaml` |

Validated against `../schema/catalog.yaml` in CI.

## Entry shape

Each `entries[]` row has:

- `id` — stable URI for the canonical `ExternalSystem` (e.g. `dp:external/stripe`)
- `canonical_name` — display label for landscape/context diagrams
- `category` — `ExternalSystemCategory` from `../taxonomy/external_system_category.yaml`
- `aliases` — `packages`, `hosts`, `import_fragments`, `keys` (at least one list non-empty)

Ingest resolves any alias hit to `id`. Instance graphs may still attach customer-specific aliases in closed intelligence.

`Container` aliases are not seeded yet; add a sibling file when a concrete rollup need appears.

See [DATAP-642](https://dataparade.atlassian.net/browse/DATAP-642).
