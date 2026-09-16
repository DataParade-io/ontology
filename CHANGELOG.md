# Changelog

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
