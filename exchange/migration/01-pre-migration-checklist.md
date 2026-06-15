# Pre-Migration Checklist

Things to verify before starting mailbox migration or DNS cutover. Go through this before every migration window — not the night before, ideally a week before so there's time to fix things.

---

## Identity & Directory

- [ ] Azure AD Connect sync is healthy
- [ ] No duplicate proxy addresses
- [ ] UPNs reviewed
- [ ] Mail-enabled objects syncing correctly
- [ ] Shared mailboxes identified
- [ ] Distribution groups documented

---

## Exchange Configuration

- [ ] Exchange version and CU level noted
- [ ] Accepted domains verified
- [ ] Send connectors exported
- [ ] Receive connectors exported
- [ ] Mail flow / transport rules documented
- [ ] Remote domains reviewed

---

## SMTP Relay

This is the one that gets missed. Talk to the sysadmins and application owners — not just IT.

- [ ] All SMTP relay dependencies identified
- [ ] Printers and scanners documented
- [ ] Application mail senders documented
- [ ] Existing relay config exported

---

## DNS

Lower TTL values at least 24-48 hours before cutover.

- [ ] MX records documented
- [ ] SPF record validated
- [ ] Autodiscover verified
- [ ] Current TTL values reviewed
- [ ] DNS cutover plan written

---

## Mailbox Readiness

- [ ] Largest mailboxes identified (these will slow down the migration batch)
- [ ] Mailboxes needing special handling noted
- [ ] Archive mailboxes reviewed
- [ ] Resource mailboxes documented
- [ ] Public folders assessed

---

## Client Access

- [ ] Outlook versions in use documented
- [ ] Autodiscover tested
- [ ] Outlook connectivity confirmed
- [ ] Mobile device impact assessed

---

## Microsoft 365 Side

- [ ] Licenses available and assigned
- [ ] Migration admin account working
- [ ] Exchange Online permissions confirmed
- [ ] Target domains verified in M365 admin

---

## Backup

- [ ] Latest full backup completed
- [ ] Restore tested (not just assumed to work)
- [ ] Recovery options documented

---

## Rollback

- [ ] Rollback procedure written and shared
- [ ] Previous DNS values recorded somewhere accessible
- [ ] Emergency contacts available
- [ ] Mail flow recovery steps ready
