# Forensic report validation checklist

Gate order matters: traceability first, because epistemic checks are
meaningless over claims that cannot be traced. A gate passes on evidence
(command output, resolved reference), never on the document's assertion.

## Gate 1 — Traceability

- [ ] Hash check runs clean: `(cd evidence && shasum -a 256 -c SHA256SUMS)`
- [ ] `SHA256SUMS` is signed or counter-signed; its own digest is recorded in
      `CHAIN-OF-CUSTODY.md` §2
- [ ] Transform script re-run regenerates `analysis/` byte-identical (or
      differences explained)
- [ ] Every finding has a `Source:` line pointing at files that exist
- [ ] Specific files cited where specific files exist (globs only for genuine
      file families)
- [ ] Key figures re-derived blind from `analysis/`/`evidence/` match the
      report (list each figure checked)
- [ ] Every timeline row cites evidence or is marked [R] with source
- [ ] Evidence manifest covers every file in `evidence/`; no unexplained
      ordinal gaps; samples labelled with cap and true window

## Gate 2 — Epistemics

- [ ] Every finding carries a confidence label from METHODOLOGY §6 vocabulary
      (no improvised wording)
- [ ] Confidence grades match corroboration: no "established fact" on a
      single uncorroborated tamperable source
- [ ] Every finding lists alternatives considered, and what excludes each or
      keeps it open
- [ ] Conclusions state support for an explanation relative to a named
      alternative; no transposed conditionals ("the probability that X did
      this is…")
- [ ] No claims of guilt, intent, or person-level identity beyond the records
      (credential ≠ person; user agent ≠ identity)
- [ ] No conclusion exceeds the Limitations section; read Limitations, then
      re-read the executive summary against it
- [ ] Unknowns stated as unknown, none silently filled
- [ ] Contradicting or exculpatory evidence is addressed in the text, not
      omitted
- [ ] Corroboration table (METHODOLOGY §5) includes the disagreements, and
      each disagreement is resolved or carried as a limitation

## Gate 3 — Completeness (SWGDE 18-Q-002 minimums)

- [ ] Report title, case identifier, page X of Y
- [ ] Requester, date of request, purpose and scope of the examination
- [ ] Authority for the examination quoted
- [ ] Items examined uniquely identified (including items received and not
      examined)
- [ ] Process described fully enough for another qualified examiner to
      evaluate what was done
- [ ] Results stated so a layperson can understand them
- [ ] Opinions labelled as opinions, each with its basis
- [ ] Deviations from standard procedure disclosed
- [ ] Evidence disposition stated (retained, returned, destroyed — where and
      until when)
- [ ] Report date and authorisation (name + signature) present
- [ ] Acronyms defined at first use

## Gate 4 — Consistency

- [ ] Revision number identical across every document in the package
- [ ] Correction count and correction references (C-0N) consistent everywhere
      they appear
- [ ] All F/Q/R/C/§ cross-references resolve to existing targets
- [ ] Closed questions struck through with reason, not deleted
- [ ] Canonical timezone declared in every time-bearing document; no silent
      conversions; dual offsets shown side by side where a source differs
- [ ] README "read in this order", layout tree and status table match the
      actual package contents

## Gate 5 — Handling and custody

- [ ] Classification line on every document, naming the sensitive classes
      actually present
- [ ] Handling note present (boundary, no-external-services rule)
- [ ] Named-individual rule honoured: false-positive framings travel with the
      name everywhere it appears
- [ ] `CHAIN-OF-CUSTODY.md` custody log has no gaps; access log current
- [ ] Verification log shows a hash check dated after the last evidence
      change
- [ ] Second-examiner review recorded, with the reviewer's independent
      reading documented before comparison (blind review)

## Gate 6 — Amendment discipline (packages past first release only)

- [ ] Every change since release has a CORRECTIONS.md entry: superseded text
      quoted, cause, severity, unchanged/changed split, lesson
- [ ] New revision references the one it supersedes; superseded revision
      noted in README and REPORT front matter

## Verdict

State one of:

- **Release** — all gates pass.
- **Fix first** — list failing items with file and location; no gate 1 or 2
  failures may be waived.
- **Re-examine** — a gate 1 or 2 failure undermines a finding itself; the
  affected finding goes back to analysis, and if the package was already
  released, the error becomes a CORRECTIONS.md entry now.
