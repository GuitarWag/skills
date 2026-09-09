# Runbook — from incident to forensic report

How to go from "something happened" to a forensic report package that a second
examiner could reproduce and a sceptical reader could challenge. Grounded in
NIST SP 800-86, RFC 3227, ISO/IEC 27037/27042/27043 and SWGDE 18-Q-002
(sources in `REFERENCES.md`, alongside this file). The package layout it
produces is in the `forensic-investigation` skill's `assets/template/`.

The process in one line: **preserve → collect → examine → analyse → report →
validate → publish**. Documentation and chain of custody run through every
step, not at the end.

---

## Step 0 — Before touching anything

1. Get the instruction in writing. Who is asking, what question they want
   answered, and what you are authorised to access. Record the exact sentence.
2. Decide the legal posture now, not later. If there is any chance of legal,
   insurance or disciplinary use, preserve to that standard from the first
   command. When unclear, preserve by default (NIST SP 800-86 §3.1.2).
3. Confirm you are in the right account context and that your access is
   read-only. Do not request elevation; request the specific read permissions
   you need.
4. Check retention clocks. List every data source you will need and how long
   it keeps records. Request preservation from the provider for anything close
   to expiry, before you do anything else.
5. Agree who else is acting. Responders contain; you collect. If containment
   is still running, coordinate so response actions are timestamped and logged
   — they become timeline rows. Agree the order too: anything a response
   action will destroy — live memory, volatile state, logs on a host due for
   rebuild, sessions killed by a credential reset — gets imaged or preserved
   first. Evidence preservation is a criterion of the containment strategy,
   not a casualty of it (CISA IR playbook 7a–7c; MITRE 11 Strategies,
   Strategy 5). Where response has already destroyed artefacts, record what
   was destroyed, when and by whom — the gap is itself a finding.
6. If a SOC alert or ticket started this, capture the detection as evidence:
   the alert payload, the rule or analytic that fired (with version), the
   triage notes and the case record. Detection data is incident data, and
   incident data is evidence (NIST SP 800-61r3 RS.AN-07; CISA IR playbook,
   preparation phase).

Done when: you can quote your authority, name your access level, no data
source expires before you can capture it, and responders know what must be
preserved before they eradicate.

## Step 1 — Set up the package

1. Copy the `forensic-investigation` skill's `assets/template/` to a working
   location named after the ticket.
2. Start `CHAIN-OF-CUSTODY.md` immediately: you are custodian number one.
3. Write your collection scripts before running them. Collection should be
   scripted, not improvised — decisions during collection are where mistakes
   happen (RFC 3227 §3).

Done when: the empty package exists and custody row one is filled in.

## Step 2 — Collect

Read-only. You are recording, not fixing. Nothing gets created, changed,
tagged, stopped or deleted.

1. Capture provenance first: your identity as seen by the system
   (`00-collector-identity`), collection start time (`00-collection-time`),
   exact tool versions.
2. Collect in order of volatility — the data that disappears first, first
   (RFC 3227 §2.1): live state and short-retention logs before configuration
   and archives.
3. Store raw responses unmodified. No filtering, no reformatting, no
   redaction at this layer.
4. Keep negative results. A query that returns zero events is evidence.
5. When in doubt, collect too much rather than too little.
6. Watch for silent truncation: set retries and page limits explicitly; label
   any capped capture as a SAMPLE in the manifest, with the window it truly
   covers.
7. Hash everything as soon as collection ends (`SHA256SUMS`), then sign the
   digest file or have a second person counter-sign it, and record the digest
   of the digest file in `CHAIN-OF-CUSTODY.md`. Hashes stored next to the
   data, self-attested, are not custody.
8. Note every step as you go: command, time, tool. Contemporaneous notes, not
   a reconstruction the next day (ISO/IEC 27042).

Done when: `evidence/` is populated, hashed, signed, catalogued in
`MANIFEST.md`, and the custody log shows an unbroken line from collection to
storage.

## Step 3 — Examine and analyse

Work from the evidence copies, never live systems and never the originals.

