# schema/

LinkML modules for the DataParade public ontology. Author here. Optional OWL/JSON Schema views belong in `../generated/`.

| File | Contents |
|------|----------|
| `ontology.yaml` | Root schema (imports the modules below) |
| `core.yaml` | `NamedThing`, `Finding`, `Evidenced`, `Association`, shared slots |
| `static.yaml` | `System`, `Actor`, `ExternalSystem`, `Container`, `Component` |
| `portfolio.yaml` | `Scope`, `in_portfolio` |
| `deployment.yaml` | `Environment`, `DeploymentNode`, `InfrastructureNode`, `Instance` |
| `privacy.yaml` | `SendsDataTo` / `sends_data_to` (`data_categories`, `purpose`) |

`CodeElement` is omitted for v1 (use `Finding.location`). Controlled vocabularies are imported from `../taxonomy/`.

See [DATAP-641](https://dataparade.atlassian.net/browse/DATAP-641).
