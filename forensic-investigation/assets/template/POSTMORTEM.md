<!--
TEMPLATE — blameless postmortem. Delete these comments.
This is the organisational read of the same events: short, plain language, no
evidence citations, no confidence markers. It defers to REPORT.md for proof and
RECOMMENDATIONS.md for actions. Keep it the shortest substantive document.
-->

# Postmortem — <TICKET-ID>: <impact in the title>

<Classification line.>

**Blameless.** This document examines decisions and systems, not people. Where
a judgement turned out wrong, the question is what made the wrong call the
easy one.

| | |
|---|---|
| Severity | <sev> |
| Impact | <cost / data / downtime, quantified> |
| Duration | <first event to containment> |
| Time to detect | <duration — and who detected it: us, a third party, the provider> |
| Time to mitigate | <duration from detection> |
| Data loss | <yes/no/unknown> |
| Status | <closed / actions pending> |

## What happened

<Three or four short paragraphs, plain language. A new joiner should follow it.>

## Timeline

All times UTC. <Condensed from TIMELINE.md: the warning signs, the incident,
the response. Only the rows that drive the lessons.>

## Why it went on for <duration>

<One numbered item per control that should have caught it, each explaining why
the failure was structural rather than individual. Italicise the single change
most likely to have prevented the loss.>

1. <control that did not fire, and why that was the system's fault>
2. <...>

## What went well

- <...>

## Where we got lucky

<Kept separate from "went well" on purpose: luck is not a control.>

- <...>

## What we still don't know

| | |
|---|---|
| <question> | <why it is open, where it is tracked (Qn)> |

## Actions

IDs shared with `RECOMMENDATIONS.md`.

| # | Action | Owner | Priority |
|---|--------|-------|----------|
| R1 | <action> | <team> | Critical |

## Note on this postmortem's accuracy

<If any earlier conclusion was corrected, say so here: what the first version
concluded, how the error was caught, and the general lesson. See CORRECTIONS.md.>
