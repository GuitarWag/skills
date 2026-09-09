<!--
TEMPLATE — chain of custody. Delete these comments.
Per RFC 3227 §4 and ISO/IEC 27037 §6.1: record where, when and by whom evidence
was discovered, collected, handled, examined and stored; every custody
transfer; and restrict and log access. Self-attested hashes stored next to the
data are not custody — this document, kept current and counter-signed, is what
closes that gap.
-->

# <TICKET-ID> — Chain of Custody

<Classification line.>

Scope: the evidence package at `<location>`, hashed in `evidence/SHA256SUMS`.

## 1. Origin

| | |
|---|---|
| Discovered by | <who first identified the evidence sources, when> |
| Collected by | <examiner>, <YYYY-MM-DD HH:MM–HH:MM UTC> |
| Collection host | <machine, under whose control> |
| Original location | <the systems of record; note the provider retains the authoritative copies> |
| Preservation request | <made to whom, when, covering what — or "not made", with reason> |

## 2. Integrity anchors

| | |
|---|---|
| Digest file | `evidence/SHA256SUMS` (<n> artefacts) |
| Digest of digest file | `<sha256 of SHA256SUMS>` — recorded here, outside `evidence/` |
| Signature | <GPG key id / signer, date — or counter-signature by second person> |
| External deposit | <where a copy of the signed digest was lodged outside the examiner's control, and when> |

## 3. Custody log

Every person who has held the package, in order. No gaps.

| From (UTC) | To (UTC) | Custodian | Location / storage | Purpose |
|------------|----------|-----------|--------------------|---------|
| <datetime> | <datetime> | <name> | <encrypted volume / repo / safe> | Collection and examination |
| <datetime> | — | <name> | <storage> | <purpose> |

## 4. Transfers

| Date (UTC) | From | To | Method | Reference |
|------------|------|----|--------|-----------|
| <date> | <name> | <name> | <how it moved: repo grant, encrypted transfer, physical media + tracking number> | <ref> |

## 5. Access log

Access is restricted to the people listed here. Unauthorised access must be
detectable — say how (repo audit log, volume access log).

| Date (UTC) | Person | Access | Reason |
|------------|--------|--------|--------|
| <date> | <name> | read | <reason> |

## 6. Verification log

Who re-ran the hash check, when, and the result.

| Date (UTC) | Person | Command | Result |
|------------|--------|---------|--------|
| <date> | <name> | `(cd evidence && shasum -a 256 -c SHA256SUMS)` | <n>/<n> OK |

## 7. Retention and disposal

| | |
|---|---|
| Retention period | <how long, set by whom> |
| Review date | <YYYY-MM-DD> |
| Disposal | <method, authorisation required, to be recorded here when done> |
