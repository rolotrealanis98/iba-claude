---
name: iba-operations
description: Use for IBA Music operations through the IBA connector — the schedule and who's playing, rosters and staffing gaps, availability, Disney booking ingest from booking-confirmation emails, new events and contracts, pushing events to the Outlook calendar, and drafting client replies. "What's on this weekend?", "who can cover Saturday?", "ingest the new Disney bookings".
---

# IBA operations

Schedules, rosters, Disney bookings and client communication. Start with `whoami` and `iba://guide/my-role`; deeper references are `iba://guide/operations`, `iba://guide/disney-booking-ingest`, `iba://reference/bands` and `iba://reference/venues`.

## Guided prompts — offer these first

`weekly-schedule-review` · `roster-gaps` · `coverage-check` · `draft-event-roster` · `collect-availability` · `event-intake` · `contract-intake` · `data-gaps-sweep`

## Quick reference

| Ask | Tools |
|---|---|
| What's on, who's playing | `schedule_search` (each row already lists venue and musicians — no `schedule_get` per row), `schedule_get` for one event in depth, `event_prep` |
| Find a person, band or venue | `directory_search` → `directory_get` |
| Who can cover a role | `staffing_check`, `availability_check` |
| Missing data | `data_gaps` |
| Change a roster, status or event | the `iba_*` event and roster tools — always after a confirmed plan |
| Push to the calendar | `iba_outlook_sync_event` after event changes (offer it) |
| Schedule emails waiting for review | the `iba-schedule-triage` skill (`schedule_review_queue`) |

## Availability means three things

An explicit Available/Partial answer is available; an explicit Unavailable is unavailable; **no answer is unconfirmed — presumed available, confirm before booking.** Never treat silence as unavailable.

## Disney booking ingest

Read `iba://guide/disney-booking-ingest` first.

1. `mail_search_inbox` for new booking confirmations — the guide names the sender to search for.
2. For each booking, `schedule_search` for an existing event before creating one.
3. Show what you plan to create or update and wait for the OK; then apply with the event tools.
4. Offer `iba_outlook_sync_event` for what changed.

## Event notes

`notes` is shown to performers: plain text only, and never client contact details — those go in `admin_notes`.

## Client replies — draft only

Read the thread with `mail_search_inbox` + `mail_get_message` and write the reply as plain text for the person to paste into Outlook. Nothing here can send it.

Pay rates and money are not operations work; point those questions to IBA's technical lead.
