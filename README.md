# DataParade ontology

Public **LinkML** schema, **taxonomy**, and **catalog** for DataParade architecture and privacy knowledge graphs (including C4 diagram projections).

Instance knowledge, ingest, diagram generation, and customer-specific aliases stay in closed intelligence (Papyrus); this repo is the public contract.

**Discovery** (sourced assertion of a graph fact — `scan` | `cloud` | `interview`) and **Finding** (security-event / OCSF-ish) are different types — not synonyms.

Prefer the full word **vocabulary** in prose. The folder for controlled term sets is **`taxonomy/`**.

**LinkML** is the authoring format ([linkml.io](https://linkml.io/)). **OWL** (and SKOS for taxonomies) may be **generated** later — not how we author the schema.

## Layout

```text
schema/       # LinkML classes and slots (static, portfolio, deployment, privacy)
taxonomy/     # DataCategory, Purpose, ActorKind, ExternalSystemCategory
catalog/      # public seed aliases (DATAP-642)
generated/    # JSON Schema, docs; later OWL/SKOS
```

Validate locally: `linkml validate schema/ontology.yaml`

Validate catalog: `linkml validate -s schema/catalog.yaml catalog/external_systems.yaml`

## Status

Schema **0.2.0** ([DATAP-684](https://dataparade.atlassian.net/browse/DATAP-684)): Discovery as sourced graph-fact assertion per [DATAP-681](https://dataparade.atlassian.net/browse/DATAP-681). Prior foundation: [DATAP-641](https://dataparade.atlassian.net/browse/DATAP-641), [DATAP-654](https://dataparade.atlassian.net/browse/DATAP-654), [DATAP-642](https://dataparade.atlassian.net/browse/DATAP-642). Epic [DATAP-680](https://dataparade.atlassian.net/browse/DATAP-680).
