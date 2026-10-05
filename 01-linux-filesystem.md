# Linux Filesystem Structure

Linux organizes its filesystem using a hierarchical directory structure that starts from the root directory `/`.

Below are some of the main directories and their purposes.

## `/bin` - Essential User Binaries

Contains essential command binaries used by the system and users.

Some common commands associated with this directory include:

```bash
ls
cat
mkdir
cp
mv
```

> **Note:** On many modern Linux distributions, `/bin` is a symbolic link to `/usr/bin`.

---

## `/dev` - Device Files

Contains special files that represent hardware devices and other system devices.

Examples include:

```text
/dev/sda
/dev/null
/dev/tty
```
  
Linux can interact with many devices through these special files.

---

## `/etc` - System Configuration

Contains system-wide configuration files.

Examples of configuration files and directories found here include:

```text
/etc/passwd
/etc/hosts
/etc/ssh/
/etc/network/
```

Many system configuration files require elevated privileges to modify.

For example:

```bash
sudo nano /etc/hosts
```

---

## `/home` - User Home Directories

Contains the personal directories of regular users.

For example:

```text
/home/mateo/
```

A user's home directory may contain directories such as:

```text
Desktop/
Documents/
Downloads/
Pictures/
```

It also contains hidden configuration files and directories.

---

## `/lib` - Essential Shared Libraries

Contains essential shared libraries required by system binaries and programs.

These libraries provide functionality that programs can reuse instead of implementing everything themselves.

> **Note:** The exact organization may vary between Linux distributions and architectures.

---

## `/media` - Removable Media

Commonly used as a mount point for removable devices such as:

- USB drives
- External drives
- Optical media

For example, a USB drive may become accessible somewhere under:

```text
/media/
```

---

## `/mnt` - Temporary Mount Point

Traditionally used to temporarily mount filesystems or partitions.

For example:

```bash
sudo mount /dev/sdb1 /mnt
```

This makes the filesystem located on `/dev/sdb1` accessible through `/mnt`.

---
---

## `/opt` - Optional Software

Used for installing optional or third-party software packages that are not part of the default system installation.

Applications installed here often have their own subdirectory.

For example:

```text
/opt/application/
/opt/tool/
```

This helps keep additional software separated from the core system files.

---

## `/root` - Root User Home Directory

The home directory of the `root` user, which is the system administrator account with the highest privileges.

```text
/root/
```

Unlike regular users, whose home directories are usually located under `/home`, the root user's home directory is located directly under `/`.

For comparison:

```text
/home/mateo/    → Regular user
/root/          → Root user
```

---

## `/sbin` - System Administration Binaries

Contains binaries primarily used for system administration and maintenance tasks.

Historically, these commands were mainly intended to be executed by the `root` user or users with elevated privileges.

> **Note:** On many modern Linux distributions, `/sbin` may be a symbolic link to `/usr/sbin`.

---

## `/srv` - Service Data

Contains data used or provided by services running on the system.

For example, a server may store data related to services such as:

```text
/srv/www/
/srv/ftp/
```

The exact structure depends on the services configured on the system.

---

## `/tmp` - Temporary Files

Used by applications and the operating system to store temporary files.

```text
/tmp/
```

Files stored here are generally not intended for permanent storage and may be automatically deleted by the system.

Because many users and applications can use `/tmp`, its permissions and contents can also be relevant when analyzing the security of a Linux system.

---

## `/usr` - User System Resources

Contains a large portion of the programs, libraries, documentation, and other read-only resources used by the system and its users.

Some important subdirectories include:

```text
/usr/bin/       → Most user commands
/usr/sbin/      → System administration commands
/usr/lib/       → Libraries
/usr/share/     → Architecture-independent shared data
/usr/local/     → Locally installed software
```

> **Note:** Despite its name, `/usr` is not the directory where individual user files are stored. Personal user files are normally located under `/home`.

---

## `/var` - Variable Data

Contains data that is expected to change while the system is running.

Common examples include:

```text
/var/log/       → System and application logs
/var/cache/     → Cached data
/var/lib/       → Application state and databases
/var/spool/     → Queued data and tasks
```

For example, system logs can often be found under:

```text
/var/log/
```

This directory can be particularly useful when troubleshooting or analyzing activity on a Linux system.

## Key Takeaway

The Linux filesystem starts at `/`, and each directory has a specific purpose.

Understanding directories such as `/bin`, `/dev`, `/etc`, `/home`, `/lib`, `/media`, and `/mnt` is important for navigating Linux systems and locating binaries, configuration files, devices, libraries, and mounted filesystems.
