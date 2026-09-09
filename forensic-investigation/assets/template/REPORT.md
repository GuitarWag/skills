<!--
TEMPLATE — primary forensic report. Fill every <placeholder>. Delete these comments.

Rules that make this document defensible:
- Every claim cites an evidence or analysis file by relative path.
- Every finding carries a confidence label from METHODOLOGY §6.
- Show your arithmetic inline so a reader can redo it.
- State what would change each conclusion.
- Facts and interpretation are visibly separate. A layperson must be able to
  follow the results (SWGDE 18-Q-002 §5.4).
-->

# <TICKET-ID> — <incident name>: Forensic Report

<Classification line — same as README.>

| | |
|---|---|
| Incident | <ticket link and priority> |
| Subject | <account / system / scope examined> |
| Requested by | <name, organisation, date of request> |
| Authority | <what authorised this examination: ticket, engagement letter, manager instruction — quote the scope sentence> |
| Examiner | <name> |
| Examiner access | <named role or permission set; read-only; no elevation sought or used> |
| Evidence collected | <YYYY-MM-DD, and why re-collected if applicable> |
| Report date | <YYYY-MM-DD — date of the final signed version> |
| Revision | <N; if >1, what superseded and pointer to CORRECTIONS.md> |
| Status | <one sentence: what is settled, what is not> |

All times are UTC.

<!-- Revision-supersession blockquote here if this is not revision 1. -->

## 1. Executive summary

<Plain language, no jargon, for senior readers. What happened, the impact in
numbers, how confident you are, what remains open. Half a page at most.>

## 2. Scope, authorisation and constraints

<What you were asked to establish, by whom, under what authority. What was in
scope and out of scope. Constraints that shaped the work: retention windows,
access limits, time pressure. Anything considered and rejected, with the reason.>

## 3. Finding F-01 — <the claim, written as one plain assertion>

Source: `evidence/<file>`, `analysis/<file>`

<Data table. Right-align numeric columns.>

- <What the data shows, at mechanism level.>
- <Arithmetic shown inline: "A ÷ B = C".>
- <The comparison that discriminates this explanation from the alternatives.>

**Alternatives considered.** <Each plausible alternative explanation, and the
evidence that excludes it or the reason it stays open. NIST SP 800-86 §3.4:
prove or disprove each one methodically.>

**Consequence.** <One paragraph: what this finding means operationally.>

**What would change this.** <The observation that would overturn or weaken it.>

*Confidence: <established fact | assessment, low/moderate/high | reported | unknown> (METHODOLOGY §6).*

---

## 4. Finding F-02 — <...>

<Repeat the same anatomy for each finding. One finding per claim; do not bundle.>

---

## <N>. Reconstruction

<The narrative that the findings jointly support, in time order. Only claims
already established above; cite findings as (F-01), not new evidence.>

## <N+1>. Unresolved questions

| | Question | Status |
|---|----------|--------|
| Q1 | <question> | Open — <priority or reason it may be unanswerable> |
| Q2 | ~~<answered question>~~ | Answered — see §<n> / Void — <reason> |

Closed questions are struck through, never deleted.

## <N+2>. Recommendations

See `RECOMMENDATIONS.md`. <One line per critical item here at most.>

## <N+3>. Evidence disposition

<Where the originals and working copies are, retention period, and what will
happen to them (retained / returned / destroyed, and when).>

## <N+4>. Appendices

| Path | Contents |
|------|----------|
| `evidence/` | <n> raw captures, hashed; see `evidence/MANIFEST.md` |
| `analysis/` | <n> derived tables |
| `METHODOLOGY.md` | Method, integrity, confidence language, limitations |
| `CHAIN-OF-CUSTODY.md` | Custody, access and verification logs |
| `CORRECTIONS.md` | Record of corrections |

---

Authorised by: <name, role> · Signature: <handwritten, digital or electronic> · <YYYY-MM-DD> · Page <n> of <total>
