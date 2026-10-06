# Basic Linux Commands

This section contains basic Linux commands learned during the course. It includes commands for user information, privilege management, navigation, file and directory management, output redirection, help, and package management.

---

## User Information

### `whoami`

Displays the username of the current user.

```bash
whoami
```

### `id`

Displays information about the current user, including:

- User ID (UID)
- Group ID (GID)
- Groups the user belongs to

```bash
id
```

### `passwd`

Changes the password of a user.

When executed without specifying another user, it changes the password of the current user.

```bash
passwd
```

---

## Privileges and Users

### `sudo`

Executes a command with elevated privileges, usually as the `root` user.

```bash
sudo <command>
```

Example:

```bash
sudo apt update
```

> `sudo` does not permanently switch the current user to root. It executes the specified command with elevated privileges when the user is authorized to do so.

### `su`

Switches to another user account.

```bash
su <username>
```

A login shell can be started using:

```bash
su - <username>
```

---

## Terminal Shortcuts

### Up Arrow `↑`

Cycles through previously executed commands in the terminal.

This is useful for quickly reusing or modifying previous commands.

### `Tab`

Autocompletes commands, filenames, and directory names when possible.

---

## Navigation

### `pwd`

**Print Working Directory**

Displays the full path of the current working directory.

```bash
pwd
```

Example:

```text
/home/user/Documents
```

### `ls`

Lists files and directories.

```bash
ls
```

Useful options:

- `-a` — Shows all entries, including hidden files and directories.
- `-l` — Displays information using a long listing format.

```bash
ls -a
ls -l
ls -la
```

In Linux, hidden files normally begin with a dot:

```text
.bashrc
.config
```

The long format includes information such as:

- Permissions
- Owner
- Group
- File size
- Last modification time
- Filename

### `ll`

On many Linux systems, `ll` is configured as an alias for:

```bash
ls -l
```

However, `ll` is not guaranteed to exist on every Linux system because it is usually an alias rather than a standalone command.

---

## Reading and Editing Files

### `cat`

Displays the contents of a file directly in the terminal.

```bash
cat file.txt
```

### `nano`

Opens the Nano text editor.

It can be used to create or modify text files directly from the terminal.

```bash
nano file.txt
```

---

## Creating Files and Directories

### `mkdir`

**Make Directory**

Creates a new directory.

```bash
mkdir <directory_name>
```

Example:

```bash
mkdir pentesting
```

### `touch`

Creates an empty file if the file does not already exist.

```bash
touch <filename>
```

Example:

```bash
touch notes.txt
```

If the file already exists, `touch` updates its timestamps instead of deleting its contents.

---

## Removing Files and Directories

### `rmdir`

**Remove Directory**

Removes an empty directory.

```bash
rmdir <directory_name>
```

Example:

```bash
rmdir test
```

The directory must be empty for `rmdir` to remove it.

### `rm`

Removes files.

```bash
rm <filename>
```

Useful options:

- `-r` — Recursively removes directories and their contents.
- `-f` — Forces removal without prompting for confirmation.

```bash
rm -r <directory>
rm -f <file>
rm -rf <directory>
```

> **Warning:** `rm -rf` can recursively and permanently delete files and directories without asking for confirmation. Always verify the target path before executing it.

---

## Output and Redirection

### `echo`

Writes text or arguments to the standard output (`stdout`).

```bash
echo "Hello World"
```

Example output:

```text
Hello World
```

### `>`

Redirects the output of a command to a file.

```bash
echo "Hello World" > test.txt
```

> **Important:** `>` overwrites the destination file if it already contains data.

### `>>`

Appends output to the end of a file instead of overwriting its existing contents.

```bash
echo "New line" >> test.txt
```

---

## Getting Help

### `man`

Displays the manual page for a command.

```bash
man <command>
```

Example:

```bash
man ls
```

Manual pages provide detailed information about commands, their syntax, available options, and behavior.

### `help`

Displays help information for Bash built-in commands.

```bash
help <command>
```

Example:

```bash
help cd
```

`help` is mainly used for commands built directly into Bash, while `man` provides manual pages for many Linux commands and programs.

---

## Package Management

Debian-based Linux distributions use APT to manage software packages.

### `apt update`

Downloads updated information about available packages from the configured repositories.

```bash
sudo apt update
```

This does **not** upgrade the installed packages by itself. It updates the local package information.

### `apt upgrade`

Upgrades installed packages when newer versions are available.

```bash
sudo apt upgrade
```

A common combination is:

```bash
sudo apt update && sudo apt upgrade
```

### `&&`

The `&&` operator executes the command on the right only if the command on the left completes successfully.

```bash
sudo apt update && sudo apt upgrade
```

This means:

1. Run `sudo apt update`.
2. If it succeeds, run `sudo apt upgrade`.

### `apt install`

Installs a package.

```bash
sudo apt install <package>
```

Example:

```bash
sudo apt install nmap
```

---

## Quick Reference

| Command | Purpose |
|---|---|
| `whoami` | Display the current username |
| `id` | Display UID, GID, and user groups |
| `passwd` | Change a user's password |
| `sudo` | Execute a command with elevated privileges |
| `su` | Switch user |
| `pwd` | Display the current directory |
| `ls` | List files and directories |
| `ls -a` | Include hidden files |
| `ls -l` | Display a long listing |
| `cat` | Display file contents |
| `nano` | Edit text files |
| `mkdir` | Create a directory |
| `rmdir` | Remove an empty directory |
| `touch` | Create an empty file or update timestamps |
| `rm` | Remove files |
| `rm -r` | Remove directories recursively |
| `rm -rf` | Recursively and forcibly remove files/directories |
| `echo` | Write text to standard output |
| `man` | Display manual pages |
| `help` | Display help for Bash built-ins |
| `sudo apt update` | Update package information |
| `sudo apt upgrade` | Upgrade installed packages |
| `sudo apt install` | Install packages |

---

## Notes

- Linux commands and filenames are case-sensitive.
- Command options such as `-a`, `-l`, `-r`, and `-f` depend on the command being used.
- `>` overwrites a file, while `>>` appends to it.
- Commands executed with `sudo` can modify important parts of the system.
- Destructive commands such as `rm -rf` should always be used carefully.
