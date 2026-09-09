<!--
TEMPLATE — package entry point. Fill every <placeholder>. Delete these comments.
This file is the front door: a reader who opens nothing else should leave with
the finding, the status, and the misreadings to avoid.
-->

# <TICKET-ID> — <short incident name>

**Forensic report package · Revision <N> · Account: <subject account> (<alias>)**

**Classification: <e.g. Internal — contains account IDs, IP addresses, usernames, cost data>**

> **Handling.** Keep this package inside <boundary>. Do not paste its contents
> into external services, including AI assistants. If any person is named here
> under a false-positive assessment, that framing must travel with the name in
> every summary made from this material.

<!-- If this revision supersedes an earlier one, say so here: what the earlier
revision concluded, why it was wrong, and link CORRECTIONS.md. Delete if rev 1. -->

## The finding in one paragraph

<One dense paragraph. What happened, over what window, at what cost or impact,
how it was contained, and what remains unknown. Bold the key numbers.>

## Read in this order

| # | Document | What it gives you |
|---|----------|-------------------|
| 0 | `POSTMORTEM.md` | The organisational read. **If you read nothing else, read this.** |
| 1 | `REPORT.md` | The findings, with evidence for each. |
| 2 | `TIMELINE.md` | Every event, timestamped and sourced. |
| 3 | `RECOMMENDATIONS.md` | What to do about it, with owners. |
| 4 | `INDICATORS.md` | Observables for detection and future responders. |
| 5 | `METHODOLOGY.md` | How the evidence was collected; limits of what it can support. |
| 6 | `CHAIN-OF-CUSTODY.md` | Who has held and verified the evidence, and when. |
| 7 | `CORRECTIONS.md` | Errors found in earlier revisions, recorded openly. |

## Layout

```
<package-root>/
├── README.md              this file
├── POSTMORTEM.md          blameless organisational postmortem
├── REPORT.md              primary forensic report (findings F-01..)
├── TIMELINE.md            master timeline, every row cites evidence
├── RECOMMENDATIONS.md     actions R1.., each with its evidence
├── INDICATORS.md          observables and detection content
├── METHODOLOGY.md         method, integrity, confidence language, limitations
├── CHAIN-OF-CUSTODY.md    custody log, access log, verification log
├── CORRECTIONS.md         errata register (C-01..), never silent edits
├── evidence/              raw, unmodified captures + MANIFEST.md + SHA256SUMS
├── analysis/              derived tables only; no network calls to produce them
└── scripts/               collect / analyse / manifest — one script per hop
```

## Reproducing this

```
<auth command>                 # read-only role, no elevation
./scripts/collect.sh           # raw captures into evidence/
./scripts/analyse.<ext>        # evidence/ -> analysis/  (no API calls)
./scripts/manifest.<ext>       # regenerates evidence/MANIFEST.md
(cd evidence && shasum -a 256 -c SHA256SUMS)
```

Run in this order. Collection must finish before analysis so every derived
number traces to a hashed capture.

## What was and was not done

**Done:** <read-only collection of X, Y, Z; corroboration of each finding from two sources.>

**Not done:** <no configuration changes, no credential operations, no deletions — see METHODOLOGY §2.>

**Could not be done:** <what the evidence cannot support — see METHODOLOGY §7.>

## The three things most likely to be acted on wrongly

<!-- Name the misreadings you expect a reader to make. Each gets the
counter-evidence and a section reference. This section prevents bad decisions
made from a skim. -->

1. <Likely misreading.> <Why it is wrong, with the evidence and §-reference.>
2. <...>
3. <...>

## Status

| | |
|---|---|
| Impact | <quantified / estimated / unknown> |
| Vector | <confirmed / assessed / unknown> |
| Containment | <complete / partial / not needed> |
| Attribution | <established / partial / not established> |
| Open questions | <count, see REPORT §Unresolved questions> |

---

Related: <ticket link> · Examiner: <name> · Revision <N>, <YYYY-MM-DD>
