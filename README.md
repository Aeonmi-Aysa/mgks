# MGKS Repository

This repository now contains a complete **MGKS text-first filesystem layout** for the `.mgk` / `.gen` formats, aligned to the v0.1 blueprint decisions dated **2026-04-12**.

## What is included

- Canonical directory layout under `data/mgks/`
- Production-ready policy notes (strict parser defaults, lenient authoring)
- Seed `.gen` templates for common glyph classes
- Seed `.mgk` stores for T2 episodic memory and T3 consensus memory
- Tier/global resolver indexes for cross-file entanglement resolution
- T1 snapshot policy (`--snapshot-t1`) with ephemeral metadata requirements

## Priority decisions encoded

1. **T1 memory-first** with optional debug snapshots.
2. **Strict vs lenient parser modes** (strict for CI/runtime, lenient for local authoring).
3. **Text-first maturity before `.mgkb`**.
4. **Promotion lineage for T2 → T3** while preserving identity unless remint is required.
5. **Scoped cross-tier references** with deterministic lookup order.

See `docs/mgks/ARCHITECTURE.md` for the full operational spec.
