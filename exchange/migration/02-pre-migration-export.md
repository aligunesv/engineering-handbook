# Exchange Pre-Migration Export

Export current Exchange config before touching anything. These files are the reference point if something breaks post-migration and you need to compare states or recreate a config.

---

## Output folder

```powershell
$Path = "$env:USERPROFILE\Desktop\Migration-Before"
New-Item -ItemType Directory -Path $Path -Force
```

---

## Mailboxes

```powershell
# Full inventory with size and last logon
Get-Mailbox -ResultSize Unlimited |
Get-MailboxStatistics |
Select DisplayName, TotalItemSize, ItemCount, LastLogonTime |
Export-Csv "$Path\Mailboxes.csv" -NoTypeInformation -Encoding UTF8

# Largest mailboxes — sort these out before migration, they'll hold up batches
Get-Mailbox -ResultSize Unlimited |
Get-MailboxStatistics |
Sort-Object TotalItemSize -Descending |
Select DisplayName, TotalItemSize, ItemCount |
Export-Csv "$Path\Largest-Mailboxes.csv" -NoTypeInformation -Encoding UTF8

# Shared mailboxes
Get-Mailbox -RecipientTypeDetails SharedMailbox |
Select Name, PrimarySmtpAddress |
Export-Csv "$Path\Shared-Mailboxes.csv" -NoTypeInformation -Encoding UTF8

# GUID mapping — needed for migration validation
Get-Mailbox -ResultSize Unlimited |
Select Name, Alias, PrimarySmtpAddress, ExchangeGuid |
Export-Csv "$Path\Mailboxes-GUID.csv" -NoTypeInformation -Encoding UTF8

# All SMTP addresses including secondary ones
Get-Mailbox -ResultSize Unlimited |
Select Name, PrimarySmtpAddress, EmailAddresses |
Export-Csv "$Path\SMTPAddresses.csv" -NoTypeInformation -Encoding UTF8
```

---

## Groups

```powershell
# Distribution groups
Get-DistributionGroup |
Select Name, PrimarySmtpAddress |
Export-Csv "$Path\DistributionGroups.csv" -NoTypeInformation -Encoding UTF8

# Group members
$Result = foreach ($Group in Get-DistributionGroup) {
    Get-DistributionGroupMember $Group.Identity |
    Select @{
        Name = "GroupName"
        Expression = { $Group.Name }
    }, Name, PrimarySmtpAddress
}

$Result |
Export-Csv "$Path\DistributionGroupMembers.csv" -NoTypeInformation -Encoding UTF8
```

---

## Permissions

```powershell
# Full Access permissions
Get-Mailbox -ResultSize Unlimited |
Get-MailboxPermission |
Export-Csv "$Path\MailboxPermissions.csv" -NoTypeInformation -Encoding UTF8

# Send As
Get-RecipientPermission |
Export-Csv "$Path\RecipientPermissions.csv" -NoTypeInformation -Encoding UTF8
```

---

## Mail Flow

```powershell
# Transport rules — Format-List * so nothing gets cut off
Get-TransportRule |
Format-List * |
Out-File "$Path\TransportRules.txt"

# Accepted domains
Get-AcceptedDomain |
Select Name, DomainName, DomainType |
Export-Csv "$Path\AcceptedDomains.csv" -NoTypeInformation -Encoding UTF8

# Remote domains
Get-RemoteDomain |
Format-List * |
Out-File "$Path\RemoteDomains.txt"

# Connectors
Get-SendConnector |
Format-List * |
Out-File "$Path\SendConnectors.txt"

Get-ReceiveConnector |
Format-List * |
Out-File "$Path\ReceiveConnectors.txt"
```

---

## Certificates

```powershell
Get-ExchangeCertificate |
Format-List * |
Out-File "$Path\ExchangeCertificates.txt"
```

---

## Client Access

```powershell
Get-AutodiscoverVirtualDirectory |
Format-List * |
Out-File "$Path\AutodiscoverVirtualDirectory.txt"

Get-ClientAccessService |
Format-List * |
Out-File "$Path\ClientAccessServices.txt"
```

---

## Server Health

```powershell
Get-ServerHealth |
Export-Csv "$Path\ServerHealth.csv" -NoTypeInformation -Encoding UTF8
```

---

## Manual — record these before cutover

- MX record (current value + TTL)
- SPF record
- DKIM config
- DMARC policy
- Autodiscover record
- SMTP relay setup (which apps, which IP, which port)
- Printers and scanners using Exchange as relay

Keep these exports until post-migration validation is done and closed.
