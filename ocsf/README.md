# DataParade OCSF extension — Architecture Discovery

**Ticket:** [DATAP-696](https://dataparade.atlassian.net/browse/DATAP-696) · **Epic:** [DATAP-680](https://dataparade.atlassian.net/browse/DATAP-680)  
**LinkML pin:** ontology `0.3.0` (conceptual model in `schema/core.yaml`)  
**OCSF base pin:** **1.7.0** ([Findings category reference](https://schema.ocsf.io/1.7.0/categories/findings))

## Purpose

**Discoveries** are architecture/privacy **graph-fact assertions** serialized as **OCSF-shaped records** via this extension so they can live in the same lake/interchange family as OCSF **Findings** (security events) and be joined at query time.

| Record kind | OCSF category | `class_uid` | Role |
| --- | --- | --- | --- |
| **Architecture Discovery** (this extension) | Architecture (`9001`) | `900101` | Sourced graph-fact assertion (`scan` \| `cloud` \| `interview`) |
| **Finding** (OCSF native) | Findings (`2`) | `2002`–`2008`, … | Security-event / posture observation |

**Discovery ≠ Finding.** Same interchange envelope; different class/category and semantics.

## Extension identity

| Field | Value |
| --- | --- |
| Extension name | `dataparade_discovery` |
| Extension version | `1.0.0` |
| Profile | `architecture_privacy` |
| Record schema | `generated/ocsf-discovery.schema.json` |

## Architecture Discovery — field table

Wire record = OCSF envelope + `dataparade` extension object (validated by `ocsf-discovery.schema.json`).

### OCSF envelope (required)

| Field | Type | Rule |
| --- | --- | --- |
| `class_name` | string | `"Architecture Discovery"` |
| `class_uid` | integer | `900101` |
| `category_name` | string | `"Architecture"` |
| `category_uid` | integer | `9001` |
| `activity_id` | integer | `1` (Create) |
| `activity_name` | string | `"Create"` |
| `type_uid` | integer | `90010101` |
| `time` | integer | Unix seconds — mirrors `dataparade.asserted_at` |
| `metadata.version` | string | **`"1.7.0"`** (OCSF base pin) |
| `metadata.extension.name` | string | `"dataparade_discovery"` |
| `metadata.extension.version` | string | `"1.0.0"` |
| `metadata.uid` | string | Discovery id (CURIE/URI) |

### `dataparade` extension object (required)

Aligns 1:1 with LinkML `Discovery` (`schema/core.yaml`).

| Field | Required | Rule |
| --- | --- | --- |
| `record_kind` | yes | `"discovery"` |
| `ontology_version` | yes | LinkML ontology version (e.g. `0.3.0`) |
| `source` | yes | `scan` \| `cloud` \| `interview` — **immutable** after create |
| `asserted_at` | yes | ISO-8601 datetime |
| `asserts` | yes | URI of asserted entity/association (`dp:…`) |
| `asserted_slot` | when slot fill | e.g. `actor_kind`, `data_categories`, `purpose`, `in_scope` |
| `asserted_value` | when `asserted_slot` | Ontology-shaped value (enum token or JSON list string) |
| `eligible_shape` | interview A0 | `D2` \| `D4` \| `D7` \| `D8` when from interview land |
| `raw_evidence_ref` | interview land | Unedited transcript/notes pointer |
| `reviewer` | interview land | Human id |
| `reviewed_at` | with reviewer | ISO-8601 datetime |
| `brief_sha` | interview land | Brief pin SHA |
| `skill_sha` | interview land | Skill pin SHA |
| `supersedes` | no | Prior Discovery id |
| `related_resource_refs` | no | Join hints for Finding↔Discovery (ARNs, `cmp_*`, `flow_*`) |

## Finding ↔ Discovery join rules

1. **Primary (resource identity):** OCSF Finding `resources[].uid` (ARN or stable id) resolves to graph entity URI (`dp:scan/entity/cmp_*`, `flow_*`, deployed resource) via entity-resolution / catalog. Match Discoveries where `asserts` equals or subsumes that entity URI.
2. **Secondary (explicit back-link):** Finding may carry `unmapped.dataparade.related_discovery_ids[]` (optional). Discovery may carry `related_resource_refs[]` (optional). Either direction is valid; at least one side required for automated fusion — never invent joins.
3. **Scan wins:** When `source=scan` Discovery and `source=interview` Discovery conflict on the same `asserts` + `asserted_slot`, **scan-backed identity wins**; interview records do not overwrite — escalate or `supersedes` with human ticket.
4. **Distinct classes:** Never map a Finding `class_uid` in category `2` to a Discovery record. Never emit Discovery `class_uid` `900101` for security events.

## Store / interchange

| Store | Role |
| --- | --- |
| **Authoritative** | One JSON file per Discovery: `{graph_root}/ocsf-discoveries/{id-slug}.json` (lake / repo JSON — not wiki markdown) |
| **Interim scratch** | `knowledge-base/project/wiki/graph/dogfood/` markdown + evidence — **deprecated** as product KG; re-emit into `ocsf-discoveries/` |
| **Conceptual** | LinkML `Discovery` in `schema/core.yaml` |

## Validation

```bash
# After Phase B land tooling — example
node ../dataparade-cli/tests/eval/interview-a0/bin/validate-ocsf-discovery.mjs path/to/record.json
```

CI: `validate.yml` checks `generated/ocsf-discovery.schema.json` exists and is valid JSON Schema.

## See also

- [DPKB design note](https://github.com/DataParade-io/knowledge-base/blob/main/project/wiki/ocsf-discovery-extension.md)
- `extension/dataparade_discovery.json` — extension manifest
- `pin.yaml` — version pins
