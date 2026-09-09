# analysis/ — derived tables

Rules for this folder:

- Everything here is produced by `../scripts/analyse.<ext>` from `../evidence/`
  only. The script makes **no network calls**. It is the single auditable hop
  between raw data and any figure quoted in the reports.
- Name files after the claim they support, not the source
  (`egress-daily-mb.csv`, not `api-response-7.csv`), so a `Source:` line in the
  report reads as an argument.
- First column is always the time key, named with its granularity and zone:
  `date_utc`, `hour_utc`, `minute_utc`. Timestamps in full ISO with `Z`.
- Units live in column names (`_mb`, `_tokens`, `_usd`).
- Keep zero columns when the zero is a finding (e.g. `client_errors` all zero).
- Minimise: emit counts and aggregates, not raw event bodies, when the raw
  data contains personal or sensitive detail.
- Normalise timezones programmatically (`astimezone(UTC)` or equivalent).
  Never slice a raw timestamp string.
