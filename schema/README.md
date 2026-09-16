# schema/

LinkML modules for the DataParade public ontology. Author here. Optional OWL/JSON Schema views belong in `../generated/`.

| File | Contents |
|------|----------|
| `ontology.yaml` | Root schema (imports the modules below) |
| `core.yaml` | `NamedThing`, `Discovery`, `Finding`, `Evidenced`, `Association`, shared slots |
| `static.yaml` | `System`, `Actor`, `ExternalSystem`, `Container`, `Component` |
| `portfolio.yaml` | `Scope`, `in_portfolio` |
| `deployment.yaml` | `Environment`, `DeploymentNode`, `InfrastructureNode`, `Instance` |
| `privacy.yaml` | `SendsDataTo` / `sends_data_to` (`data_categories`, `purpose`) |
| `catalog.yaml` | Public alias catalog meta-schema (`PublicAliasCatalog`, `ExternalSystemCatalogEntry`) |

`CodeElement` is omitted for v1 (use `Discovery.location` for scan/cloud locators). Controlled vocabularies are imported from `../taxonomy/`.

## Discovery vs Finding (not synonyms)

| Name | Means | In ontology? |
|------|--------|----------------|
| **Discovery** | **Sourced assertion of a graph fact** — a learning record with mandatory immutable `source` ∈ {`scan`, `cloud`, `interview`}. Asserts an entity or association (`asserts`); optional `asserted_slot` / `asserted_value` for attribute fills. Entities (`System`, `Actor`, `SendsDataTo`, …) stay entities — not subclasses of Discovery. | Yes — class `Discovery` |
| **Finding** | Security-event / OCSF-ish record (GuardDuty, Security Lake, etc.). Not scanner output or interview answers. Do **not** map Discovery → Finding. | Yes — class `Finding` |
| Kanbus issue type **"finding"** | Gold-review cards. Neither Discovery nor OCSF Finding. | No — docs quarantine only |

Graph facts cite supporting Discoveries via `asserted_by` on the `Evidenced` mixin. Security-event citations use `finding_refs` → `Finding`.

### Discovery source rules (0.2+)

- `source` is **immutable after create** — never retcon `interview` → `scan`. Corrections use a new `Discovery` with `supersedes`.
- Interview-sourced Discoveries require human `reviewer` + `raw_evidence_ref` to land in living KB.
- Scan-sourced identity wins conflicts; interview/cloud assertions that would rewrite scan-known identity → escalate, do not land.

## Edges

Do not treat all object properties as the same kind of graph edge:

| Kind | Slots | Shape |
|------|--------|--------|
| Dependency / routing | `interacts_with`, `uses`, `exposes`, `routes_to` | Simple object slots (lists of `NamedThing` ids). Ranges are intentionally broad in v0.1; tighten with `slot_usage` when real graphs show noise. |
| Data / privacy flow | `sends_data_to` | Inlined list of `SendsDataTo` **association objects** (`source` / `target`, `data_categories`, `purpose`, `asserted_by`). |

Query helpers and diagram generators ([DATAP-645](https://dataparade.atlassian.net/browse/DATAP-645)) must expand `SendsDataTo` rather than walking it like `interacts_with`.

See [DATAP-641](https://dataparade.atlassian.net/browse/DATAP-641), [DATAP-681](https://dataparade.atlassian.net/browse/DATAP-681), [DATAP-684](https://dataparade.atlassian.net/browse/DATAP-684).
