# Linux ACL

Standard permissions (owner/group/others) aren't always enough. ACL lets you give a specific user or group access to a file without changing the owner or primary group.

---

## Detecting ACL

```bash
ls -l
```

Without ACL:
```text
-rw-r-----
```

With ACL:
```text
-rw-r-----+
```

The `+` means extended ACL entries exist.

---

## Viewing ACL

```bash
getfacl file.txt
```

Example output:
```text
# file: file.txt
# owner: ali
# group: developers
user::rw-
user:ahmet:r--
group::r--
mask::r--
other::---
```

| Entry | Meaning |
| ------ | ------- |
| `user::` | File owner's permissions |
| `user:ahmet:` | ACL for a specific user |
| `group::` | Group permissions |
| `mask::` | Maximum effective ACL permissions |
| `other::` | Everyone else |

---

## Adding ACL

```bash
# Read only
setfacl -m u:ahmet:r file.txt

# Read + write
setfacl -m u:ahmet:rw file.txt

# Full access
setfacl -m u:ahmet:rwx file.txt

# Group
setfacl -m g:developers:rw file.txt
```

Syntax: `setfacl -m u:<user>:<perms> <file>`

---

## Removing ACL

```bash
# Remove one user's ACL
setfacl -x u:ahmet file.txt

# Remove all ACL entries — back to standard permissions
setfacl -b file.txt
```

---

## Default ACL

New files inside a directory can inherit ACL automatically.

```bash
setfacl -d -m u:ahmet:rwx project/
```

Every file created inside `project/` will inherit this entry.

```bash
getfacl project/
```

```text
default:user::rwx
default:user:ahmet:rwx
default:group::r-x
default:mask::rwx
default:other::r-x
```

---

## ACL vs Standard Permissions

| | Standard | ACL |
| --- | --- | --- |
| Users | One owner | Multiple |
| Groups | One group | Multiple |
| Flexibility | Limited | Fine-grained |

---

## Cheat Sheet

```
getfacl <file>              → View ACL
setfacl -m u:<u>:<p> <f>   → Add / modify user ACL
setfacl -m g:<g>:<p> <f>   → Add / modify group ACL
setfacl -x u:<u> <f>       → Remove one entry
setfacl -b <f>              → Remove all ACL entries
setfacl -d -m u:<u>:<p> <d> → Set default ACL on directory
```
