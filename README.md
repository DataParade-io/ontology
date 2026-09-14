# DataParade ontology

Public **LinkML** schema, **taxonomy**, and **catalog** for DataParade architecture and privacy knowledge graphs (including C4 diagram projections).

Instance knowledge, ingest, diagram generation, and customer-specific aliases stay in closed intelligence (Papyrus); this repo is the public contract.

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

Foundation on `main`: [DATAP-641](https://dataparade.atlassian.net/browse/DATAP-641) schema, [DATAP-654](https://dataparade.atlassian.net/browse/DATAP-654) taxonomy, [DATAP-642](https://dataparade.atlassian.net/browse/DATAP-642) catalog seed. Epic [DATAP-640](https://dataparade.atlassian.net/browse/DATAP-640).
