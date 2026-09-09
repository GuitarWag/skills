# References

The sources behind `RUNBOOK.md`, `PROCESS.md`, the templates and the skills.
Grouped by what to use them for. Verified September 2026.

## Standards and official guidance

- **NIST SP 800-86** — Guide to Integrating Forensic Techniques into Incident
  Response (2006). The four-phase process (collect, examine, analyse, report),
  chain-of-custody requirements, and the rule that every plausible alternative
  explanation gets methodical treatment.
  https://csrc.nist.gov/pubs/sp/800/86/final
- **RFC 3227** — Guidelines for Evidence Collection and Archiving (2002).
  Order of volatility, "collection first, analysis later", the five legal
  criteria (admissible, authentic, complete, reliable, believable), custody
  documentation list.
  https://www.rfc-editor.org/rfc/rfc3227
- **ISO/IEC 27037:2012** — Identification, collection, acquisition and
  preservation of digital evidence. The four defensibility properties:
  auditability, repeatability, reproducibility, justifiability.
  https://www.iso.org/standard/44381.html
- **ISO/IEC 27042:2015** — Analysis and interpretation of digital evidence.
  Contemporaneous notes, uncertainty treatment, suggested report content,
  competence and proficiency.
  https://www.iso.org/standard/44406.html
- **ISO/IEC 27043:2015** — Investigation principles and processes. Readiness
  before the incident; documentation, authorisation and custody as continuous
  processes; repeatability as the basic principle.
  https://www.iso.org/standard/44407.html
- **NIST SP 800-61r3** — Incident Response Recommendations (2025). Where
  forensics sits in incident handling; records integrity and provenance
  (RS.AN-06/07); "collected incident data is still considered evidence" even
  without formal custody procedures. Reframes the old four-phase lifecycle as
  CSF 2.0 functions: Govern/Identify/Protect prepare, Detect/Respond/Recover
  handle, lessons feed back continuously (ID.IM) rather than only at closure.
  https://csrc.nist.gov/pubs/sp/800/61/r3/final
- **SWGDE 18-Q-002** — Requirements for Report Writing in Digital and
  Multimedia Forensics (2018). The minimum report elements (Gate 3 of the
  validation checklist) and the amendment rule: post-release edits identified
  and explained, never silent.
  https://www.swgde.org/documents/published-complete-listing/18-q-002-swgde-requirements-for-report-writing-in-digital-and-multimedia-forensics/
- **SWGDE 18-F-001 v2.0** — Best Practices for Computer Forensic Examinations
  (2025). Write blockers, work on copies, workstation isolation, deviation
  disclosure, "sound, supported by the data, replicable, and defensible".
  https://www.swgde.org/documents/published-complete-listing/18-f-001-2/
- **ACPO Good Practice Guide for Digital Evidence v5** (2012). The four
  principles in PROCESS.md Part 2. Still the de facto UK standard.
  https://www.digital-detective.net/digital-forensics-documents/ACPO_Good_Practice_Guide_for_Digital_Evidence_v5.pdf
- **ENFSI Guideline for Evaluative Reporting in Forensic Science** (2015).
  Balance, logic, robustness, transparency; propositions set before
  examination; the transposed-conditional prohibition; verbal scales derived
  from assessed strength, never the reverse.
  https://enfsi.eu/wp-content/uploads/2016/09/m1_guideline.pdf

## Incident response and SOC context

Where the forensic process sits when an incident is live: what the SOC hands
over, and how containment interacts with preservation. Each claim these
support in `PROCESS.md`/`RUNBOOK.md` is corroborated by at least two of them.

- **CISA — Federal Government Cybersecurity Incident and Vulnerability
  Response Playbooks** (2021). IR phases (preparation, detection & analysis,
  containment, eradication & recovery, post-incident); evidence preservation
  as an explicit criterion of the containment strategy (checklist 7a);
  backups to preserve evidence and law-enforcement coordination before
  eradication (7b–7c); preparation includes case management capturing
  affected systems, activity type, TTPs and impact, with storage accessible
  only to responders.
  https://www.cisa.gov/sites/default/files/2024-08/Federal_Government_Cybersecurity_Incident_and_Vulnerability_Response_Playbooks_508C.pdf
