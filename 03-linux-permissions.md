# Linux File Permissions

Linux uses file permissions to control who can read, modify, or execute files and directories.

Understanding permissions is important for Linux administration, security, and pentesting because incorrect permissions can allow unauthorized users to access, modify, or execute files.

---

## Viewing Permissions

File and directory permissions can be viewed using:

```bash
ls -l
```

Example:

```text
-rwxr-xr--
```

The permission string can be divided into four sections:

```text
- | rwx | r-x | r--
    │     │     │
    │     │     └── Others
    │     └──────── Group
    └────────────── Owner
```

The first character represents the type of filesystem object.

The remaining nine characters represent permissions for:

1. Owner
2. Group
3. Others

---

## File Type

The first character indicates the type of filesystem object.

```text
- = Regular file
d = Directory
```

Example:

```text
-rw-r--r--
```

The `-` indicates a regular file.

Example:

```text
drwxr-xr-x
```

The `d` indicates a directory.

> Other filesystem object types exist, but these are the ones covered so far.

---

## Permission Types

Linux uses three basic permissions:

| Permission | Meaning |
|---|---|
| `r` | Read |
| `w` | Write |
| `x` | Execute |

If a permission is not granted, a `-` appears in its position.

Example:

```text
r-x
```

This means:

- Read: allowed
- Write: not allowed
- Execute: allowed

---

## Permission Groups

Linux permissions are divided into three groups.

### Owner

The first three permissions belong to the user who owns the file.

```text
rwx
```

### Group

The next three permissions apply to the group associated with the file.

```text
r-x
```

### Others

The final three permissions apply to other users.

```text
r--
```

---

## Reading a Permission String

Consider the following permissions:

```text
-rwxr-xr--
```

Breaking them down:

```text
- | rwx | r-x | r--
    │     │     │
    │     │     └── Others
    │     └──────── Group
    └────────────── Owner
```

This means:

| Section | Permissions |
|---|---|
| Type | Regular file |
| Owner | Read, Write, Execute |
| Group | Read, Execute |
| Others | Read |

---

## `chmod`

`chmod` stands for **change mode**.

It is used to change the permissions of files and directories.

Basic syntax:

```bash
chmod <permissions> <file>
```

Permissions can be changed using different notations.

Two common methods are:

- Symbolic notation
- Numeric notation

---

## Symbolic Permissions

Symbolic notation identifies the user category and the permission that should be added, removed, or assigned.

Common user categories are:

| Symbol | Meaning |
|---|---|
| `u` | User / Owner |
| `g` | Group |
| `o` | Others |
| `a` | All |

Permission operators include:

| Operator | Meaning |
|---|---|
| `+` | Add permission |
| `-` | Remove permission |
| `=` | Set exact permissions |

For example:

```bash
chmod u+x script.sh
```

This means:

```text
u = User / Owner
+ = Add
x = Execute
```

Therefore, the command adds execute permission for the owner of `script.sh`.

Another example:

```bash
chmod o-w file.txt
```

This removes write permission from others.

---

## Numeric Permissions

Linux permissions can also be represented using numbers.

Each permission has a numeric value:

```text
r = 4
w = 2
x = 1
```

The values are added together to determine the permissions for each group.

### Common Values

| Value | Permissions | Meaning |
|---|---|---|
| `7` | `rwx` | Read, Write, Execute |
| `6` | `rw-` | Read, Write |
| `5` | `r-x` | Read, Execute |
| `4` | `r--` | Read |
| `0` | `---` | No permissions |

For example:

```text
rwx = 4 + 2 + 1 = 7
rw- = 4 + 2 = 6
r-x = 4 + 1 = 5
r-- = 4
```

---

## Understanding `chmod 755`

Example:

```bash
chmod 755 script.sh
```

Each number represents one permission group:

```text
7 | 5 | 5
│   │   │
│   │   └── Others
│   └────── Group
└────────── Owner
```

The permissions are:

```text
7 = rwx
5 = r-x
5 = r-x
```

Therefore:

```text
rwxr-xr-x
```

This means:

| User | Permissions |
|---|---|
| Owner | Read, Write, Execute |
| Group | Read, Execute |
| Others | Read, Execute |

---

## Understanding `chmod 644`

Another common permission configuration is:

```bash
chmod 644 file.txt
```

Breaking it down:

```text
6 = rw-
4 = r--
4 = r--
```

Result:

```text
rw-r--r--
```

This means:

- Owner can read and modify the file.
- Group can only read the file.
- Others can only read the file.

---

## Security Considerations

File permissions are an important part of Linux security.

Incorrect permissions can expose sensitive files or allow unauthorized modification or execution.

For example:

```bash
chmod 777 file
```

gives:

```text
rwxrwxrwx
```

This grants read, write, and execute permissions to everyone.

> **Security Note:** Avoid using `chmod 777` as a quick solution to permission problems. Giving every user full permissions can create unnecessary security risks.

When troubleshooting permissions, it is better to understand which user or group actually needs access and grant only the necessary permissions.

---

## Quick Reference

| Command / Value | Purpose |
|---|---|
| `ls -l` | View file and directory permissions |
| `chmod` | Change permissions |
| `r` | Read |
| `w` | Write |
| `x` | Execute |
| `u` | Owner |
| `g` | Group |
| `o` | Others |
| `a` | All users |
| `+` | Add permission |
| `-` | Remove permission |
| `=` | Set exact permissions |
| `7` | `rwx` |
| `6` | `rw-` |
| `5` | `r-x` |
| `4` | `r--` |
| `0` | `---` |

---

## Notes

- Permissions are separated into Owner, Group, and Others.
- `r`, `w`, and `x` represent Read, Write, and Execute.
- `chmod` modifies permissions.
- Permissions can be expressed symbolically or numerically.
- Numeric permissions are calculated using `r = 4`, `w = 2`, and `x = 1`.
- Avoid unnecessarily permissive configurations such as `777`.
