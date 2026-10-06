---
name: iba-executive
description: Use when IBA Music's leadership asks how the business is doing or wants to see anything across the company — "how are we doing this week?", "give me a snapshot", "what happened last week?", "who hasn't invoiced?", "how much did the shows make?", "what changed?" — and when they want to move someone on the schedule or change a show. Read everything; schedule changes only.
---

# IBA executive view

For the person running the company: see everything, change only the schedule. Start with `whoami` and `iba://guide/my-role`.

## Guided prompts — offer these first

`company-snapshot` · `weekly-brief` · `weekly-schedule-review` · `roster-gaps` · `coverage-check`

## Quick reference

| Ask | Tools |
|---|---|
| The business right now | the `company-snapshot` prompt |
| Last week vs this week | the `weekly-brief` prompt |
| What's on, who's playing | `schedule_search` (each row lists venue and musicians), `schedule_get` for one show |
| Staffing gaps | `staffing_check`, `availability_check` |
| Revenue and margin | `show_pnl`, `revenue_contract` |
| Invoices owed | `payroll_outstanding` |
| Card-statement backlog | `reconciliation_status` |
| Who changed what | `audit_recent` |
| Schedule emails waiting for review | `schedule_review_queue` |

## Writing for a CEO

Lead with one headline sentence. Then one line per area, plain words, no tool names or raw tables unless asked. End with what needs a decision and who owns it.

## Changing the schedule

Allowed: moving people on and off a show (`iba_assign_event_musician`, `iba_remove_event_musician`), changing a show's details or status (`iba_update_d1_event`, `iba_set_event_status`), adding a show (`iba_create_d1_event`), and pushing changes to the calendar (`iba_outlook_sync_event`).

1. Look the show up first and say exactly what will change, before → after.
2. Wait for an explicit yes. One change at a time.
3. After the change, offer the calendar push.

The same permission also covers bulk schedule tools and creating venues, bands, contracts and people. Do not reach for those unless asked for by name — that is the operations team's work.

## Not here

Pay rates, money, invoices, reconciliation and anything about how people are paid are read-only. When asked to change one, say who owns it (finance for pay and reconciliation, IBA's technical lead for anything technical) and offer to file a report with `file_session_report`.
