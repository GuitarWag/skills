# The forensic process, and the person running it

Two things decide whether a forensic investigation holds up: the process, and
the conduct of the investigator. This document describes both. The
step-by-step procedure is `RUNBOOK.md`; the sources behind every claim here
are in `REFERENCES.md`.

## Part 1 — The process

### The shape

```
prepare → preserve → collect → examine → analyse → report → review → close
─────────────────────────────────────────────────────────────────────────
documentation and chain of custody run underneath every phase, continuously
```

This follows NIST SP 800-86 (collect, examine, analyse, report) and ISO/IEC
27043, which adds readiness before the incident and treats documentation,
authorisation and custody as continuous processes rather than steps. The exact
model matters less than picking one and following it the same way every time.

### What each phase is for

**Prepare.** Authority in writing, scope agreed, legal posture decided,
retention clocks checked. Most investigations that fail are lost here, before
any evidence is touched.

**Preserve and collect.** Get the data before it disappears, without changing
it, in a way you can prove. Most volatile first. Raw and unmodified. Hashed
and signed at capture. Custody logged from the first minute.

**Examine and analyse.** Turn data into answers to the questions that started
the investigation, using methods someone else could repeat. Every number
traces back to a raw capture through one auditable transform. Every hypothesis
gets an honest attempt at disproof.

**Report.** Say what the evidence supports, how strongly, and where it stops.
Facts sit apart from interpretation. Unknowns stay unknown.

**Review.** A second examiner works from the documentation alone and checks
whether they reach the same result. The review is blind: the reviewer forms
their own reading of the evidence before seeing the first examiner's
conclusions, because knowing the expected answer measurably changes what
people find (Dror & Charlton 2006; Sunde & Dror 2021).

**Close.** Disposition of evidence recorded, retention set, lessons captured.
Anything found wrong after release becomes a correction entry and a new
revision. Never a silent edit.

### Where this sits in incident response

When the investigation is part of a live incident, the forensic process runs
inside the incident response lifecycle: preparation → detection & analysis →
containment, eradication & recovery → post-incident activity (NIST SP 800-61;
the same phases appear in the CISA response playbooks, and as PICERL in the
SANS handbook). NIST SP 800-61r3 (2025) recasts these as CSF 2.0 functions —
Govern/Identify/Protect prepare, Detect/Respond/Recover handle — with lessons
fed back continuously instead of waiting for closure. Three consequences for
the examiner:

**The SOC's output is your input — and it is evidence.** Detection usually
arrives as a SOC alert that has been triaged and escalated (MITRE 11
Strategies, Table 1). The alert payload, the rule or analytic that fired and
its version, the triage notes and the case record are the investigation's
first evidence items, not background reading. NIST SP 800-61r3 is explicit
that collected incident data is evidence even when formal custody procedures
are not in play.

**Containment competes with preservation.** Rebuilding a host, resetting
credentials or killing processes destroys the artefacts you have not yet
captured (MITRE 11 Strategies, Strategy 5). Evidence preservation is a stated
criterion when the containment strategy is chosen, and preservation — imaging,
backups — comes before eradication (CISA playbook, steps 7a–7c). This is why
the runbook has the examiner agree the containment order with responders
before collection starts, and why response actions are timestamped into the
timeline.

**Decide the grade of forensics at the start.** A SOC doing IR-grade forensics
answers "what did the adversary do" so response can proceed; legal-grade
forensics supports proceedings and demands stricter handling throughout (MITRE
11 Strategies §11.7). NIST SP 800-61r3 notes most incidents never see formal
custody procedures — but the possibility of prosecution is a factor to weigh
when collecting and retaining. When the grade is uncertain, handle to the
higher one from the first command; that decision cannot be retrofitted.

### What makes evidence defensible

ISO/IEC 27037 names four properties. In plain words:

| Property | Plain meaning |
|----------|---------------|
| Auditability | Every action is on the record: who, what, when, with which tool. |
| Repeatability | The same person, same method, same data gets the same result. |
| Reproducibility | A different competent person gets the same result from the documentation alone. |
| Justifiability | You can defend why you chose each method. |

