# Common Migration Issues

Issues that come up repeatedly during Exchange → M365 migrations.

---

## Mail Delay

**Usual causes**
- DNS propagation still in progress
- Connector queue backlog on-prem
- Exchange Online throttling
- Transport service delay

**Where to look**
- Message trace in M365
- Exchange queue viewer (on-prem)
- Connector logs
- MX resolution — `nslookup -type=MX yourdomain.com 8.8.8.8`

**Fix**
Verify MX points to Exchange Online. Check connector health. If it's DNS, wait it out — there's no shortcut past TTL. If messages are queued on-prem, retry submission after MX is confirmed.

---

## Outlook Not Connecting

**Usual causes**
- Autodiscover not resolving to M365 yet
- Cached Outlook profile pointing to on-prem
- DNS SCP or virtual directory mismatch
- Credential cache

**Where to look**
- Test Autodiscover inside Outlook (hold Ctrl, right-click tray icon → Test Email AutoConfiguration)
- Check DNS for autodiscover record
- Exchange Online mailbox status in M365 admin
- Windows Credential Manager

**Fix**
Recreate the Outlook profile. Flush DNS cache. Validate Autodiscover DNS record. If the mailbox isn't fully provisioned in EXO yet, that'll cause this too.

---

## Missing Emails

**Usual causes**
- Transport rules silently filtering
- Spam quarantine
- User-side mailbox rules
- Message trace being misread (check the full time range)
- Journaling delay

**Where to look**
- M365 message trace — extended trace if outside 10-day window
- Quarantine portal
- Transport rule logs
- User's inbox rules

**Fix**
Check transport rules for anything that could match the affected messages. Check quarantine. If it's user inbox rules, that's on them but worth checking. Rerun the message trace with a wider time range before assuming the mail is actually lost.

---

## Large Mailbox Migration Failure

**Usual causes**
- M365 throttling the migration batch
- Corrupted items in the source mailbox
- Large attachments
- Network instability mid-sync

**Where to look**
- Migration batch report in M365 admin
- Exchange Online migration logs
- Error codes in the move request
- Item-level failure reports

**Fix**
Retry the batch. If it keeps failing, reduce batch size. Corrupted items can be excluded with `-BadItemLimit` if you're okay with the data loss. Give large mailboxes their own batch and a longer window.

---

## Notes

DNS, transport config, and identity issues usually aren't isolated — they show up together. Fix DNS first, then look at mail flow, then clients. Jumping straight to Outlook troubleshooting while DNS is still propagating wastes time.
