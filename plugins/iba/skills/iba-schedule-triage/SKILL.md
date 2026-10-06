---
name: iba-schedule-triage
description: Use to work IBA Music's schedule-email review queue end to end — when asked to "work the schedule queue", "run the schedule review", "check the schedule emails", "are we up to date with the schedule?", or when a monthly lineup email needs to reach the rosters. Needs the schedule write grant.
---

# Schedule triage

Band schedules arrive by email and are ingested into a review queue every few minutes. Only guardrailed nights are applied automatically; everything else waits for a reviewer. You are that reviewer. **The email is the source of truth; the queue is a proposal.**

**Read `iba://guide/schedule-triage` before starting.** It holds the full procedure, the judgment calls, the name-resolution rules and the report format. This skill is the outline.

## Outline

1. **Ground.** `whoami` — stop if the `schedule` grant is missing. `schedule_review_sync`, then compare its watermark with the newest schedule email. `schedule_review_health` if something looks stuck.
2. **Read the queue.** `schedule_review_queue`. Nothing pending and the watermark is current → report "up to date" and stop.
3. **Read each email** with proposals or findings (`mail_search_inbox`, `mail_get_message`) — the current message only, never the quoted history.
4. **Verify every night**, not just the parser's diff: `schedule_get` for every event in the email's range, and compare the email's lineup with the live roster.
5. **Write rosters, removals first:** `iba_remove_event_musician`, then one `iba_assign_event_musicians_bulk` with every add. Report overlap and availability warnings verbatim.
6. **Record:** `schedule_review_resolve` (applied only for what you wrote; dismissed for what the email no longer supports), then `schedule_review_acknowledge` for findings you handled.
7. **Sync and re-read:** `iba_outlook_sync_pending`, then `schedule_review_queue` again.

## Never

- Resolve a change as applied without having written the roster.
- Apply a change whose night you did not verify against the email body.
- Touch past dates; report them instead.
