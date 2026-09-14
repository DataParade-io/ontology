# DataParade ontology

Public **LinkML** schema, **taxonomy**, and **catalog** for DataParade architecture and privacy knowledge graphs (including C4 diagram projections).

Prefer the full word **vocabulary** in prose. The folder for controlled term sets is **`taxonomy/`**.

**LinkML** is the authoring format ([linkml.io](https://linkml.io/)). **OWL** (and SKOS for taxonomies) may be **generated** later — not how we author the schema.

## Layout

```text
schema/       # LinkML classes and slots
taxonomy/     # controlled vocabularies (enums / hierarchies)
catalog/      # public seed aliases
generated/    # JSON Schema, docs; later OWL/SKOS
```

## Status

Initial stub for [DATAP-655](https://dataparade.atlassian.net/browse/DATAP-655) under epic [DATAP-640](https://dataparade.atlassian.net/browse/DATAP-640).
