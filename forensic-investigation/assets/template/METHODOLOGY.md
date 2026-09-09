<!--
TEMPLATE — methodology, evidence handling and limitations. Delete these comments.
Purpose test: a second examiner must be able to reproduce the result
independently from this document, or challenge it (ISO/IEC 27042 §5;
ISO/IEC 27043: repeatability is a basic principle of digital investigations).
-->

# <TICKET-ID> — Methodology, Evidence Handling and Limitations

<Classification line.>

This document exists so that a second examiner can reproduce the result
independently, or challenge it.

## 1. Examiner and authority

| | |
|---|---|
| Examiner | <name, role, relevant competence: certifications, years, prior examinations> |
| Independence | <declared conflicts of interest, or "none"> |
| Principal | <full identity used for collection, e.g. ARN> |
| Access | <named permission set; read-only; no elevation was sought or used> |
| Instruction | "<verbatim scope-of-authority sentence, and who gave it>" |
| Collection host | <machine, OS version, tool versions: CLI, runtime, libraries> |
| Collection window | <start and end, UTC — see `evidence/00-collection-time.txt`> |

Collector identity is captured as evidence item `00-collector-identity.*` so the
access level behind every subsequent call is on the record.

## 2. Read-only guarantee

| Service / system | Operations used |
|------------------|-----------------|
| <service> | <exact list of read operations issued> |

**Explicitly not done:** <create, modify, delete, tag, start, stop; credential
operations; policy edits; snapshots initiated by the examiner; writes to any
repository; posts to external services.>

<If a capability was considered and rejected, name it and give the reason.>

## 3. Collection

```
scripts/collect.sh        all raw captures -> evidence/     (read-only API calls)
scripts/analyse.<ext>     evidence/ -> analysis/            (NO API CALLS)
scripts/manifest.<ext>    regenerates evidence/MANIFEST.md  (NO API CALLS)
```

<Collection order and why. Order of volatility: most volatile first (RFC 3227
§2.1). Retry and throttling settings, and what silent truncation they prevent.
Timezone pinned to UTC at collection.>

Raw responses are stored unmodified: no filtering, no reformatting, no
redaction. All arithmetic lives in one transform script that can be audited.
Negative results (zero-event captures) are stored as evidence, not omitted.

## 4. Evidence integrity and custody

Hashes: `evidence/SHA256SUMS`, covering every artefact including the analysis
tables and this package's documents at time of issue. Verify:

```
(cd evidence && shasum -a 256 -c SHA256SUMS)
```

The digest file is signed: <how — GPG signature, counter-signature by a second
person, or external deposit — and where the signature lives>.

Custody, access and verification history are in `CHAIN-OF-CUSTODY.md`. <If any
part of custody is self-attested (collector, hasher and custodian are the same
person), say so plainly here and state the remediation taken or still owed.>

<Name the upstream systems that retain the authoritative records, and whether a
preservation request was made before retention windows close.>

## 5. Corroboration

Every finding rests on at least two independent sources where possible.
Disagreements are listed, not hidden — they are how errors get found.

| Claim | Source A | Source B | Result |
|-------|----------|----------|--------|
| <claim> | `<file>` | `<file>` | Agree / Disagree — <what the disagreement revealed> |

## 6. Confidence language

Used throughout the package. Every finding carries one of these labels.

| Marker | Meaning |
|--------|---------|
| **Established fact** | Directly recorded in a raw capture in `evidence/`; reproducible by re-running the query. |
| **Assessment (low / moderate / high)** | Inference. The reasoning is stated so it can be challenged, and the finding names what would change it. |
| **Reported** | Sourced from the ticket or a third party; not independently verified inside the examined scope. |
| **Unknown** | Stated as unknown. Not filled with a plausible guess. |

## 7. Limitations — what this examination cannot support

These are load-bearing. Any conclusion beyond them is not carried by this
evidence.

1. **<Scope boundary.>** <e.g. single account examined; adjacent accounts not examined.>
2. **<Attribution limit.>** <e.g. source identity behind credential X not established.>
3. **<Visibility limit.>** <e.g. no payload or content visibility in these logs.>
4. **<Retention boundary.>** <per data source: what window each source still held.>
5. **<Sampling.>** <which capture is a sample, what cap produced it, which findings do and do not rest on it.>
6. **<Hypotheses not excluded.>** <the alternative that could not be ruled out, and why.>
7. **<Tooling limits.>** <what the tools could not enumerate; known tool limitations.>
8. **<Deviations.>** <any deviation from this methodology or from standard procedure, what was done instead, and its effect (SWGDE: deviations must be disclosed).>

## 8. Handling

<What sensitive classes this material contains. Where it may live. Who may see
it. The named-individual rule: any false-positive framing travels with the
name. Redaction instructions for sharing outside the boundary.>
