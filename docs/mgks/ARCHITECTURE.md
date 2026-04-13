# MGKS Architecture Spec (Text-First)

Version: 0.1  
Date: 2026-04-12

## 1) Directory contract

```text
data/mgks/
├── genesis/            # .gen template schemas
├── t1/                 # ephemeral tier notes + optional snapshots only
├── t2/                 # episodic stores (.t2.mgk)
├── t3/                 # consensus stores (.t3.mgk)
├── archive/            # append-only decayed stores
└── index/              # tier + global resolver indexes
```

## 2) Tier behavior

### T1
- Default: in-memory only.
- Optional debug snapshots: `--snapshot-t1` writes
  `data/mgks/t1/<timestamp>_session-<id>.t1.mgk`.
- Snapshot metadata requirements:
  - `ephemeral: true`
  - `ttl: <duration>` (short retention)

### T2
- Episodic truth candidates (superposition, entanglement, early evidence).
- Default decay: `7d`.

### T3
- Consensus memory after collapse + evidence thresholds.
- Promotion policy:
  - Preserve source `id` when promoted directly.
  - Record lineage (`promoted_from_tier`, `promoted_from_store`, `promoted_at`).
  - For semantic merges, mint new id + include `aliases` of contributing source ids.

## 3) Parser modes

### Strict mode (default for CI/runtime)
- Reject if any amplitude is outside `0.0..1.0`.
- Reject if `Σα > 1.0 + 1e-6`.
- Treat unresolved references as hard errors.

### Lenient mode (default for local authoring)
- Keep amplitude bounds enforcement (`0.0..1.0`).
- Allow `Σα > 1.0 + 1e-6` with warnings.
- Emit normalization hints.
- Keep unresolved references as soft errors/warnings.

## 4) Cross-file entanglement

Scoped reference format:

```text
|Bell⟩ ↔ t3::consensus_graph::proceed_with_api_launch_staged
```

Resolver order:
1. Same file
2. Same-tier index
3. Global cross-tier index

## 5) Performance profile (text format stage)

To optimize text `.mgk` performance prior to `.mgkb`:

1. **Canonicalization pipeline**
   - Stable field ordering
   - Sorted glyph labels
   - Deterministic float precision for `conf`, `α`, and `weight`

2. **Incremental index refresh**
   - Update tier/global indexes on write
   - Avoid full-store scans during lookup

3. **Hashing strategy (Stage 2.5)**
   - Canonical store hash for change detection
   - Per-glyph hash for targeted cache invalidation

4. **Strict runtime / lenient editing split**
   - Keeps production integrity while preserving authoring speed

## 6) Binary roadmap

- Stage 2: `.mgk` + `.gen` parser/validator/resolver
- Stage 2.5: canonicalization + deterministic hashing
- Stage 3: `.mgkb` with guaranteed lossless round-trip to canonical `.mgk`
