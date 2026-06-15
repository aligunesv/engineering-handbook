# Exchange

Running notes from Exchange environments. Mostly on-prem and hybrid, some Exchange Online.

Covers day-to-day operations and what actually breaks in production.

---

## Areas covered

- Mail flow — internal/external, connectors, queues
- SMTP relay (printers, apps, monitoring tools)
- Mailbox operations
- Migration (On-Prem → M365)
- Hybrid coexistence
- Auth, certificates, SPF/DKIM/DMARC
- Incident troubleshooting

---

## Mail flow

Everything depends on Transport service, Send/Receive connectors, DNS, and queues. When mail stops flowing, it's almost always one of those four.

Most common culprits: connector misconfiguration, DNS resolution failure, auth issue, queue backlog.

---

## Migration

Standard flow: inventory → identity validation (SMTP/GUID) → mailbox move → DNS cutover → client and relay validation.

The dangerous parts are DNS cutover, client reconfiguration, and hybrid coexistence period. Most issues cluster there.

---

## Security

SPF, DKIM, DMARC, transport rules, anti-spam, certificates. Certificates expire quietly. SPF breaks after domain changes. DKIM signing tends to break post-migration if you're not watching.

---

## When something breaks

Start with message trace. Then DNS. Then connectors. Then queue state. Then certs/auth.

Almost everything fits into one of those buckets.