RFC 3227 adds the court's view: evidence must be admissible, authentic,
complete (the whole story, not one side's), reliable in how it was handled,
and believable to a non-specialist.

### Why the package has three layers

```
evidence/  raw, unmodified, hashed     ← what happened
analysis/  derived by one script,      ← the arithmetic
           no network calls
*.md       interpretation              ← what it means
```

Each layer regenerates from the one below. A sceptical reader can start at any
claim and walk down to a hashed raw capture. This is reproducibility made
mechanical rather than promised.

### Known limits of digital evidence

Honest reports disclose these even when nobody asks (NIST IR 8354):

- Not all relevant evidence may have been found. Two competent examiners
  searching the same data can find different subsets.
- Recovered or derived data can include extraneous material.
- The meaning of an artefact can change between software versions.
- Tools have blind spots and are rarely formally peer reviewed; tool output is
  input to the examiner's reasoning, never the conclusion itself.
- Digital errors are mostly systematic rather than random, so explain how
  errors were looked for and mitigated instead of quoting a single error rate.
- A capable adversary may have staged or altered the scene. Certainty comes
  from agreement between independent, tamper-resistant sources, never from one
  log file.

## Part 2 — The investigator

### The four principles (after ACPO)

1. Change no data that the investigation may rely on.
2. If you must touch original data, be competent to do it and able to explain
   exactly what you did and what it changed.
3. Keep an audit trail complete enough that an independent third party could
   repeat the process and reach the same result.
4. One named person carries overall responsibility for the investigation
   staying within these principles and the law.

### Bias is a working condition, not a character flaw

The research is blunt: honest, competent, experienced experts change their
conclusions when given irrelevant context. Fingerprint experts contradicted
their own earlier findings after hearing "the suspect confessed" (Dror,
Charlton & Péron 2006). Digital examiners given the same disk with different
cover stories found and reported different traces (Sunde & Dror 2021).

Dror (2020) lists the beliefs that stop people from protecting themselves.
The short version: bias is not an ethics problem, does not only affect bad
examiners, is not cured by expertise or by tools, is easier to see in others
than in yourself, and cannot be willed away. Protection comes from procedure.

### Habits that protect the work

**Look at the evidence before the theory.** Examine and document what the data
shows before reading who is suspected, what the ticket concludes, or what a
colleague thinks happened. Record your initial reading; after seeing the
context, changes to it are allowed only openly and with a reason. This is
Linear Sequential Unmasking (Dror et al. 2015, 2021), and it works as well for
a CloudTrail sweep as for a fingerprint.

**Write your hypotheses down before examining, then attack them.** State the
competing explanations first and spend your effort trying to disprove the one
you favour. If the results arrived before the hypotheses did, ask someone who
has not seen the results to frame them.

**Keep task-irrelevant context out.** You do not need to know that a person is
disliked, or was already blamed, to read a log. If someone else scopes your
task, ask them to pass you what the analysis needs and hold back the rest.

**Weigh each source by how hard it is to fake.** One uncorroborated,
tamperable source supports at most a weak claim, whatever it seems to show.
Confidence rises with agreement between independent sources on systems an
attacker would have had to compromise separately (Casey 2002). Always ask what
a deliberate adversary could have staged.

**Give the other explanation equal work.** Evaluate the evidence under the
innocent explanation with the same rigour as under the incriminating one.
Record every trace you considered, including the ones that cut against your
conclusion. The report must tell the whole story, and evidence that
contradicts a working theory is a finding, never an inconvenience.

**Phrase conclusions carefully.** Say how strongly the findings support one
explanation over the stated alternative. Do not flip it into the probability
that the explanation is true, and do not let "weak support for X" read as
support for anything else (ENFSI 2015). No claims about guilt or intent. No
conclusions outside your own competence.

**Prefer "unknown" to a plausible guess.** Filling gaps feels helpful and
produces corrections later. A stated unknown is a finding; a guess is a
defect.

**Know when to stop.** When no alternative explanation can even be formulated,
describe the findings without evaluating them, and say why. When the evidence
cannot separate the hypotheses, report exactly that. "No conclusion can be
drawn yet" is a legitimate professional result (NIST SP 800-86).

**Write as you go, sign what you write.** Notes made at the time, with
timestamps and timezone, signed. You may need to explain an action years later
under challenge; technically sound work has been thrown out on documentation
alone.

**Invite the challenge.** Hand the package to a reviewer without your
conclusions attached. If they cannot reproduce your result from the
documentation, the documentation is the defect, whatever the analysis was
worth. Review works best attached to each phase of the investigation rather
than as one signature at the end (Sunde & Horsman 2021).

**Be wrong in public.** When a conclusion falls, record what the superseded
text said, what caused the error, what survives, and the lesson. A visible
corrections register is what makes the surviving findings believable.
