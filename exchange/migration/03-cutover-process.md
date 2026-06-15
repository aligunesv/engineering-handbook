# Migration Cutover Process

The cutover window is where mailbox migration finalizes and mail flow switches to Exchange Online. Keep the scope tight and avoid making unrelated changes during this window.

---

## Phase 1 — Pre-Cutover Validation

Before touching DNS or mail flow:

- All migration batches synchronized?
- Migration errors reviewed — no failed items left?
- Azure AD Connect sync healthy?
- M365 licenses assigned?
- Target mailboxes accessible?
- Rollback info available and accessible to everyone in the room?

Don't start Phase 2 if any of these are unresolved.

---

## Phase 2 — Final Mailbox Sync

- Run final delta sync
- Confirm mailbox moves completed
- No mailboxes stuck in failed state
- Review migration reports — note any warnings even if non-blocking

---

## Phase 3 — DNS Cutover

Changes to make:

- MX record → Exchange Online
- Autodiscover record → M365
- SPF record update if needed

After making changes:

- Verify MX propagation (`nslookup` or MXToolbox)
- Verify Autodiscover resolves correctly
- Don't assume propagation is done — check it

---

## Phase 4 — Mail Flow Validation

Test all directions:

- Internal → Internal
- Internal → External
- External → Internal
- Shared mailboxes
- Distribution groups

Use message trace in M365 admin center. Check Exchange Online queues. Don't move on until mail is confirmed flowing in both directions.

---

## Phase 5 — Client Validation

- Outlook (desktop)
- OWA
- Mobile devices
- Shared mailbox access
- Calendar

Users should be able to send, receive, and access existing mail. If Outlook is prompting for credentials repeatedly, Autodiscover is probably not resolving correctly yet.

---

## Phase 6 — SMTP Relay Validation

Test everything that sends mail through Exchange:

- Printers / scanners
- ERP systems
- Monitoring tools
- Internal scripts or services

This is the step that gets skipped and causes a ticket the next morning. Confirm delivery actually lands, not just that the relay accepted the message.

---

## Phase 7 — Done

Migration is complete when:

- Mailboxes accessible
- Mail flowing in all directions
- DNS verified
- SMTP relay working
- No open critical errors

---

## Rollback

If mail flow or auth issues can't be resolved within the maintenance window: stop, rollback DNS, restore previous config. Don't try to fix an unknown problem under time pressure during a cutover.

The rollback procedure should already be documented before this window starts.