1. All arithmetic goes through one transform script (`scripts/analyse.*`) that
   makes no network calls. Every number in the report must trace:
   report figure → `analysis/` table → `evidence/` file.
2. Corroborate every claim from two independent sources where possible. Log
   the comparisons in METHODOLOGY §5 — including the disagreements. A
   disagreement is not a problem to hide; it is how errors get found.
3. For each hypothesis, actively try to disprove it, and give every plausible
   alternative the same treatment (NIST SP 800-86 §3.4). What you cannot
   exclude goes in Limitations, not in a footnote.
4. Handle time with care. Pin UTC at collection, convert programmatically,
   never trim timestamp strings, and show dual timezones side by side when a
   source records another offset.
5. It is a valid outcome to conclude that no conclusion can be drawn yet.

Done when: every intended finding has an evidence path, a corroboration row,
and a considered set of alternatives.

## Step 4 — Build the timeline

1. One row per event, every row cites its evidence file, every row labelled
   [F] fact / [A] assessment / [R] reported.
2. Group into phases. Bold the pivotal rows. Keep uneventful rows where the
   flat line is itself a finding.
3. Assessments go in blockquotes under the phase, with confidence, reasoning
   and what would falsify them — not mixed into the fact rows.

Done when: a reader can rebuild the story from the rows alone, and can tell at
a glance which rows are records and which are inference.

## Step 5 — Write the report

Fill the package's `REPORT.md`, `POSTMORTEM.md`, `INDICATORS.md`,
`RECOMMENDATIONS.md`, `METHODOLOGY.md`. The `forensic-report` skill carries the
writing and validation rules; a person runs it with `/forensic-report`. The
short version:

1. One finding per claim (F-01, F-02, …), each with: `Source:` line, the data,
   the reasoning, alternatives considered, consequence, what would change it,
   and a confidence label from the fixed vocabulary (METHODOLOGY §6).
2. Facts and opinion stay visibly separate. Results must be understandable by
   a layperson (SWGDE 18-Q-002 §5.4); mechanism detail goes under the plain
   statement, not instead of it.
3. Unknowns are stated as unknown. Never fill a gap with a plausible guess.
4. Write the Limitations section as load-bearing: scope, retention, sampling,
   attribution limits, hypotheses not excluded, deviations from procedure.
5. The postmortem is blameless and cites no evidence; the report proves, the
   postmortem teaches.

## Step 6 — Validate

Run the full checklist in the `forensic-report` skill's
`references/validation.md`. The gates that most often fail:

- A claim with no evidence path, or citing a glob when a specific file exists.
- Arithmetic that does not reproduce from the `analysis/` tables.
- A conclusion that quietly exceeds the Limitations section.
- Confidence labels missing or improvised.
- Revision numbers and correction counts inconsistent across documents.
- Hash check not re-run after the last evidence change.

Then get a second examiner to review from the documentation alone. The test is
repeatability: could they reach the same result without asking you anything
(ISO/IEC 27043)? Record their review and sign-off in the report front matter.

Done when: checklist passes, hashes verify, a named reviewer has signed.

## Step 7 — Publish and maintain

1. Classification line and handling rules on every document. Distribution
   recorded in `CHAIN-OF-CUSTODY.md` §5.
2. Corrections are never silent. Anything found wrong after release gets a
   C-entry in `CORRECTIONS.md` (quoted wrong text, cause, blast radius,
   lesson) and a new revision that references the old one (SWGDE 18-Q-002 §6).
3. Record evidence disposition: what is retained, where, until when, and who
   authorises disposal.

---

## Roles

| Role | Does | Does not |
|------|------|----------|
| Examiner | Collects, analyses, writes, owns the report's accuracy | Contain, remediate, or touch originals |
| Reviewer | Reproduces and challenges from the documentation alone | Rubber-stamp |
| Custodian | Keeps custody, access and verification logs current | Analyse |
| Responder | Contains and remediates, logs actions with times | Collect evidence unsupervised |

One person may hold several roles on a small incident. Say so in METHODOLOGY
§1 and §4 — self-attestation is a limitation to disclose, not to hide.
