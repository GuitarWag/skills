<!--
TEMPLATE — evidence manifest. Delete these comments.
Generate this file with scripts/manifest.<ext> from the directory listing plus
SHA256SUMS plus a description map — do not maintain it by hand.

File naming: NN[b]-<source>-<subject>[-<region>].<ext>
  NN   two-digit collection-step ordinal (00 = provenance, then investigative order)
  b    variant capture of the same subject at a different scope (e.g. capped sample)
  ext  .json single response · .jsonl paginated sweep, one event per line · .txt CLI output
If a collection step is dropped, keep the ordinal and record why — no silent gaps.
-->

# Evidence Manifest — <TICKET-ID>

<Classification line.>

**Provenance.** Collected <YYYY-MM-DD> by <examiner identity / email> under
<named read-only role>, subject <account/system>. Every call was read-only
(<e.g. `Get*`, `List*`, `Describe*`, `LookupEvents`>). Collector identity and
collection time are evidence items `00-*`. Tool versions: <exact versions>.

**Integrity.** No file has been filtered, reformatted or redacted. Derived
tables live in `../analysis/`, produced by `../scripts/analyse.<ext>`, which
makes no API calls. Verify:

```
shasum -a 256 -c SHA256SUMS
```

`SHA256SUMS` covers every artefact except itself; its own digest and signature
are recorded in `../CHAIN-OF-CUSTODY.md` §2.

> Digests alone are not a chain of custody. Custody, access and verification
> history: `../CHAIN-OF-CUSTODY.md`.

**<N> artefacts · <size>**

## Inventory

Descriptions name the call, the query window, the per-item collection time,
and the report section the file supports. Label the special cases in caps:
SAMPLE (with the cap and the window it truly covers, and which findings may
not rest on it), ZERO EVENTS (negative results are evidence), AUTHORITATIVE,
COMPLETE.

| Artefact | Size (bytes) | Collected (UTC) | Description |
|----------|--------------|------------------|-------------|
| `00-collector-identity.json` | <n> | <time> | Identity and access level used for every call. |
| `00-collection-time.txt` | <n> | <time> | Collection window start/end. |
| `01-<source>-<subject>.json` | <n> | <time> | <call, window>. Basis of REPORT §<n>. |

## SHA-256

| Artefact | Digest |
|----------|--------|
| `<file>` | `<64-hex>` |
