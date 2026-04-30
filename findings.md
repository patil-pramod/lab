# Salesforce Access Issues — Summary & Root Cause Analysis

**Source:** [github/business-systems](https://github.com/github/business-systems) issues
**Labels included:** `salesforce`, `access-request`, `update-access-request`
**Period:** January 1, 2025 – April 29, 2026 (16 months)
**Generated:** April 29, 2026

---

## Executive Summary

Over 16 months, **890 Salesforce-related access issues** were filed in `github/business-systems`. While most eventually close, resolution times are consistently slow — median **7.0 days**, P90 **40 days**. One in seven issues takes over a month. Root causes are structural: multi-tool bundling doubles resolution times, serial manual handoffs create a 7-day floor, manager approval blocks 15% of issues, and a team of ~4 admins has no SLA enforcement. Currently **31 issues remain open**, with 18 open longer than 14 days.

---

## Overview

| Category | Total | Open | Closed | Avg Resolution |
|---|---|---|---|---|
| New Access Requests | 757 | 21 | 736 | 14.7 days |
| Permission / Role Updates | 133 | 10 | 123 | 23.1 days |
| **Total** | **890** | **31** | **859** | **15.9 days** |

**Key finding:** Permission update requests take **57% longer** than new access requests (23.1 vs. 14.7 days avg). Updates represent 15% of volume but **32% of open issues**.

---

## Resolution Time Distribution (859 closed issues)

| Time to Close | Count | % | Cumulative % |
|---|---|---|---|
| < 1 day | 103 | 12% | 12% |
| 1–3 days | 129 | 15% | 27% |
| 3–7 days | 200 | 23% | 50% |
| 7–14 days | 202 | 24% | 74% |
| 14–30 days | 111 | 13% | 87% |
| 30+ days | 114 | 13% | 100% |

**Percentiles:** P25 = 2.3 days · P50 = 7.0 days · P75 = 14.2 days · P90 = 40.0 days · P95 = 61.5 days

Half of all issues take over a week. **114 issues (13%) took over a month** to resolve. The large gap between P75 (14 days) and P90 (40 days) reveals a long tail of severely delayed issues that inflate the mean well above the median.

---

## Quarterly Trends

| Quarter | Issues Filed | Closed | Avg Resolution | Median Resolution |
|---|---|---|---|---|
| 2025-Q1 | 211 | 210 | 23.0 days | 6.9 days |
| 2025-Q2 | 167 | 167 | 18.8 days | 7.1 days |
| 2025-Q3 | 155 | 155 | 10.9 days | 6.8 days |
| 2025-Q4 | 139 | 134 | 12.1 days | 6.1 days |
| 2026-Q1 | 150 | 146 | 14.4 days | 9.0 days |
| 2026-Q2 (partial) | 68 | 47 | 6.2 days | 6.9 days |

**Key trends:**
- **Volume is stable** at roughly 50–60 issues/month, with seasonal dips in summer and December.
- **Average resolution improved** significantly from 23.0 days (Q1 2025) to ~12 days in recent quarters.
- **Median resolution is stubbornly consistent** at 6–9 days across all quarters — indicating a structural floor imposed by the multi-step workflow.
- **Q1 2026** saw a median increase to 9.0 days, potentially reflecting a regression.

### Monthly Detail

| Month | Issues | Avg Res | Median Res |
|---|---|---|---|
| Jan 2025 | 94 | 29.8 days | 9.0 days |
| Feb 2025 | 54 | 22.4 days | 5.6 days |
| Mar 2025 | 63 | 13.4 days | 3.1 days |
| Apr 2025 | 75 | 20.1 days | 7.1 days |
| May 2025 | 54 | 12.5 days | 5.9 days |
| Jun 2025 | 38 | 25.0 days | 12.7 days |
| Jul 2025 | 47 | 10.0 days | 5.9 days |
| Aug 2025 | 50 | 12.8 days | 7.0 days |
| Sep 2025 | 58 | 10.0 days | 6.8 days |
| Oct 2025 | 50 | 13.2 days | 11.5 days |
| Nov 2025 | 52 | 15.8 days | 6.1 days |
| Dec 2025 | 37 | 5.7 days | 3.2 days |
| Jan 2026 | 47 | 16.2 days | 7.8 days |
| Feb 2026 | 51 | 14.0 days | 10.5 days |
| Mar 2026 | 52 | 13.0 days | 9.0 days |
| Apr 2026 | 68 | 6.2 days | 6.9 days |

Notable spikes: **January 2025** (29.8-day avg — post-holiday backlog) and **June 2025** (25.0-day avg despite low volume — likely staffing shortage).

---

## Year-over-Year Comparison

| Metric | 2025 (12 months) | 2026 (4 months) |
|---|---|---|
| Total Issues | 672 | 218 |
| Monthly Rate | 56/month | 55/month |
| Avg Resolution | 16.9 days | 12.4 days |
| Median Resolution | 6.8 days | 7.7 days |
| New Access | 594 (88%) | 163 (75%) |
| Updates | 78 (12%) | 55 (25%) |

Resolution averages improved by 27% in 2026. The proportion of update requests has doubled (12% → 25%), contributing to a slightly higher 2026 median (7.7 vs 6.8 days) since updates are inherently slower.

---

## Multi-Tool vs. Single-Tool Requests

| Type | Count | Avg Resolution | Median Resolution | Open Rate |
|---|---|---|---|---|
| Multi-tool (2+ apps) | 380 (43%) | 20.5 days | 9.9 days | 4% |
| Single-tool (SF only) | 475 (53%) | 12.4 days | 5.8 days | 3% |

Multi-tool requests take **65% longer on average** and have a **71% higher median resolution**. This is because:
1. Issues bundle Salesforce with Aviso, LinkedIn Sales Navigator, Outreach, and/or Certinia
2. Each tool requires a different admin to provision
3. Aviso explicitly depends on Salesforce being completed first
4. The issue stays open until the *last* tool is done

---

## Manager Approval Bottleneck

Over 16 months, **87 issues** were labeled "Awaiting Manager Approval" — roughly **10% of all issues**. Additionally:
- **62 issues** labeled "Salesforce Access Request Error" (form/data problems)
- **39 issues** labeled "Pending Salesforce Access Request" (awaiting processing)

Combined, roughly **21% of issues** encounter at least one process friction point beyond the initial submission.

Currently open approval-blocked issues:

| Issue | Age |
|---|---|
| [#14253](https://github.com/github/business-systems/issues/14253) | 43 days |
| [#14316](https://github.com/github/business-systems/issues/14316) | 19 days |
| [#14351](https://github.com/github/business-systems/issues/14351) | 6 days |
| [#14358](https://github.com/github/business-systems/issues/14358) | 1 day |

---

## Aging Open Issues

**18 issues** have been open for more than 14 days, with the oldest at **428 days**:

| Issue | Age | Title |
|---|---|---|
| [#12821](https://github.com/github/business-systems/issues/12821) | 428 days | Access Request: @emjane3 to Aviso |
| [#13957](https://github.com/github/business-systems/issues/13957) | 205 days | Access Request: @merelblaak |
| [#13959](https://github.com/github/business-systems/issues/13959) | 205 days | Access Request: Chrunchbase |
| [#13960](https://github.com/github/business-systems/issues/13960) | 204 days | Access Request: @alimarcozzi |
| [#13999](https://github.com/github/business-systems/issues/13999) | 185 days | Update permissions for: @gus-max2000 |
| [#14000](https://github.com/github/business-systems/issues/14000) | 184 days | Update permissions for: @AbbyKing |
| [#14239](https://github.com/github/business-systems/issues/14239) | 48 days | Access Request: @beverlyleung |
| [#14253](https://github.com/github/business-systems/issues/14253) | 43 days | Update permissions for: @mattcase1 |
| [#14256](https://github.com/github/business-systems/issues/14256) | 42 days | Access Request: @jglamagnere |
| [#14265](https://github.com/github/business-systems/issues/14265) | 35 days | Access Request: @ (blank handle) |

Issues open for 200+ days represent complete process abandonment — these users likely never received their requested access or the request became moot.

---

## Top Issue Submitters (16 months)

| Submitter | Issues | Role Pattern |
|---|---|---|
| @lramilo | 94 | Operations/admin role (10.5% of all volume) |
| @matt-tindall | 14 | Manager |
| @Anirudh-Jajodia | 14 | Manager |
| @nscobb | 12 | Manager |
| @jvalsamis | 12 | Manager |
| @caitevans | 12 | Manager |
| @julie-pujol | 10 | Manager |
| @cheri-dean | 10 | Manager |
| @parkerbrown11 | 10 | Manager |

A small number of repeat submitters file the majority of requests, suggesting concentrated onboarding in specific teams.

---

## Root Cause Analysis — Slow Issue Resolution

Based on analysis of **890 issues over 16 months**, including detailed review of issue comments, labels, and activity timelines.

---

### 1. Multi-Tool Request Serialization (Biggest Impact)

**380 of 890 issues (43%)** request access to multiple tools simultaneously. These take significantly longer:

- Multi-tool median: **9.9 days** vs. single-tool: **5.8 days** (71% slower)
- Multi-tool average: **20.5 days** vs. single-tool: **12.4 days** (65% slower)

**Why this happens:** The issue template allows requesters to check multiple apps (Salesforce, Aviso, LinkedIn Sales Navigator, Outreach, Certinia) in a single submission. The issue stays open until *every* tool is provisioned, even if Salesforce — the primary request — was granted within hours.

**Compounding factor — hard dependency chain:** Aviso provisioning *cannot begin* until Salesforce access is active. The Aviso admin confirmed this across multiple issues:

> *"Once SFDC user access has been provisioned, we'll be able to properly provision their account. User record is key with mapping the respective deals between both systems."*

This creates a mandatory serial chain: Issue → Salesforce entitlement PR → manager approval → Salesforce provisioning → Aviso entitlement PR → Aviso provisioning → (other tools) → close. Each handoff introduces wait time, and a delay at any step cascades downstream.

**Why it persists:** The current issue template and bot workflow treat multi-tool requests as a single atomic unit. There is no mechanism to partially close an issue or track per-tool completion status. Requesters and admins have no visibility into which tools are done vs. pending.

> **Proposed Solution — Automated Issue Decomposition:**
> Modify the `business-systems-bot` to automatically split multi-tool requests into **linked sub-issues** (one per tool) at creation time, using a parent tracking issue. Each sub-issue follows its own provisioning lifecycle and can be closed independently. The parent issue auto-closes when all sub-issues are resolved. This eliminates artificial serialization without any manual effort — the bot already parses the `[x]` checkboxes and could use them to generate per-tool sub-issues.
>
> **Expected impact:** Reduce median resolution from 9.9 to ~5.8 days for 43% of all issues (380 issues over 16 months). This is the single highest-leverage change available.

---

### 2. Multi-Step Entitlement PR Workflow (Systemic)

Every access request triggers a multi-step pipeline with manual handoffs:

```
Issue filed
  → Bot opens entitlement PR in github/entitlements
    → Manager approves and merges PR
      → Admin manually provisions user in Salesforce
        → (If multi-tool) Other admins provision their tools
          → Admin returns to issue and closes it
```

Over 16 months, the median time through this pipeline is **7.0 days**, with P90 reaching **40 days** and P95 at **61.5 days**.

**Why this happens:** Each step requires a different person to take action, and there is no automated notification between steps. After a manager merges an entitlement PR, the Salesforce admin must *notice* the merge and then manually go into Salesforce to provision the user. After provisioning, the admin must return to the GitHub issue to post a confirmation and/or close it. Each of these context switches adds idle time.

**Where the time goes (typical flow for a single-tool request):**
1. **Issue → entitlement PR:** Automated, near-instant (minutes)
2. **PR → manager approval:** 1–8 days (see Root Cause #4)
3. **Approval → provisioning:** 1–5 days (admin must notice and act)
4. **Provisioning → issue closure:** 0–2 days (admin returns to close)

Steps 2 and 3 are the primary bottlenecks. The pipeline is entirely "pull-based" — each actor must check for work rather than being pushed to act.

**Why it persists:** The workflow was designed for auditability (entitlement PRs create a paper trail), which is valuable. But the manual steps between automated triggers create dead time that compounds with volume.

> **Proposed Solution — Event-Driven Notifications and Auto-Provisioning:**
> - **Short-term:** Add webhook-triggered Slack/email notifications to push alerts to the Salesforce admin the moment an entitlement PR is merged (eliminating step 3 idle time). Add a daily automated digest of "merged but not provisioned" PRs to prevent anything from falling through.
> - **Medium-term:** Investigate Salesforce provisioning APIs to auto-create user accounts when entitlement PRs merge, reducing the manual provisioning step to a verification-only action. This could cut the median from 7.0 to ~3 days.
> - **Long-term:** Implement a fully event-driven pipeline where each step auto-triggers the next, with human intervention only for exceptions.
>
> **Expected impact:** Reduce median from 7.0 to 3–4 days by eliminating idle time between steps.

---

### 3. Permission Updates Are Disproportionately Slow

Permission update requests average **23.1 days** — 57% longer than new access (14.7 days). Updates represent 15% of volume but **32% of currently open issues** (10 of 31). All 10 currently open update requests have been open >14 days.

**Why this happens:**
- **Additional approval requirements:** Updates require managers to post an explicit attestation comment (checkboxes in a comment template), adding a manual step not present in new access requests.
- **Ambiguous scope:** Update requests often describe complex permission changes in free-text (e.g., "moving to a new team, needs Sales Ops view"), requiring the admin to interpret the request and determine the correct Salesforce profile/permission set — unlike new access requests which follow a standardized template.
- **No dedicated workflow:** The bot handles new access requests with automated entitlement PRs, but update requests appear to follow a less automated path. Some updates are tagged "Update Access Request Error," suggesting the bot's update handling is fragile.
- **Lower priority:** With 56 issues/month, admins naturally prioritize new access (people who can't work at all) over updates (people who have some access but need changes).

**Why it persists:** The update-access-request template and bot workflow were likely designed as an afterthought to the primary new-access flow. There is no parity in automation between the two paths.

> **Proposed Solution — Standardized Update Workflow:**
> - Create a structured update request template with **predefined permission change types** (team transfer, role upgrade, additional module access) instead of free-text descriptions. This enables the bot to generate the correct entitlement PR automatically.
> - Auto-request manager approval via **@mention and a Slack DM** at submission time, rather than waiting for the manager to discover the issue.
> - Add **auto-merge for low-risk updates** (e.g., team transfers where the new manager has already approved) to skip the manual merge step.
>
> **Expected impact:** Reduce update resolution from 23.1 to ~14 days (parity with new access) by standardizing the process and eliminating ambiguity.

---

### 4. Manager Approval Bottleneck

**87 issues** (10%) were tagged "Awaiting Manager Approval" over 16 months. Combined with 62 "Salesforce Access Request Error" and 39 "Pending Salesforce Access Request" labels, roughly **21% of issues** encounter at least one process friction point.

**Why this happens:**
- **Passive approval mechanism:** Managers must visit the GitHub issue or entitlement PR and post an approval comment/review. GitHub does not send push notifications for these by default unless the manager is explicitly @mentioned.
- **Competing priorities:** Managers filing access requests for their reports are typically busy with other work. Approving an entitlement PR is a low-urgency, low-visibility task that gets deferred.
- **No deadline pressure:** There is no SLA, no reminder, and no escalation. An approval request from 43 days ago (#14253) looks identical to one from yesterday.
- **Multiple approval paths:** Some issues require approval via PR review, others via comment attestation, and updates require a different checkbox format. This inconsistency adds cognitive friction.

**Why it persists:** The approval step was designed for compliance and auditability, but no operational tooling was built around it to ensure timely completion.

> **Proposed Solution — Automated Approval Nudging with Escalation:**
> - **Day 0:** Bot @mentions the manager in the issue and sends a Slack DM with a direct approval link.
> - **Day 2 (48 hours):** Automated reminder via Slack and GitHub comment: *"This access request is awaiting your approval. Please review."*
> - **Day 5 (business days):** Escalation to the manager's manager (extractable from the org chart / Workday integration) with a note: *"Access request pending 5 days without approval."*
> - **Day 10:** Auto-flag for the business-systems team to manually intervene or close as stale.
>
> This requires no additional headcount — only a GitHub Actions workflow with Slack integration.
>
> **Expected impact:** Reduce approval delays from 3–43 days to <3 days for the majority of issues. Addresses 10% of all volume directly and unblocks downstream provisioning.

---

### 5. Single Points of Failure in Provisioning

The provisioning team is very small, with each tool depending on a single individual:

| Admin | Role | Observations |
|---|---|---|
| @zahmed727 | Primary Salesforce provisioner | Appears on nearly every SF issue; sole person doing setup |
| @DianeEnriquez | Aviso administrator | Blocked until SF is done; single assignee |
| @ElleKell | Outreach administrator | Single assignee for all Outreach provisioning |
| @Jcrosstheuniverse | Certinia/FinancialForce admin | OOO caused multi-week delays |

**Why this happens:** Salesforce provisioning requires admin-level access to the Salesforce org and knowledge of profile/permission set assignments, role hierarchies, and forecasting setup. This is specialized knowledge that hasn't been documented or cross-trained.

**Evidence of impact:** When key admins are unavailable, resolution times spike dramatically:
- **June 2025:** 25.0-day avg resolution (vs 12.5 in May) with below-average volume — likely admin PTO
- **October 2025:** 11.5-day median (vs 6.1 in surrounding months)
- **Issue #14326:** Required two follow-up bumps over 11 days because the Certinia admin was OOO for a full week

**Why it persists:** These are specialized roles, and the provisioning volume (~56 issues/month) may not seem large enough to justify redundancy. However, the impact of a single person's absence on resolution times across all issues makes this a high-risk single point of failure.

> **Proposed Solution — Reduce Manual Provisioning Dependency:**
> Since adding headcount is not possible, the focus should be on **reducing the amount of work that requires these specific individuals:**
> - **Automate Salesforce provisioning** via Salesforce APIs (User creation, Profile assignment, Permission Set assignment). The entitlement PR already contains the required information (access type, mirror user). A post-merge webhook could trigger a Salesforce API call to provision the user automatically, with the admin reviewing the result rather than performing the action.
> - **Create runbook documentation** for each tool's provisioning process so that *any* team member can perform provisioning when the primary admin is unavailable. Even without additional headcount, existing team members can cover for each other.
> - **Implement Salesforce provisioning via Okta SCIM** (if not already in place) to automate user lifecycle management — when the entitlement is merged, Okta automatically provisions the Salesforce account.
> - **Batch provisioning:** Instead of processing issues one-at-a-time, implement a daily batch job that provisions all approved-and-merged requests in one session. This is more efficient for a single admin managing high volume.
>
> **Expected impact:** Reduce admin dependency from "all issues" to "exception handling only." Eliminate PTO/OOO-related spikes.

---

### 6. Stale / Abandoned Issues

**18 issues** are currently open for more than 14 days. Six have been open for **184+ days**, representing complete process abandonment. The oldest (#12821) has been open for **428 days**.

**Why this happens:**
- **No triage mechanism:** After the bot opens an entitlement PR, there is no assignment of the issue to a specific admin. The issue sits in the queue and depends on someone noticing it.
- **No aging alerts:** There are no automated notifications when issues exceed a time threshold. Issues that miss the initial processing window can sit indefinitely.
- **Queue overwhelm:** With ~56 issues/month, admins process what's in front of them. Older issues get pushed down and forgotten — there is no prioritization mechanism favoring older issues.
- **Ambiguous state:** Some stale issues may be functionally resolved (the user got access through another channel) but were never formally closed. There is no mechanism to verify or auto-close these.

**Why it persists:** The current system is purely reactive — it depends on the requester to follow up if their issue is stuck. If the requester moves on (or finds another way to get access), the issue is never closed.

> **Proposed Solution — Automated Lifecycle Management:**
> - **Auto-assign:** When the entitlement PR is merged, automatically assign the issue to the appropriate provisioning admin based on the tool type (the bot already knows which tool is requested).
> - **Stale detection (7 days):** Auto-comment on issues with no human activity after 7 days: *"This issue has had no activity for 7 days. @admin — is this still pending?"*
> - **Escalation (14 days):** Auto-label as "stale" and notify the business-systems team lead.
> - **Auto-close (30 days):** After 30 days of no activity, auto-close with a message: *"This issue has been automatically closed due to inactivity. If access is still needed, please reopen or file a new request."*
> - **Retroactive cleanup:** Run a one-time triage of the 18 currently stale issues to close or reactivate them.
>
> **Expected impact:** Eliminate the stale issue backlog and prevent future accumulation. Zero issues should be open >30 days without active work.

---

### 7. Incomplete / Malformed Submissions

**62 issues** were labeled "Salesforce Access Request Error" and 6 had "Update Access Request Error" over 16 months — **7.6% of all issues** contain data quality problems that delay processing.

**Common problems observed:**
- **Missing required fields:** Manager handle, mirror user handle left blank or filled with placeholder text
- **Blank GitHub handles:** Titles like "Access Request: @" with the actual handle buried in the body or missing entirely
- **App names as handles:** Titles like "Access Request: @Salesforce @Aviso" where the requester entered tool names instead of their username
- **"TBD" placeholder values:** Fields filled with "TBD" that technically pass validation but are unusable
- **Duplicate/conflicting requests:** Same user requesting access via multiple issues, creating confusion

**Why this happens:** The issue template uses GitHub's form schema which validates field presence but not field *quality*. A field containing "@" or "TBD" passes the "required" check but is meaningless. Additionally, the template instructions may be unclear for first-time submitters.

**Why it persists:** The bot catches some errors (e.g., completely missing manager handle) and posts an error comment, but many malformed submissions pass initial validation and are only caught during manual provisioning — by which point the issue has been open for days.

> **Proposed Solution — Enhanced Front-End Validation:**
> - **Pre-submission validation:** Add GitHub Actions validation on issue creation that checks:
>   - GitHub handle resolves to a real user (API call to `api.github.com/users/{handle}`)
>   - Mirror user handle is not blank, "TBD", or an app name
>   - Manager handle resolves to a user in the org
>   - At least one application checkbox is checked
>   - For updates: description field is not blank and exceeds a minimum length
> - **Auto-reject with guidance:** If validation fails, auto-comment with specific instructions on what to fix and remove the processing label until corrected. This prevents malformed issues from entering the provisioning queue.
> - **Template improvements:** Add inline examples and helper text in the issue template (e.g., *"Enter your GitHub username without the @ symbol, e.g., `johndoe`"*).
>
> **Expected impact:** Reduce error-labeled issues from 7.6% to <1%, eliminating ~60 rework cycles per 16 months.

---

### 8. No SLA Enforcement or Escalation Path

There is no evidence of defined SLAs, automated reminders, escalation workflows, or resolution metrics across any of the 890 issues analyzed.

**Impact of the absence:**
- **No accountability:** Without a target, there is no way to distinguish between acceptable and unacceptable resolution times. A 7-day resolution and a 428-day resolution are treated identically by the system.
- **No prioritization:** All issues look the same in the queue. There is no mechanism to surface urgent requests or aging issues above new ones.
- **No trend visibility:** The team has no dashboard or metrics to identify when resolution times are trending upward, which months have backlogs, or which admins are overloaded.
- **Reactive follow-ups only:** Currently, the only escalation mechanism is a requester manually posting "friendly bump" comments. Analysis of issue comments shows these bumps are common (observed in #14325, #14326, #14327, and others), confirming that requesters regularly experience delays with no recourse.

**Why it persists:** SLA enforcement requires tooling (dashboards, alerts, workflows) that hasn't been prioritized. The team may perceive current resolution times as acceptable because there's no baseline or benchmark to compare against.

> **Proposed Solution — SLA Framework with Automated Enforcement:**
>
> **Define tiered SLAs:**
> | Request Type | Target Resolution | Escalation Trigger |
> |---|---|---|
> | New access, single-tool | 3 business days | Day 4 |
> | New access, multi-tool | 5 business days | Day 6 |
> | Permission update | 5 business days | Day 6 |
> | Priority / urgent (new label) | 1 business day | Day 2 |
>
> **Implement via GitHub Actions:**
> - On issue creation, calculate the SLA deadline based on type and add it as a comment and label (e.g., `sla:2026-05-05`).
> - Daily scheduled workflow scans all open issues and:
>   - At 75% of SLA: posts a reminder comment and Slack DM to the assigned admin
>   - At 100% of SLA: labels as `sla-breach`, notifies team lead
>   - At 150% of SLA: escalates to management
> - Weekly auto-generated summary posted to a Slack channel showing: issues opened, closed, breached, average resolution time, and aging distribution.
>
> **Build a resolution dashboard** (GitHub Projects board or a simple web dashboard fed by the GitHub API):
> - Open issues by age bucket (on-track / at-risk / breached)
> - Per-admin workload and queue depth
> - Monthly trend: volume, resolution time, SLA compliance rate
> - Bottleneck analysis: which step (approval / provisioning / closure) has the most idle time
>
> **Expected impact:** Create organizational visibility and accountability. Establish a measurable baseline and drive continuous improvement. Target: 80% of issues resolved within SLA within 3 months of implementation.

---

## Summary of Root Causes

| # | Root Cause | Impact (16 months) | Scale |
|---|---|---|---|
| 1 | Multi-tool request serialization | Multi-tool takes 71% longer (9.9d vs 5.8d median) | 380/890 issues (43%) |
| 2 | Multi-step entitlement PR workflow | Median 7.0d, P90 = 40d, P95 = 61.5d | All 890 issues |
| 3 | Permission updates disproportionately slow | Updates avg 23.1d vs new access 14.7d (57% slower) | 133 issues; 10 of 31 open |
| 4 | Manager approval delays | 87 issues tagged "Awaiting Approval" (10%) | ~21% hit friction points |
| 5 | Single points of failure | Admin OOO causes multi-week spikes | All issues depend on ~4 people |
| 6 | Stale/abandoned issues | 18 open >14 days; oldest at 428 days | Chronic |
| 7 | Malformed submissions | 68 issues with error labels (7.6%) | Systemic |
| 8 | No SLA / escalation | No systemic pressure to resolve on time | All open issues |

---

## Recommendations — Prioritized Implementation Roadmap

All recommendations are designed to work **within existing headcount** by leveraging automation (GitHub Actions, bot enhancements, API integrations) to reduce manual work and eliminate idle time.

### Phase 1: Quick Wins (1–2 weeks to implement)

| # | Action | Addresses Root Cause | Expected Impact |
|---|---|---|---|
| 1 | **Automated approval nudging** — Add a GitHub Actions workflow that @mentions managers on issue creation, sends a Slack DM with approval link, and auto-reminds at 48h and 5 business days. | #4 (Manager approval) | Reduce approval delays from 3–43 days to <3 days |
| 2 | **Stale issue lifecycle** — Add auto-comment at 7 days of inactivity, auto-label "stale" at 14 days, auto-close at 30 days with reopen instructions. Run one-time cleanup of 18 currently stale issues. | #6 (Stale issues) | Eliminate stale backlog; prevent future accumulation |
| 3 | **Enhanced intake validation** — Add issue-creation GitHub Actions workflow to validate GitHub handles exist, reject "TBD" values, and check required fields before processing. | #7 (Malformed submissions) | Reduce error rate from 7.6% to <1% |

### Phase 2: Structural Changes (2–4 weeks to implement)

| # | Action | Addresses Root Cause | Expected Impact |
|---|---|---|---|
| 4 | **Automated issue decomposition** — Modify `business-systems-bot` to split multi-tool requests into linked sub-issues (one per tool), each with its own lifecycle. Parent auto-closes when all subs resolve. | #1 (Multi-tool serialization) | Reduce median from 9.9 to ~5.8 days for 43% of issues |
| 5 | **Event-driven admin notifications** — Add webhook-triggered Slack alerts to provisioning admins when entitlement PRs are merged. Include a daily digest of "merged but not provisioned" items. | #2 (Pipeline idle time), #5 (Single points of failure) | Cut idle time between approval and provisioning from 1–5 days to <1 day |
| 6 | **Standardized update workflow** — Create structured update request template with predefined change types. Enable bot to auto-generate entitlement PRs for updates (parity with new access). | #3 (Slow updates) | Reduce update resolution from 23.1 to ~14 days |

### Phase 3: Automation & Visibility (1–2 months to implement)

| # | Action | Addresses Root Cause | Expected Impact |
|---|---|---|---|
| 7 | **SLA framework with automated enforcement** — Define tiered SLAs (3 days single-tool, 5 days multi-tool/updates). Implement via scheduled GitHub Actions: reminders at 75%, breach alerts at 100%, escalation at 150%. | #8 (No SLA) | Establish accountability; target 80% SLA compliance in 3 months |
| 8 | **Salesforce provisioning automation** — Use Salesforce APIs or Okta SCIM to auto-provision users when entitlement PRs merge. Reduce admin role to verification only. | #2 (Pipeline), #5 (Single points of failure) | Reduce manual provisioning dependency; eliminate OOO-related stalls |
| 9 | **Resolution dashboard** — Build a GitHub Projects board or lightweight web dashboard showing open issues by age, SLA status, admin workload, monthly trends, and bottleneck analysis. | #8 (No SLA), all | Organizational visibility; data-driven process improvement |

### Projected Cumulative Impact

| Metric | Current | After Phase 1 | After Phase 2 | After Phase 3 |
|---|---|---|---|---|
| Median resolution (all) | 7.0 days | 5–6 days | 4–5 days | 2–3 days |
| Median resolution (multi-tool) | 9.9 days | 8 days | 5–6 days | 3–4 days |
| P90 resolution | 40 days | 25 days | 15 days | 7–10 days |
| Issues open >14 days | 18 | 5–8 | 2–3 | 0–1 |
| Error-labeled issues | 7.6% | <1% | <1% | <1% |
| Manager approval delay | 3–43 days | <3 days | <3 days | <2 days |
