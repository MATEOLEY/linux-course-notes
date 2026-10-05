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

## Key Takeaway

The Linux filesystem starts at `/`, and each directory has a specific purpose.

Understanding directories such as `/bin`, `/dev`, `/etc`, `/home`, `/lib`, `/media`, and `/mnt` is important for navigating Linux systems and locating binaries, configuration files, devices, libraries, and mounted filesystems.
