# Exchange Migration Overview

Notes from Exchange On-Prem to Microsoft 365 migration work.

The core goal is simple: move mailboxes and mail flow to Exchange Online without breaking client access, mail routing, or SMTP identities. In practice it's rarely that clean.

---

## Environment scope (example)

- Source: Exchange On-Premises
- Target: Exchange Online
- ~400 mailboxes

Numbers vary per project but the risk areas stay the same.

---

## What to verify before touching anything

- Exchange version and CU level
- SMTP domains and accepted domains
- Send/Receive connectors
- SMTP relay dependencies (printers, apps, scripts)
- Shared mailboxes and distribution groups
- Public folders (if they still exist)
- Mailbox sizes — large ones cause problems
- DNS config
- AD Connect sync status

---

## Objectives

- Preserve primary SMTP addresses
- No mailbox data loss
- Minimize user impact during cutover
- Keep mail flowing during transition
- Validate everything before closing the window
- Have a rollback plan ready — not just written down

---

## Migration flow

1. Assess the existing environment
2. Export Exchange config (connectors, rules, certs, permissions)
3. Validate identities and mail flow
4. Prepare DNS changes (lower TTL early)
5. Migrate mailboxes
6. Validate mail flow and client access
7. Clean up and decommission on-prem components

---

## Where things usually go wrong

- SMTP address mapping errors
- DNS cutover timing
- SMTP relay apps that weren't documented
- Outlook profile issues post-cutover
- Autodiscover not resolving correctly
- Mail flow gaps during the transition window
- Large mailbox migrations taking longer than the maintenance window

Check all of these before the cutover window, not during it.
