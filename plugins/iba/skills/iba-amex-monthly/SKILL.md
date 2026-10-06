---
name: iba-amex-monthly
description: Use for IBA Music's monthly company-card reconciliation — importing the new Amex statement, matching it to receipts, categorizing, and reporting what still needs a person. "Run the monthly Amex reconciliation", "the new statement is in", "close out last month's card", or a scheduled monthly run.
---

# Monthly Amex reconciliation

One statement a month becomes reconciled, categorized expense lines, and a short list of exceptions for a person. Designed to run unattended; the same steps work in conversation.

**Read `iba://guide/expense-reconciliation` before starting.** It says how statements and receipts arrive, the exact sequence, and the autonomy contract — what may be confirmed automatically and what must be escalated. Follow it over anything here. The guided prompt `expense-reconciliation-monthly` runs the same loop.

## Outline

1. **Find the statement email** for the period (`mail_search_inbox`, then `mail_list_attachments`). Expect several attachments, including more than one CSV.
2. **Preview every CSV** with `preview_statement_attachment` — it writes nothing. Import only the one that is importable and covers a single cycle; a file at the row cap is the multi-month export, never the statement.
3. **Import** with `ingest_statement_from_email`. A period-overlap refusal means the wrong file — go back to step 2.
4. **Match:** `expense_trigger_inbox_match` if receipts may have arrived since the daily run, then `expense_auto_match` for the statement.
5. **Review:** `reconciliation_status` — lines needing a receipt, receipts to review, matched lines not yet categorized.
6. **Categorize only what you are sure of:** `expense_categories_list` for valid ids, then `categorize_expense` and `set_line_workflow`. Unsure → leave it and list it.
7. **Report the exceptions** with `file_session_report` — one report per run.

## Never

- Reverse a match or send a reminder on an unattended run — report it instead.
- Invent an amount, date, vendor or category.
- Mark a line complete with a guessed category.
