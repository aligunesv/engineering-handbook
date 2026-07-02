# Linux systemd

`systemd` is Linux's init system and service manager. It is responsible for starting the operating system, managing background services (daemons), handling dependencies, and controlling the system state.

---

## Service Management

Check service status:

```bash
systemctl status nginx
```

Start a service:

```bash
systemctl start nginx
```

Stop a service:

```bash
systemctl stop nginx
```

Restart a service:

```bash
systemctl restart nginx
```

Reload configuration without restarting:

```bash
systemctl reload nginx
```

---

## Enable / Disable at Boot

Start automatically when the system boots:

```bash
systemctl enable nginx
```

Disable automatic startup:

```bash
systemctl disable nginx
```

Enable and start immediately:

```bash
systemctl enable --now nginx
```

---

## Checking Service State

Is the service running?

```bash
systemctl is-active nginx
```

Example:

```text
active
```

Is the service enabled at boot?

```bash
systemctl is-enabled nginx
```

Example:

```text
enabled
```

---

## Listing Services

Show all active services:

```bash
systemctl list-units --type=service
```

Show all installed service units:

```bash
systemctl list-unit-files --type=service
```

---

## Viewing Logs

View all system logs:

```bash
journalctl
```

View logs for a specific service:

```bash
journalctl -u nginx
```

Follow logs in real time:

```bash
journalctl -u nginx -f
```

Show logs from the current boot:

```bash
journalctl -b
```

---

## Service Unit Files

Systemd services are defined using **unit files**.

Common locations:

```text
/etc/systemd/system/
/usr/lib/systemd/system/
```

Example:

```text
nginx.service
```

---

## Example Service File

```ini
[Unit]
Description=Python API

[Service]
User=ubuntu
WorkingDirectory=/opt/api
ExecStart=/usr/bin/python3 app.py
Restart=always

[Install]
WantedBy=multi-user.target
```

---

## Unit Sections

### `[Unit]`

General information and dependencies.

Example:

```ini
Description=Python API
After=network.target
```

Common directives:

| Directive | Purpose |
| ---------- | ------- |
| `Description=` | Service description |
| `After=` | Start after another unit |
| `Requires=` | Required dependency |
| `Wants=` | Optional dependency |

---

### `[Service]`

Defines how the service runs.

Common directives:

| Directive | Purpose |
| ---------- | ------- |
| `ExecStart=` | Command to execute |
| `WorkingDirectory=` | Working directory |
| `User=` | Run as user |
| `Group=` | Run as group |
| `Restart=` | Restart policy |
| `Environment=` | Environment variables |

---

### `[Install]`

Defines when the service should be enabled.

Most common:

```ini
WantedBy=multi-user.target
```

---

## Reloading systemd

After creating or modifying a unit file:

```bash
systemctl daemon-reload
```

Reloads systemd so it recognizes new or updated unit files.

---

## Targets

Targets are collections of units that represent a system state.

Common targets:

| Target | Purpose |
| ------- | ------- |
| `multi-user.target` | Multi-user command-line system |
| `graphical.target` | Graphical desktop environment |
| `rescue.target` | Single-user rescue mode |
| `reboot.target` | Reboot system |
| `poweroff.target` | Shut down system |

Check current target:

```bash
systemctl get-default
```

Change default target:

```bash
systemctl set-default graphical.target
```

---

## Creating a Custom Service

Create a unit file:

```text
/etc/systemd/system/myapp.service
```

Reload systemd:

```bash
systemctl daemon-reload
```

Enable service:

```bash
systemctl enable myapp
```

Start service:

```bash
systemctl start myapp
```

Check status:

```bash
systemctl status myapp
```

---

## Service Lifecycle

```text
Create service file
        │
        ▼
systemctl daemon-reload
        │
        ▼
systemctl enable myapp
        │
        ▼
systemctl start myapp
        │
        ▼
systemctl status myapp
        │
        ▼
journalctl -u myapp -f
```

---

## Common Restart Policies

| Policy | Behavior |
| -------- | -------- |
| `no` | Never restart |
| `always` | Always restart |
| `on-failure` | Restart only on failure |
| `on-abnormal` | Restart after abnormal termination |

Example:

```ini
Restart=on-failure
```

---

## Cheat Sheet

```
systemctl status <service>          → Show service status
systemctl start <service>           → Start service
systemctl stop <service>            → Stop service
systemctl restart <service>         → Restart service
systemctl reload <service>          → Reload configuration
systemctl enable <service>          → Enable at boot
systemctl disable <service>         → Disable at boot
systemctl enable --now <service>    → Enable and start
systemctl is-active <service>       → Check running state
systemctl is-enabled <service>      → Check boot status
systemctl list-units --type=service → List running services
systemctl daemon-reload             → Reload unit files
journalctl                          → View system logs
journalctl -u <service>             → Service logs
journalctl -u <service> -f          → Follow logs
```
