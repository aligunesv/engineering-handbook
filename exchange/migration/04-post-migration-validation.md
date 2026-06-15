# Post-Migration Validation

Confirm that mailboxes, mail flow, and client access are working after migration. Test it — don't assume it's fine because the migration batch completed without errors.

---

## Mail Flow

Test all directions:

- Internal → Internal
- Internal → External
- External → Internal
- Shared mailboxes
- Distribution groups

Check message trace in M365 admin center. Look at delivery reports. If hybrid still exists, check on-prem queues too.

---

## SMTP Relay

Every application that was sending mail through Exchange needs to be confirmed working:

- Printers / scanners
- ERP / business applications
- Monitoring tools
- Internal scripts

Confirmed = message delivered, not just accepted by the relay. Check the receiving end.

---

## Client Access

- Outlook — create new profile if needed post-migration
- OWA
- Mobile devices (ActiveSync / native mail apps)
- Shared mailbox access
- Calendar sync

Watch for: repeated credential prompts (Autodiscover issue), missing mail (profile cache), calendar not syncing (permissions).

---

## Data Validation

Compare pre/post migration:

- Mailbox item counts reasonable?
- Folder structure intact?
- Shared mailbox access working?
- Send As / Full Access delegation intact?

If counts are off or permissions are missing, check migration logs and verify sync completed fully.

---

## Identity & Security

- SPF aligned correctly for Exchange Online
- DKIM signing active
- DMARC policy enforced
- Domain verified in M365
- Admin accounts accessible
- MFA working

DKIM breaks more often than expected post-migration. Verify it with a test message through mail-tester.com or similar.

---

## Monitoring

After cutover, keep an eye on:

- Exchange Online service health (M365 admin center)
- Message trace for anomalies
- Failed login attempts
- Connector errors if hybrid remains

---

## Done when

- All mailboxes accessible
- Mail flowing in all directions
- SMTP relay applications confirmed working
- No critical errors in message trace
- No open user-reported blocking issues
