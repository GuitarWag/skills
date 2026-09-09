<!--
TEMPLATE — observables and indicators. Delete these comments.
Audience: future responders and detection engineers. Benign entries are listed
so nobody re-investigates them from scratch.
-->

# <TICKET-ID> — Observables and Indicators

<Classification line. Warning if entries contain personal data.>

**Presence here is not an allegation.** Each entry carries an assessment.
Several are benign and are listed so that a future responder does not
re-investigate them from scratch.

## 1. Network observables

| Indicator | ASN / Org | Geo | First seen | Context | Assessment |
|-----------|-----------|-----|------------|---------|------------|
| <IP / domain> | <asn> | <geo, quoted from tool — state if the examiner did no geolocation> | <date> | <where it appeared> | **Confirmed incident vector.** / **Priority lead.** / **Unexplained.** / Benign — <reason> |

> <If a key indicator is NOT available, say so and why: "No source IP exists
> for the incident traffic itself — the records were never created. See
> REPORT.md §<n>.">

## 2. Identity and credential observables

| Indicator | Type | Assessment |
|-----------|------|------------|
| <principal / key id / user> | <type> | **Confirmed incident vector.** / **Capability of concern.** / **False positive.** / Benign / Excluded |

## 3. Machine-matchable signatures

<The strings a detection can match on: service names, usage types, operation
names, metric namespaces and dimensions, user agents (note: a user agent is
not an identity).>

| Signature | Value |
|-----------|-------|
| <field> | `<value>` |

## 4. Behavioural signature

| Attribute | Observed |
|-----------|----------|
| Onset | <sudden / ramped, time> |
| Rate | <peak and stability> |
| Shape | <request pattern, error rate, cache ratio> |
| Termination | <how it ended> |

<One closing paragraph: what this combination is consistent with, and what it
is not.>

## 5. Suggested detections

Each rationale states when the detection would have fired during this incident
and at what loss.

| # | Detection | Rationale |
|---|-----------|-----------|
| D1 | <alert definition> | Would have fired at <time>, ~<duration> in, at roughly <impact so far>. |
