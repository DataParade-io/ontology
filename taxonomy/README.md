# taxonomy/

Controlled vocabularies used by the schema. Prefer the word **vocabulary** in prose; this folder is `taxonomy/` (not an abbreviation).

Each file is a LinkML enum module imported by `schema/core.yaml`:

| File | Enum | Use |
|------|------|-----|
| `data_category.yaml` | `DataCategory` | Kinds of data on `sends_data_to` |
| `purpose.yaml` | `Purpose` | Why a flow exists |
| `actor_kind.yaml` | `ActorKind` | Person / role / persona |
| `external_system_category.yaml` | `ExternalSystemCategory` | Rollup bucket for `ExternalSystem` |

These are often hierarchical (`DataCategory` uses `is_a` on permissible values). Customer-specific terms stay closed. Public seed **aliases** (package → system) belong in `../catalog/`, not here.

See [DATAP-654](https://dataparade.atlassian.net/browse/DATAP-654).
