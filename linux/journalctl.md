# Linux journalctl

`journalctl` is the command-line utility used to view logs collected by **systemd-journald**. It provides centralized logging for the Linux system, including the kernel, services, and applications managed by systemd.

---

## Viewing Logs

Show all logs:

```bash
journalctl
```

Show the newest logs first:

```bash
journalctl -r
```

Show only the last 20 lines:

```bash
journalctl -n 20
```

Follow logs in real time:

```bash
journalctl -f
```

---

## Viewing Service Logs

Show logs for a specific service:

```bash
journalctl -u nginx
```

Multiple services:

```bash
journalctl -u nginx -u ssh
```

Follow logs in real time:

```bash
journalctl -u nginx -f
```

---

## Filtering by Boot

Show logs from the current boot:

```bash
journalctl -b
```

Show logs from the previous boot:

```bash
journalctl -b -1
```

List available boots:

```bash
journalctl --list-boots
```

Example:

```text
-2  8a7b3...  Tue 2025-07-01
-1  4d5e2...  Wed 2025-07-02
 0  f1c8a...  Thu 2025-07-03
```

---

## Filtering by Time

Logs since a specific time:

```bash
journalctl --since "2025-07-01"
```

Last hour:

```bash
journalctl --since "1 hour ago"
```

Today:

```bash
journalctl --since today
```

Between two times:

```bash
journalctl --since "09:00" --until "11:00"
```

---

## Filtering by Priority

| Priority | Description |
| -------- | ----------- |
| `0` | Emergency |
| `1` | Alert |
| `2` | Critical |
| `3` | Error |
| `4` | Warning |
| `5` | Notice |
| `6` | Info |
| `7` | Debug |

Show only errors:

```bash
journalctl -p err
```

Warnings and higher:

```bash
journalctl -p warning
```

Only critical messages:

```bash
journalctl -p crit
```

---

## Kernel Logs

Show kernel messages:

```bash
journalctl -k
```

Kernel logs from current boot:

```bash
journalctl -k -b
```

---

## Filtering by User

Show logs for the current user:

```bash
journalctl --user
```

Show logs for a user service:

```bash
journalctl --user -u myservice
```

---

## Output Formats

Default output:

```bash
journalctl
```

Without paging:

```bash
journalctl --no-pager
```

Short ISO timestamps:

```bash
journalctl -o short-iso
```

JSON output:

```bash
journalctl -o json
```

Verbose output:

```bash
journalctl -o verbose
```

---

## Disk Usage

Show journal disk usage:

```bash
journalctl --disk-usage
```

Example:

```text
Archived and active journals take up 320.0M on disk.
```

---

## Cleaning Old Logs

Keep only the last 7 days:

```bash
journalctl --vacuum-time=7d
```

Limit logs to 500 MB:

```bash
journalctl --vacuum-size=500M
```

Keep only the newest 5 journal files:

```bash
journalctl --vacuum-files=5
```

---

## Useful Examples

Show SSH logs:

```bash
journalctl -u ssh
```

Show Docker logs:

```bash
journalctl -u docker
```

Show logs since yesterday:

```bash
journalctl --since yesterday
```

Show today's errors:

```bash
journalctl --since today -p err
```

Show logs without pagination:

```bash
journalctl --no-pager
```

---

## Common Options

| Option | Purpose |
| ------- | ------- |
| `-u` | Filter by service |
| `-b` | Filter by boot |
| `-k` | Kernel logs |
| `-f` | Follow logs |
| `-n` | Show last N lines |
| `-p` | Filter by priority |
| `--since` | Start time |
| `--until` | End time |
| `-o` | Output format |
| `-r` | Reverse order |

---

## Cheat Sheet

```
journalctl                         → Show all logs
journalctl -f                      → Follow logs
journalctl -r                      → Newest logs first
journalctl -n 50                   → Last 50 lines
journalctl -u <service>            → Logs for a service
journalctl -u <service> -f         → Follow service logs
journalctl -b                      → Current boot logs
journalctl -b -1                   → Previous boot logs
journalctl --list-boots            → List boots
journalctl --since today           → Today's logs
journalctl --since "1 hour ago"    → Last hour
journalctl -p err                  → Error logs
journalctl -k                      → Kernel logs
journalctl --disk-usage            → Journal size
journalctl --vacuum-time=7d        → Remove logs older than 7 days
journalctl --no-pager              → Disable pager
journalctl -o json                 → JSON output
```
