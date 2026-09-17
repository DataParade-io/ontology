# Changelog

## 0.3.0 — DATAP-696

**OCSF Architecture Discovery extension** — wire format for Discoveries in OCSF lake/interchange (OCSF base **1.7.0**).

### Added

- `ocsf/` — extension manifest (`extension/dataparade_discovery.json`), pins (`pin.yaml`), README (field table + Finding↔Discovery join rules)
- `generated/ocsf-discovery.schema.json` — JSON Schema for Architecture Discovery records (`class_uid` 900101)
- Architecture category `9001` / class `900101` — distinct from OCSF Finding category `2`

### Unchanged

- LinkML `Discovery` / `Finding` classes in `schema/core.yaml` (semantic model from 0.2.0)
- Taxonomy enums

## 0.2.0 — DATAP-684

**Discovery reshape** per [DATAP-681](https://dataparade.atlassian.net/browse/DATAP-681): sourced assertion of a graph fact (not scanner-only).

### Added

- `DiscoverySource` enum: `scan` | `cloud` | `interview` (immutable after create)
- Discovery fields: `asserted_at`, `asserts`, `asserted_slot`, `asserted_value`, interview review/evidence (`raw_evidence_ref`, `reviewer`, `reviewed_at`, `brief_sha`, `skill_sha`), `supersedes`
- `asserted_by` on `Evidenced` mixin (entity/edge → Discoveries)

### Changed

- `Discovery` description: sourced assertion of a graph fact; entities stay entities
- `Discovery.source` (via slot_usage): required immutable `DiscoverySource` (distinct from `Association.source` endpoints)
- Renamed `evidenced_by` → `asserted_by` on `Evidenced` (breaking)

### Unchanged

- `Finding` (OCSF) — distinct from Discovery
- No instance migration in this release

## 0.1.0

Foundation schema ([DATAP-641](https://dataparade.atlassian.net/browse/DATAP-641)).
