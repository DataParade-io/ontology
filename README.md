# DataParade ontology

Public **LinkML** schema, **taxonomy**, and **catalog** for DataParade architecture and privacy knowledge graphs (including C4 diagram projections).

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

## Status

[DATAP-641](https://dataparade.atlassian.net/browse/DATAP-641) schema and [DATAP-654](https://dataparade.atlassian.net/browse/DATAP-654) taxonomy seeds. Epic [DATAP-640](https://dataparade.atlassian.net/browse/DATAP-640).
