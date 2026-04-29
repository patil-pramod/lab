# Salesforce Access Issues — Summary & Root Cause Analysis

**Source:** [github/business-systems](https://github.com/github/business-systems) issues
**Period:** January 28 – April 28, 2026 (3 months)
**Generated:** April 28, 2026

---

## Overview

A total of **177 Salesforce-related access issues** were filed in the `github/business-systems` repository over the past 3 months. Of these:

| Category | Count | Open | Closed | Avg Resolution |
|---|---|---|---|---|
| New Access Requests | 154 | 17 | 137 | 11.9 days |
| Permission / Role Updates | 23 | 8 | 15 | 14.7 days |
| Access Removals | 0 | — | — | — |
| **Total** | **177** | **25** | **152** | **12.2 days** |

### Monthly Trend

| Month | Issues Filed | Open | Closed | Avg Resolution | Median Resolution |
|---|---|---|---|---|---|
| Jan 2026 (partial) | 6 | 0 | 6 | 37.5 days | 47.6 days |
| Feb 2026 | 52 | 1 | 51 | 14.0 days | 10.5 days |
| Mar 2026 | 52 | 4 | 48 | 13.0 days | 9.0 days |
| Apr 2026 | 67 | 20 | 47 | 6.3 days | 6.9 days |

Volume has been increasing month-over-month (52 → 52 → 67), with April on pace for the highest monthly volume. Resolution times have improved from a median of 10.5 days in February to 6.9 days in April, though April has many issues still open.

### Resolution Time Distribution (152 closed issues)

| Time to Close | Count | % |
|---|---|---|
| < 1 day | 20 | 13% |
| 1–3 days | 19 | 13% |
| 3–7 days | 30 | 20% |
| 7–14 days | 36 | 24% |
| 14–30 days | 34 | 22% |
| 30+ days | 13 | 9% |

**Key percentiles:** P25 = 3.0 days, P50 (median) = 7.7 days, P75 = 15.7 days, P90 = 28.0 days, P95 = 35.0 days

Nearly half of all issues (46%) take over a week to resolve. One in ten issues takes nearly a month.

---

## Aging Open Issues

**9 issues** have been open for more than 14 days:

| Issue | Age | Title |
|---|---|---|
| [#14178](https://github.com/github/business-systems/issues/14178) | 79 days | akash1-dotcom SFDC access issue |
| [#14239](https://github.com/github/business-systems/issues/14239) | 47 days | Access Request: @beverlyleung Outreach access |
| [#14253](https://github.com/github/business-systems/issues/14253) | 42 days | Update Existing Access or Permissions for: @mattcase1 |
| [#14256](https://github.com/github/business-systems/issues/14256) | 41 days | Access Request: @jglamagnere |
| [#14265](https://github.com/github/business-systems/issues/14265) | 34 days | Access Request: @ Access to Salesforce via Okta |
| [#14279](https://github.com/github/business-systems/issues/14279) | 28 days | Update Existing Access or Permissions for: @louisleccia |
| [#14280](https://github.com/github/business-systems/issues/14280) | 28 days | Update Existing Access or Permissions for: @justin-goertz |
| [#14308](https://github.com/github/business-systems/issues/14308) | 20 days | Update Existing Access or Permissions for: @bpalmore |
| [#14316](https://github.com/github/business-systems/issues/14316) | 18 days | Update Existing Access or Permissions for: @adamstama |

Issue [#14178](https://github.com/github/business-systems/issues/14178) has been open for **79 days** — nearly 3 months with no resolution.

---

## Multi-Tool vs. Single-Tool Requests

| Type | Count | Avg Resolution | Median Resolution | Open Rate |
|---|---|---|---|---|
| Multi-tool (2+ apps) | 66 | 17.9 days | 15.0 days | 24% (16/66) |
| Single-tool (SF only) | 104 | 9.6 days | 6.8 days | 8% (8/104) |

Multi-tool requests take **nearly twice as long** to resolve and are **3× more likely** to remain open. This is the single largest driver of slow resolution.

---

## Manager Approval Bottleneck

**12 issues** were labeled "Awaiting Manager Approval" over the 3-month period. Among the currently open issues, several have been awaiting approval for weeks:

| Issue | Age | Status |
|---|---|---|
| [#14253](https://github.com/github/business-systems/issues/14253) | 42 days | Open — awaiting approval |
| [#14316](https://github.com/github/business-systems/issues/14316) | 18 days | Open — awaiting approval |
| [#14351](https://github.com/github/business-systems/issues/14351) | 5 days | Open — awaiting approval |
| [#14358](https://github.com/github/business-systems/issues/14358) | < 1 day | Open — awaiting approval |

---

## Top Issue Submitters (3 months)

| Submitter | Issues Filed |
|---|---|
| @caitevans | 10 |
| @curtisfoye | 6 |
| @dimmykumont | 6 |
| @matt-tindall | 5 |
| @elstudio | 4 |
| @DGpeach | 4 |
| @michaelsainz | 3 |
| @cheri-dean | 3 |
| @Claudiadenb | 3 |
| @andrewkodsi | 3 |

A small number of managers file the majority of requests, suggesting concentrated onboarding in specific teams.

---

## Access Removals

No Salesforce access removal or deprovisioning requests were filed during this entire 3-month period, despite 177 new access and update requests. This raises concerns about access hygiene and timely offboarding.

---

## Root Cause Analysis — Slow Issue Resolution

Based on analysis of **177 issues over 3 months**, including detailed review of issue comments, labels, and activity timelines, the following root causes were identified.

---

### 1. Multi-Tool Request Serialization (Biggest Impact)

**66 of 177 issues (37%)** request access to multiple tools simultaneously. These take nearly twice as long to resolve:

- Multi-tool median resolution: **15.0 days** vs. single-tool: **6.8 days**
- Multi-tool open rate: **24%** vs. single-tool: **8%**

Issues remain open until **every** tool is provisioned, even if Salesforce access was granted promptly. Critically, **Aviso provisioning cannot begin until Salesforce access is active**. The Aviso admin (@DianeEnriquez) stated across multiple issues:

> *"Once SFDC user access has been provisioned, we'll be able to properly provision their account. User record is key with mapping the respective deals between both systems."*

This hard dependency creates serial delays where each tool waits for the previous one.

---

### 2. Multi-Step Entitlement PR Workflow (Systemic)

Every access request triggers a multi-step pipeline:
1. Issue filed → bot opens an **entitlement PR** in `github/entitlements`
2. Manager or team owner must **approve and merge** the PR
3. A Salesforce admin manually **provisions** the user
4. If other tools are requested, separate admins complete their steps
5. Issue is closed only after **all** tools are provisioned

This creates a serial chain of handoffs. Over 3 months, the median time through this pipeline is **7.7 days**, with P90 reaching **28 days**. For example, [#14327](https://github.com/github/business-systems/issues/14327) had its entitlement PR opened on April 15 but Salesforce access wasn't completed until April 24 — a 9-day gap for a process that should take hours.

---

### 3. Manager Approval Bottleneck

Entitlement PRs require the listed manager to approve before they can be merged. Over 3 months, **12 issues** were tagged "Awaiting Manager Approval" — and these are among the slowest to resolve:

| Issue | Age | Status |
|---|---|---|
| [#14253](https://github.com/github/business-systems/issues/14253) | 42 days | Still awaiting approval |
| [#14316](https://github.com/github/business-systems/issues/14316) | 18 days | Still awaiting approval |
| [#14356](https://github.com/github/business-systems/issues/14356) | @michaelsainz | 3-day delay (PR opened Apr 24, approved Apr 27) |
| [#14327](https://github.com/github/business-systems/issues/14327) | @john-john-florence | 8-day delay (user had to follow up) |

Permission update requests are particularly affected — they average **14.7 days** to resolve vs. 11.9 days for new access, largely because they require additional manager attestation. There is no visible SLA or automated escalation for overdue approvals.

---

### 4. Small Admin Team / Single Points of Failure

The comment history reveals a very small provisioning team:

| Admin | Role | Observations |
|---|---|---|
| @zahmed727 | Primary Salesforce provisioner | Appears on nearly every issue; sole person doing SF setup |
| @DianeEnriquez | Aviso administrator | Blocked until SF is done; appears on all Aviso requests |
| @ElleKell | Outreach administrator | Single assignee for all Outreach provisioning |
| @Jcrosstheuniverse | Certinia/FinancialForce admin | Was OOO for a full week, blocking [#14326](https://github.com/github/business-systems/issues/14326) |

When any one of these individuals is unavailable, issues stall. [#14326](https://github.com/github/business-systems/issues/14326) required **two follow-up bumps** from @caitevans over 11 days because @Jcrosstheuniverse was out of office.

---

### 5. Stale Issues with No Activity

Over 3 months, multiple issues have gone dormant with minimal or zero human follow-up:

| Issue | Age (days) | Last Activity |
|---|---|---|
| [#14178](https://github.com/github/business-systems/issues/14178) | 79 | Oldest open issue — nearly 3 months unresolved |
| [#14239](https://github.com/github/business-systems/issues/14239) | 47 | Outreach access still pending |
| [#14256](https://github.com/github/business-systems/issues/14256) | 41 | No resolution after 6 weeks |
| [#14265](https://github.com/github/business-systems/issues/14265) | 34 | Blank handle in title; likely lost |
| [#14332](https://github.com/github/business-systems/issues/14332) | 12 | Only bot comment; no admin engagement |
| [#14334](https://github.com/github/business-systems/issues/14334) | 12 | Only bot comment; no admin engagement |

These issues appear to have fallen through the cracks — the entitlement PR was opened but nobody picked them up. There is no visible triage or assignment mechanism beyond the initial bot automation.

---

### 6. Incomplete / Malformed Submissions

Several issues contained data quality problems that either delayed processing or required manual intervention:

| Issue | Problem |
|---|---|
| [#14328](https://github.com/github/business-systems/issues/14328) | Missing required "Manager GitHub Handle" — bot flagged it, submitter had to edit and re-trigger |
| [#14356](https://github.com/github/business-systems/issues/14356) | Title shows "Access Request: @" (blank handle); actual handle buried in body |
| [#14327](https://github.com/github/business-systems/issues/14327) | Title lists app names (@Salesforce, @Aviso) instead of user handle |
| [#14353](https://github.com/github/business-systems/issues/14353) | Mirror User Handle listed as "TBD" |
| [#14357](https://github.com/github/business-systems/issues/14357) | Labeled "Update Access Request Error" — indicates a submission problem |

While the bot catches some missing fields, issues with incorrect (but present) data pass validation and cause confusion downstream.

---

### 7. No SLA Enforcement or Escalation Path

There is no evidence of:
- Defined SLAs for issue resolution time
- Automated reminders for aging issues
- Escalation workflows when issues exceed a time threshold
- Dashboard or reporting on resolution metrics

Follow-ups are ad-hoc — requesters or their colleagues manually bump stale issues (e.g., @skmishra84 bumping [#14325](https://github.com/github/business-systems/issues/14325) after 2 days, @caitevans bumping [#14326](https://github.com/github/business-systems/issues/14326) twice).

---

## Summary of Root Causes

| # | Root Cause | Impact (3-month data) | Scale |
|---|---|---|---|
| 1 | Multi-tool request serialization | Multi-tool issues take 2× longer (15d vs 6.8d median); 3× more likely to stay open | 66/177 issues (37%) |
| 2 | Multi-step entitlement PR workflow | Median 7.7 days end-to-end; P90 = 28 days | All 177 issues |
| 3 | Manager approval delays | 12 issues tagged "Awaiting Approval"; some waiting 42+ days | Recurring across all months |
| 4 | Single points of failure (small admin team) | One person OOO blocks all issues for that tool | All issues depend on ~4 admins |
| 5 | Stale issues with no triage | Issues open 34–79 days with no engagement | 9 issues open > 14 days |
| 6 | Incomplete submissions | Rework and reprocessing delays | Multiple per month |
| 7 | No SLA / escalation mechanism | No systemic pressure to resolve on time | All open issues |

---

## Recommendations

1. **Decouple multi-tool issues** (highest impact) — Split multi-tool requests into separate sub-issues per tool so Salesforce access can be closed independently. This alone would reduce median resolution from 15 days to ~7 days for 37% of issues.
2. **Set and enforce SLAs** — Define target resolution times (e.g., 2 business days for Salesforce-only, 5 for multi-tool) with automated reminders at 24h and 48h. Current P90 of 28 days is unacceptable.
3. **Auto-assign provisioning admins** — Extend the bot to assign @zahmed727 (or a team rotation) immediately when Salesforce is requested, not just for Aviso/Outreach.
4. **Add backup admins** — Cross-train at least one backup for each tool admin to prevent OOO-related stalls. The Certinia admin OOO incident (#14326) caused an 11-day delay.
5. **Automate manager approval escalation** — If a manager hasn't approved an entitlement PR within 48 hours, auto-remind them. After 5 business days, escalate to their manager.
6. **Improve intake validation** — Strengthen bot validation to catch blank handles, "TBD" fields, and app-name-as-handle errors before the issue is accepted. At least 5 issues per month have data quality problems.
7. **Implement stale issue detection** — Auto-label and escalate issues with no human activity after 48 hours. Currently, 9 issues are open > 14 days with no escalation.
8. **Dashboard for visibility** — Create a tracking dashboard showing open issues by age, assignee workload, and bottleneck stage to enable proactive management.
9. **Review access hygiene** — Zero deprovisioning requests in 3 months despite 177 access grants warrants an audit of former employee access.
