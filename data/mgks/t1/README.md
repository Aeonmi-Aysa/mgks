# T1 Tier Policy

T1 is ephemeral by default and should remain in process memory.

## Optional snapshot mode

Use `--snapshot-t1` only for debugging, postmortems, or reproducibility.

Snapshot path format:

`data/mgks/t1/<timestamp>_session-<id>.t1.mgk`

Required metadata in snapshot header/body:
- `ephemeral: true`
- `ttl: <short_duration>`
