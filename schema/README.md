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

`CodeElement` is omitted for v1 (use `Discovery.location` for scanner spans). Controlled vocabularies are imported from `../taxonomy/`.

## Discovery vs Finding (not synonyms)

| Name | Means | In ontology? |
|------|--------|----------------|
| **Discovery** | DataParade scanner output / code evidence. Product/docs noun; scanner code symbol remains `ScanResult` (ingest maps ScanResult → Discovery). | Yes — class `Discovery` |
| **Finding** | Security-event / OCSF-ish record (GuardDuty, Security Lake, etc.). Not scanner output. Do **not** map Discovery → Finding. | Yes — class `Finding` |
| Kanbus issue type **"finding"** | Gold-review cards. Neither Discovery nor OCSF Finding. | No — docs quarantine only |

Architecture/privacy facts from the scanner cite `Discovery` via `evidenced_by`. Security-event citations use `finding_refs` → `Finding`.


## Edges

Do not treat all object properties as the same kind of graph edge:

| Kind | Slots | Shape |
|------|--------|--------|
| Dependency / routing | `interacts_with`, `uses`, `exposes`, `routes_to` | Simple object slots (lists of `NamedThing` ids). Ranges are intentionally broad in v0.1; tighten with `slot_usage` when real graphs show noise. |
| Data / privacy flow | `sends_data_to` | Inlined list of `SendsDataTo` **association objects** (`source` / `target`, `data_categories`, `purpose`, `evidenced_by`). |

Query helpers and diagram generators ([DATAP-645](https://dataparade.atlassian.net/browse/DATAP-645)) must expand `SendsDataTo` rather than walking it like `interacts_with`.

See [DATAP-641](https://dataparade.atlassian.net/browse/DATAP-641).
