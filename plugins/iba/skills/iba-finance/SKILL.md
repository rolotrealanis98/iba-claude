---
name: iba-finance
description: Use for IBA Music finance work through the IBA connector — verifying a musician's, contractor's or audio tech's invoice against the schedule, correcting the event or rate behind it, payroll checks, who hasn't invoiced, invoice reminders, receipt and Amex statement reconciliation, categorizing expenses, and summaries for the accountant. "Verify Juan's invoice", "reconcile last month's receipts", "who hasn't sent an invoice yet?"
---

# IBA finance

Payroll for musicians, contractors and audio techs, and expense reconciliation for the accountant. Start with `whoami` and `iba://guide/my-role`; deeper references are `iba://guide/expense-reconciliation`, `iba://guide/invoice-tracker` and `iba://guide/rates-and-payroll`.

## Guided prompts — offer these first

`receipt-reconciliation` · `payroll-verification` · `unpaid-this-period` · `chase-this-weeks-invoices` · `expense-summary-for-accountant` · `expense-reconciliation-monthly` · `statement-revenue-cycle`

## Quick reference

| Ask | Tools |
|---|---|
| Verify an invoice | `cross_check_invoice` — it cites the rate source per line (event override vs contract); report it, do not conclude on your own |
| Invoice details | `lookup_invoice_submission`, `lookup_audio_tech_invoice`, `get_musician_rates`, `money_contract`, `reimbursement_lookup` |
| Who still owes an invoice | `payroll_outstanding`, `invoice_tracker_status`; then `send_invoice_reminder` per person, confirmed one at a time (capped at one a day per person) |
| Size the receipt backlog | `reconciliation_status` for the period |
| Find a match | `expense_search` (entity `receipt` or `statement_line`), `expense_get`, `receipt_read_file` |
| Apply a match | `match_receipt` / `reconcile_statement_line`; `set_statement_line_no_receipt` when it genuinely has none; `categorize_expense` / `categorize_receipt` |
| Find the invoice or receipt in email | `mail_search_inbox` → `mail_get_message` → `mail_list_attachments` (own inbox). Invoices also land in a shared invoices mailbox — `iba://guide/my-role` says which, and the Microsoft 365 connector can reach it if connected |

## Reconcile: email → match → confirm → apply

1. Find the invoice or receipt and read out vendor, amount, date and what it was for.
2. Find the statement line that matches (merchant, amount, nearby date).
3. Show the proposed match side by side with your confidence and the exact before → after. Wait for "yes".
4. Apply only after the yes. Every write shows before/after and can be reversed.
5. Keep a numbered checklist in the chat — ✅ done, ⏳ in progress, ❓ needs a decision — and end each batch of 5–10 with: matched, set to no-receipt, and what needs their eyes and why.

## Fixing what a check turns up

When an invoice check shows the schedule or a rate is wrong, fix the data — then re-run `cross_check_invoice`.

| Wrong | Fix |
|---|---|
| Show details, times, venue, notes | `iba_update_d1_event` |
| Who played | `iba_assign_event_musician` / `iba_remove_event_musician` (audio techs: `iba_assign_event_audio_tech` / `iba_remove_event_audio_tech`) |
| A show that did not happen | `iba_set_event_status` (Cancelled) |
| A one-off rate for one show | `iba_set_event_musician_rate` / `iba_set_event_audio_tech_rate` |
| The standing rate on a contract | `iba_set_musician_contract_rate` / `iba_set_audio_tech_contract_rate` |

Every change shows before → after and waits for a yes. Offer `iba_outlook_sync_event` after a schedule change so the calendar matches. Rate rules: `iba://guide/rates-and-payroll`.

## Monthly statement

The whole monthly loop — import, match, categorize, report — is the `iba-amex-monthly` skill.

## Statement imports

Forward an Amex statement as a real file attachment on a new email, not Outlook's "Forward as attachment" — that arrives with no readable file. `import_statement_csv` asks for an acknowledged step; confirm it with the person.

## Working style

Explain what you are about to do in plain language before doing it, define jargon the first time (a *statement line* is one charge on the company card; *reconciling* matches it to its receipt), and suggest the next step.
