# Windows Services

Windows Services are background processes managed by the Service Control Manager (SCM). They start automatically, manually, or on demand and provide core operating system and application functionality.

---

## Managing Services

Open the Services console:

```text
services.msc
```

List services with PowerShell:

```powershell
Get-Service
```

Get a specific service:

```powershell
Get-Service Spooler
```

---

## Starting and Stopping Services

Start a service:

```powershell
Start-Service Spooler
```

Stop a service:

```powershell
Stop-Service Spooler
```

Restart a service:

```powershell
Restart-Service Spooler
```

---

## Service Startup Types

| Startup Type | Description |
|--------------|-------------|
| Automatic | Starts during system boot |
| Automatic (Delayed Start) | Starts shortly after boot |
| Manual | Starts only when requested |
| Disabled | Cannot be started |

---

## Checking Service Status

```powershell
Get-Service | Where-Object Status -eq Running
```

Show all stopped services:

```powershell
Get-Service | Where-Object Status -eq Stopped
```

---

## Configure Startup Type

```powershell
Set-Service Spooler -StartupType Automatic
```

Disable a service:

```powershell
Set-Service Spooler -StartupType Disabled
```

---

## Using sc.exe

Query service:

```cmd
sc query Spooler
```

Start service:

```cmd
sc start Spooler
```

Stop service:

```cmd
sc stop Spooler
```

---

## Troubleshooting

Useful Event Viewer log:

```
Windows Logs
└── System
```

Useful commands:

```powershell
Get-Service
Get-WinEvent
```

---

## Cheat Sheet

```text
Get-Service
Start-Service
Stop-Service
Restart-Service
Set-Service
sc query
sc start
sc stop
services.msc
```
