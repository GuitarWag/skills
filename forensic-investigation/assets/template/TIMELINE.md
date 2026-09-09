<!--
TEMPLATE — master timeline. Delete these comments.
Rules: one canonical timezone declared up front; every row cites its evidence;
facts and assessments visibly separated; uneventful rows kept where the flat
line is itself a finding.
-->

# <TICKET-ID> — Timeline

<Classification line.>

**Revision <N>.** All times **UTC**. <If a source records another offset, show
both, side by side — never convert silently.> Every row cites its evidence.

Legend — **[F]** established fact · **[A]** assessment · **[R]** reported (ticket or third party, not independently verified)

## Phase 0 — <baseline / environment established> (<date range>)

| Time (UTC) | Event | Src | Evidence |
|------------|-------|-----|----------|
| <YYYY-MM-DD HH:MM:SS> | <event> | [F] | `<evidence file>` |
| <YYYY-MM-DD> | <day-granular event> | [R] | ticket |
| **<YYYY-MM-DD HH:MM:SS>** | <pivotal event — bold the time cell> | [F] | `<file>` |

> **[A] <Confidence>: <the inference this phase supports>.** <Reasoning.>
> <What would falsify it.> (Q<n>)

## Phase 1 — <exposure / trigger> (<date range>)

<Same row format. Approximate times as `~HH:MM`. Unknown-order events as
`*(later)*`. Ranges as `YYYY-MM-DD HH:MM → MM-DD HH:MM`.>

## Phase 2 — <the incident> (<date range>)

## Phase 3 — <response and containment> (<date range>)

<For the response window, add columns if a second timezone or a per-interval
metric matters:>

| Time (UTC) | Local (<offset>) | Event | Src | <metric per interval> |
|------------|------------------|-------|-----|-----------------------|
| <time> | <time> | <action taken> | [F] | <value> |
| <time> | <time> | — | [F] | <value — keep flat rows: flat is observed, not missing> |

## Phase 4 — post-incident

## The containment picture

<Optional: a small fenced ASCII diagram lining up control actions against the
observed rate, followed by the one or two conclusions it supports. This is the
only place the timeline argues; everywhere else it records.>
