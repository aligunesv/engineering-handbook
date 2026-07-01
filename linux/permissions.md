# Linux File Permissions

## Basics

Every file and directory in Linux has:

- **Owner**
- **Group**
- **Others**

Each of these has its own permissions.

Permissions are:

- `r` → Read
- `w` → Write
- `x` → Execute

---

## Checking Permissions

```bash
ls -l
```

Example:

```text
drwxrwxr-x
-rw-rw-r--
```

Permission layout:

```text
d rwx rwx r-x
│ │   │   │
│ │   │   └── Others
│ │   └────── Group
│ └────────── Owner
└──────────── File type
```

First character:

- `d` → Directory
- `-` → Regular file

---

## Example

```text
-rw-rw-r--
```

Owner

- Read
- Write

Group

- Read
- Write

Others

- Read only

---

Another example:

```text
drwxrwxr-x
```

Owner

- Read
- Write
- Execute

Group

- Read
- Write
- Execute

Others

- Read
- Execute

No write permission.

---

## Numeric Permissions

Linux converts permissions into numbers.

| Permission | Value |
| ---------- | ----: |
| Read | 4 |
| Write | 2 |
| Execute | 1 |

Common combinations:

| Permission | Number |
| ---------- | ------ |
| `rwx` | 7 |
| `rw-` | 6 |
| `r-x` | 5 |
| `r--` | 4 |

Example:

```text
rw-rw-r--
```

Owner → `rw-` → 6

Group → `rw-` → 6

Others → `r--` → 4

Result:

```text
664
```

---

## chmod

Changes permissions.

```bash
chmod 755 script.sh
```

```text
rwxr-xr-x
```

Another example:

```bash
chmod 664 config.yaml
```

```text
rw-rw-r--
```

---

## chown

Changes ownership.

Owner only:

```bash
sudo chown aligunes file.txt
```

Owner + group:

```bash
sudo chown aligunes:developers file.txt
```

Check:

```bash
ls -l
```

---

## Common Permission Modes

### Files

| Mode | Usage |
| ----: | ----- |
| 644 | Default file |
| 664 | Group writable |
| 600 | Private file |
| 400 | Read-only private file |

### Directories

| Mode | Usage |
| ----: | ----- |
| 755 | Default directory |
| 775 | Group writable |
| 700 | Private directory |

---

## Directory Permissions

Permissions behave a little differently on directories.

`r`

- List files inside.

`w`

- Create, rename, delete files.

`x`

- Enter (`cd`) the directory.

Without `x`, you generally cannot access the directory even if you can read it.

---

## Secure Files

Private SSH keys or AWS `.pem` files should be restricted.

Example:

```bash
chmod 400 mykey.pem
```

Meaning:

- Owner → Read only
- Group → No access
- Others → No access

---

## Root-owned Files

Many system files are owned by `root`.

Example:

```bash
cd /etc
ls -l
```

Usually:

```text
root root
```

This prevents regular users from modifying critical system files.

---

## Commands to Remember

```bash
ls -l
```

View permissions.

```bash
chmod
```

Change permissions.

```bash
chown
```

Change owner/group.

---

## Quick Cheat Sheet

```
r = 4
w = 2
x = 1
```

```
7 = rwx
6 = rw-
5 = r-x
4 = r--
3 = -wx
2 = -w-
1 = --x
0 = ---
```

Most common:

```
644 → Default file

755 → Default directory

600 → Private file

400 → Read-only secret (SSH key, PEM)
```