- **MITRE — 11 Strategies of a World-Class Cybersecurity Operations Center**,
  2nd ed. (2022). The SOC functional areas (real-time alert monitoring and
  triage; incident analysis and investigation — including "characterizing the
  confidence of these conclusions"; containment, eradication and recovery).
  Strategy 5: containment actions such as rebuilds and credential resets
  destroy forensic artefacts unless preserved first; clear command structure,
  no one acts beyond their authorisation. Section 11.7: the difference
  between IR-grade forensics (determine what happened, respond) and
  legal-grade forensics (proceedings), and involving counsel the moment legal
  use is plausible.
  https://www.mitre.org/news-insights/publication/11-strategies-world-class-cybersecurity-operations-center
- **SANS — Incident Handler's Handbook** (Kral, 2012). The six-phase PICERL
  model: preparation, identification, containment, eradication, recovery,
  lessons learned. Same shape as NIST/CISA with different labels; useful when
  a counterpart's process speaks SANS.
  https://www.sans.org/white-papers/33901

## Scientific papers — bias and investigator conduct

- Dror, Charlton & Péron, "Contextual information renders experts vulnerable
  to making erroneous identifications", *Forensic Science International*
  156(1), 2006. Experts contradicted their own prior conclusions under
  biasing context.
- Dror, "Cognitive and Human Factors in Expert Decision Making: Six Fallacies
  and the Eight Sources of Bias", *Analytical Chemistry* 92(12), 2020.
  https://pubs.acs.org/doi/10.1021/acs.analchem.0c00704
- Dror et al., "Context Management Toolbox: Linear Sequential Unmasking",
  *Journal of Forensic Sciences* 60(4), 2015. Evidence before context; the
  one-way workflow.
- Dror & Kukucka, "Linear Sequential Unmasking–Expanded (LSU-E)", *FSI:
  Synergy* 3, 2021. Sequencing all case information by bias power,
  objectivity, relevance.
- Sunde & Dror, "Cognitive and human factors in digital forensics", *Digital
  Investigation* 29, 2019. The bias problem mapped onto digital forensics.
- Sunde & Dror, "A hierarchy of expert performance applied to digital
  forensics", *FSI: Digital Investigation* 37, 2021. Digital examiners given
  different cover stories found different traces in the same evidence.
- Krane et al., "Sequential Unmasking", *Journal of Forensic Sciences* 53(4),
  2008. The precursor: interpret evidence before seeing reference material.

## Scientific papers — reporting, certainty, review

- Casey, "Error, Uncertainty, and Loss in Digital Evidence", *International
  Journal of Digital Evidence* 1(2), 2002. The C-Scale: certainty graded per
  evidence item by corroboration and tamper-resistance.
- Casey, *Digital Evidence and Computer Crime*, 3rd ed., Academic Press,
  2011. The book form of the above, with worked examples.
- Casey, "Standardization of forming and expressing preliminary evaluative
  opinions on digital evidence", *FSI: Digital Investigation* 32, 2020.
- Horsman & Sunde, "Part 1: The need for peer review in digital forensics",
  *FSI: Digital Investigation* 35, 2020.
- Sunde & Horsman, "Part 2: The Phase-oriented Advice and Review Structure
  (PARS)", *FSI: Digital Investigation* 36, 2021. Review attached to each
  phase, with templates.

## Scientific foundations and their limits

- National Research Council, *Strengthening Forensic Science in the United
  States: A Path Forward*, National Academies Press, 2009. Standard
  terminology, model reports, uncertainty in reported results, and research
  into observer bias.
  https://nap.nationalacademies.org/catalog/12589/
- NIST IR 8354 — *Digital Investigation Techniques: A NIST Scientific
  Foundation Review* (2022). The disclosure list in PROCESS.md Part 1:
  incomplete discovery, version-dependent artefact meaning, systematic rather
  than random error, examiner variation.
  https://nvlpubs.nist.gov/nistpubs/ir/2022/NIST.IR.8354.pdf
- NIST IR 8412 — *Results from a Black-Box Study for Digital Forensic
  Examiners* (2022). First large accuracy study of digital examiners.
  https://nvlpubs.nist.gov/nistpubs/ir/2022/NIST.IR.8412.pdf
