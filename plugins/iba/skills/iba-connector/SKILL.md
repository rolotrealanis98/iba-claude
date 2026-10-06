---
name: iba-connector
description: Use for anything involving IBA Music data — the schedule, musicians and techs, bands, venues, invoices, receipts, payroll, Disney bookings — and whenever the IBA tools are missing, not connected, or refusing ("I can't see the IBA tools", "it says not authorized", "connect IBA"). Covers starting a session, connecting, and the rules every IBA session follows.
---

# The IBA connector

IBA Music's data lives behind one connector, `https://mcp.ibamusic.com/mcp`. Each person signs in with their own `@ibamusic.com` Microsoft account, and what they can see and change follows their account, not the device.

## Start every involved session

1. `whoami` — who you are to the connector: role, access tier, write grants, focus.
2. Read the resource `iba://guide/my-role` — the playbook for that person's job.
3. Offer the guided prompts the connector lists for their focus (finance or operations).

Never assume what someone may change: the grants `whoami` reports are the only source.

## If the IBA tools are missing

| Where | Fix |
|---|---|
| claude.ai, Claude Desktop, phone | Customize → Connectors → **IBA** → **Connect**, then sign in with the `@ibamusic.com` Microsoft account. With this plugin installed, connect from the plugin's **Connectors** tab instead. Not listed at all? Add it from https://claude.ai/customize/connectors?modal=add-custom-connector&connectorName=IBA&connectorUrl=https%3A%2F%2Fmcp.ibamusic.com%2Fmcp |
| Claude Code | `/mcp` → select the IBA server → **Authenticate**. |

- "Your IBA account is not authorized for this connector" means the sign-in worked but the account is not set up on IBA's side. That is for IBA's technical lead to fix; do not retry.
- The connector address is `https://mcp.ibamusic.com/mcp`. If a connector was added with any other address, remove it and add it again from the install link.

## Rules for every IBA session

- **Reads are free; writes are confirmed.** Look things up without asking. Before any change, show exactly what will change (before → after) and wait for an explicit yes. Work in small batches.
- **Email is read-only and only the person's own inbox.** Nothing here sends email or touches a mailbox or calendar. A client reply is a draft the person pastes into Outlook themselves; never say a message was sent.
- **Never mark anything paid or settled.** No tool does it; do not imply one did.
- **When something does not add up, flag it — do not guess.** A wrong match is worse than an unmatched line.
- **A tool refuses, errors, or the data looks wrong:** offer to file a session report to IBA's technical lead with `file_session_report` (with the person's OK) rather than working around it.
