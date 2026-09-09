# scripts/ — one script per hop

The package is regenerable in three hops. Each hop is one named script; nothing
happens between hops by hand.

| Script | Hop | Network |
|--------|-----|---------|
| `collect.sh` | live systems → `evidence/` | Read-only API calls only |
| `analyse.<ext>` | `evidence/` → `analysis/` | **None** |
| `manifest.<ext>` | `evidence/` + `SHA256SUMS` + description map → `evidence/MANIFEST.md` | **None** |

Rules for `collect.sh`:

- Pin the timezone: `export TZ=UTC`.
- Echo a step label per collection ordinal so the console log matches the
  `NN-` file prefixes.
- Set retry/backoff explicitly and comment why — throttled APIs can truncate
  results silently without it.
- Record identity first (`00-collector-identity`), collection start time
  (`00-collection-time`), and exact tool versions.
- Capture negative results too. A zero-event response is evidence.
- Hash everything at the end and write `SHA256SUMS`; then sign it (see
  `../CHAIN-OF-CUSTODY.md` §2).

Rules for `analyse.<ext>`:

- No API calls. State it in a comment at the top.
- All arithmetic for the report lives here, in one file, auditable.
- Emit counts/aggregates rather than raw bodies where the raw data is
  sensitive.
- Normalise time via timezone-aware conversion; never slice timestamp strings.
