# Linux Command Reference Guide

A structured reference guide for Linux terminal commands, system administration tools, networking utilities, and Bash fundamentals.

Designed for Ubuntu/Debian systems, including WSL2 environments.

---

# 1. System Information & Identification

Commands used to identify the operating system, hardware, user information, and system state.

| Command | Syntax | Description |
|---|---|---|
| `whoami` | `whoami` | Displays the current username. |
| `id` | `id [username]` | Shows user ID (UID), group ID (GID), and group membership. |
| `hostname` | `hostname` | Displays the system hostname. |
| `uname` | `uname [options]` | Displays kernel and system information. |
| `uname -a` | `uname -a` | Displays all available system information. |
| `hostnamectl` | `hostnamectl` | Shows system information managed by systemd. |
| `lscpu` | `lscpu` | Displays CPU architecture information. |
| `lsmem` | `lsmem` | Displays memory information. |
| `uptime` | `uptime` | Shows system uptime and load averages. |
| `printenv` | `printenv` | Displays environment variables. |
| `env` | `env` | Prints the current environment. |
| `which` | `which <command>` | Shows the executable location. |
| `type` | `type <command>` | Shows whether a command is built-in, alias, or executable. |

---

# 2. Terminal Control & Productivity

Commands and shortcuts for efficient terminal usage.

## Keyboard Shortcuts

| Shortcut | Description |
|---|---|
| `Tab` | Autocomplete commands and file names. |
| `Ctrl + A` | Move cursor to the beginning of the line. |
| `Ctrl + E` | Move cursor to the end of the line. |
| `Ctrl + L` | Clear terminal screen. |
| `Ctrl + C` | Interrupt the running command. |
| `Ctrl + Z` | Suspend the current process. |
| `Ctrl + R` | Search command history. |
| `!!` | Execute the previous command. |

---

## Command History

| Command | Description |
|---|---|
| `history` | Displays previously executed commands. |
| `history \| grep <text>` | Searches command history. |
| `clear` | Clears the terminal screen. |

---

## echo Command

| Command | Description |
|---|---|
| `echo "text"` | Prints text to the terminal. |
| `echo $VAR` | Prints the value of a variable. |
| `echo $(command)` | Prints the output of another command. |
| `echo -n "text"` | Prints text without adding a new line. |
| `echo -e "text\ntext"` | Enables escape sequences. |
| `echo -e "text\ttext"` | Adds tab spacing using `\t`. |
| `echo "text" > file.txt` | Writes output to a file (overwrites existing content). |
| `echo "text" >> file.txt` | Appends output to the end of a file. |
| `echo "text" \| tee file.txt` | Displays output and writes it to a file. |
| `echo "$PATH"` | Prints environment variable values. |
| `echo "$HOME"` | Prints the user's home directory. |
| `echo "$PWD"` | Prints the current working directory. |
| `echo "$USER"` | Prints the current username. |
| `echo "$?"` | Prints the exit status of the last command. |
| `echo "$$"` | Prints the current shell process ID (PID). |

> [!NOTE]
> Use `<command> >> <file>` to push output of the command in the end of the file.

---

# 3. File System Navigation

Commands for navigating and inspecting the Linux filesystem.

| Command | Syntax | Description |
|---|---|---|
| `pwd` | `pwd` | Displays the current directory path. |
| `ls` | `ls [options]` | Lists directory contents. |
| `cd` | `cd <directory>` | Changes the current directory. |
| `tree` | `tree [options]` | Displays directory structure recursively. |

![Hierarchy](assets\images\linux.png)
![Folders](assets\images\folders.png)

> [!NOTE]
> `tree` is not installed by default on Ubuntu. you can use `find`.

Install:

```bash
sudo apt install tree
```

---

## Common `ls` Options

| Option | Description |
|---|---|
| `-l` | Long listing format. |
| `-a` | Includes hidden files. |
| `-h` | Human-readable file sizes. |
| `-R` | Recursive listing. |

Example:

```bash
ls -lah
```

---

## Directory Shortcuts

| Command | Description |
|---|---|
| `cd ..` | Move to parent directory. |
| `cd ~` | Go to home directory. |
| `cd` | Go to home directory. |
| `cd -` | Return to previous directory. |

---

# 4. File & Directory Management

Commands for creating, copying, moving, and deleting files.

| Command | Syntax | Description |
|---|---|---|
| `touch` | `touch <file>` | Creates an empty file. |
| `mkdir` | `mkdir <directory>` | Creates a directory. |
| `mkdir -p` | `mkdir -p <path>` | Creates parent directories if required. |
| `cp` | `cp <source> <destination>` | Copies files. |
| `cp -r` | `cp -r <source> <destination>` | Copies directories recursively. |
| `mv` | `mv <source> <destination>` | Moves(files & folders) or **renames** files. |
| `rm` | `rm <file>` | Removes files. |
| `rm -r` | `rm -r <directory>` | Removes directories recursively. |
| `rmdir` | `rmdir <directory>` | Removes empty directories. |
| `ln` | `ln <target> <link>` | Creates hard links. |
| `ln -s` | `ln -s <target> <link>` | Creates symbolic links. |
| `find` | `find <path> <options>` | Searches for files and directories. |

> [!TIP]
> Use `mkdir -p tools/index/helper-scripts` to create many folders with one command.


> [!TIP]
> Use `touch file1.txt file2.txt file3.txt` to create many files in the current folder


---

## Common `find` Examples

Find by name:

```bash
find . -name "file.txt"
```

Find directories:

```bash
find /home -type d
```

Find files:

```bash
find /var -type f
```

---

> [!WARNING]
> `rm -rf` permanently removes files and directories without confirmation.

Example:

```bash
rm -rf folder_name
```

Use carefully.

---

# 5. File Information & Content Viewing

Commands for inspecting file content and metadata.

| Command | Syntax | Description |
|---|---|---|
| `cat` | `cat <file>` | Displays file content. |
| `less` | `less <file>` | Interactive file viewer. |
| `more` | `more <file>` | Displays content page by page. |
| `head` | `head <file>` | Shows first 10 lines. |
| `tail` | `tail <file>` | Shows last 10 lines. |
| `tail -f` | `tail -f <file>` | Follows file changes in real time. |
| `file` | `file <file>` | Displays file type information. |
| `stat` | `stat <file>` | Displays detailed file metadata. |

---

# 6. Text Processing

Commands for searching and manipulating text.

| Command | Syntax | Description |
|---|---|---|
| `grep` | `grep <pattern> <file>` | Searches text patterns. |
| `grep -r` | `grep -r <pattern> <path>` | Recursive search. |
| `sed` | `sed 's/old/new/' file` | Stream text replacement. |
| `awk` | `awk '{print $1}' file` | Processes text columns. |
| `cut` | `cut -d <delimiter> -f <field>` | Extracts text fields. |
| `sort` | `sort <file>` | Sorts lines. |
| `uniq` | `uniq <file>` | Removes duplicate lines. |
| `wc` | `wc <file>` | Counts lines, words, and characters. |
| `diff` | `diff <file1> <file2>` | Compares files. |

---

## Pipes & Redirection

| Symbol | Description |
|---|---|
| `>` | Redirect output and overwrite file. |
| `>>` | Append output to file. |
| `|` | Send output of one command to another. |
| `2>` | Redirect errors. |
| `2>&1` | Combine stdout and stderr. |

Example:

```bash
cat file.txt | grep "error"
```

# 7. File Permissions & Ownership

Linux uses a permission system to control access to files and directories.

Each file has three permission groups:

| Permission Group | Description |
|---|---|
| User (`u`) | File owner |
| Group (`g`) | Users belonging to the file group |
| Others (`o`) | All other users |

---

## Permission Types

| Permission | Symbol | Value | Description |
|---|---|---|---|
| Read | `r` | 4 | View file contents |
| Write | `w` | 2 | Modify file contents |
| Execute | `x` | 1 | Run a file as a program |

---

## Permission Commands

| Command | Syntax | Description |
|---|---|---|
| `ls -l` | `ls -l <file>` | Displays file permissions and ownership. |
| `chmod` | `chmod <permissions> <file>` | Changes file permissions. |
| `chown` | `chown <user>:<group> <file>` | Changes file ownership. |
| `chgrp` | `chgrp <group> <file>` | Changes file group ownership. |

---

## chmod Examples

Symbolic mode:

```bash
chmod u+x script.sh
```

Add execute permission for the owner.

Numeric mode:

```bash
chmod 755 script.sh
```

Permission breakdown:

| Number | Permission |
|---|---|
| 7 | Read + Write + Execute |
| 5 | Read + Execute |
| 4 | Read only |

Common permissions:

| Mode | Usage |
|---|---|
| `755` | Executable files and directories |
| `644` | Regular files |
| `700` | Private executable files |
| `600` | Private files |

---

# 8. User Management

Commands for managing users and groups.

| Command | Syntax | Description |
|---|---|---|
| `whoami` | `whoami` | Shows current user. |
| `id` | `id <user>` | Displays UID, GID, and groups. |
| `groups` | `groups <user>` | Shows group membership. |
| `passwd` | `passwd <user>` | Changes user password. |
| `useradd` | `useradd <username>` | Creates a new user. |
| `usermod` | `usermod [options] <user>` | Modifies user settings. |
| `userdel` | `userdel <user>` | Deletes a user. |
| `groupadd` | `groupadd <group>` | Creates a group. |
| `groupdel` | `groupdel <group>` | Deletes a group. |

---

## Privilege Management

| Command | Description |
|---|---|
| `sudo <command>` | Runs a command with administrator privileges. |
| `su <user>` | Switches to another user. |
| `su -` | Switches to root with login environment. |

Example:

```bash
sudo apt update
```

---

# 9. Package Management (Ubuntu / Debian)

APT is the default package manager for Ubuntu and Debian-based systems.

| Command | Description |
|---|---|
| `sudo apt update` | Updates package information. |
| `sudo apt upgrade` | Upgrades installed packages. |
| `sudo apt install <package>` | Installs a package. |
| `sudo apt remove <package>` | Removes a package. |
| `sudo apt purge <package>` | Removes package and configuration files. |
| `sudo apt autoremove` | Removes unused dependencies. |
| `sudo apt search <name>` | Searches available packages. |
| `apt show <package>` | Displays package information. |
| `dpkg -l` | Lists installed packages. |
| `dpkg -i <file.deb>` | Installs a `.deb` package manually. |

---

## Common Optional Packages

Some Linux commands are not installed by default.

| Command | Package |
|---|---|
| `tree` | `tree` |
| `htop` | `htop` |
| `tcpdump` | `tcpdump` |
| `sensors` | `lm-sensors` |
| `sar` | `sysstat` |
| `smartctl` | `smartmontools` |
| `stress-ng` | `stress-ng` |

Install packages:

```bash
sudo apt install <package>
```

---

# 10. Process Management

Commands for monitoring and controlling running programs.

---

## Process Information

| Command | Syntax | Description |
|---|---|---|
| `ps` | `ps` | Shows current shell processes. |
| `ps aux` | `ps aux` | Lists all running processes. |
| `top` | `top` | Real-time process monitor. |
| `htop` | `htop` | Interactive process monitor. |
| `pgrep` | `pgrep <name>` | Finds process IDs by name. |
| `jobs` | `jobs` | Lists background jobs. |

---

## Background Processes

| Command | Description |
|---|---|
| `command &` | Runs command in background. |
| `fg` | Brings process to foreground. |
| `bg` | Resumes suspended process in background. |
| `Ctrl + Z` | Suspends current process. |

---

## Terminating Processes

| Command | Description |
|---|---|
| `kill <PID>` | Sends termination signal. |
| `kill -9 <PID>` | Forces process termination. |
| `pkill <name>` | Kills processes by name. |
| `killall <name>` | Terminates all processes with a name. |

Example:

```bash
kill 1234
```

---

# 11. System Services

Services are background processes managed by `systemd`.

| Command | Description |
|---|---|
| `systemctl status <service>` | Shows service status. |
| `systemctl start <service>` | Starts a service. |
| `systemctl stop <service>` | Stops a service. |
| `systemctl restart <service>` | Restarts a service. |
| `systemctl enable <service>` | Enables service at boot. |
| `systemctl disable <service>` | Disables service at boot. |

Example:

```bash
sudo systemctl status ssh
```

> [!NOTE]
> In WSL, systemd support depends on configuration. Some services may not run by default.

---

# 12. Disk & Storage Management

Commands for checking disk usage and storage devices.

| Command | Syntax | Description |
|---|---|---|
| `df` | `df -h` | Shows filesystem disk usage. |
| `du` | `du -h` | Shows directory sizes. |
| `lsblk` | `lsblk` | Lists block devices. |
| `mount` | `mount` | Displays mounted filesystems. |
| `findmnt` | `findmnt` | Shows mounted filesystems tree. |
| `blkid` | `blkid` | Displays device UUID information. |

---

## Disk Usage Examples

Show folder sizes:

```bash
du -sh *
```

Show free disk space:

```bash
df -h
```

List disks:

```bash
lsblk
```

---

# 13. Archive & Compression

Commands for creating and extracting archives.

| Command | Description |
|---|---|
| `tar` | Creates and extracts tar archives. |
| `gzip` | Compresses files. |
| `gunzip` | Extracts gzip files. |
| `zip` | Creates ZIP archives. |
| `unzip` | Extracts ZIP archives. |

---

## tar Examples

Create archive:

```bash
tar -cvf archive.tar folder/
```

Extract archive:

```bash
tar -xvf archive.tar
```

Create compressed archive:

```bash
tar -czvf archive.tar.gz folder/
```

Extract compressed archive:

```bash
tar -xzvf archive.tar.gz
```

# 14. Networking

Commands for network configuration, diagnostics, and remote communication.

---

# Network Information

| Command | Syntax | Description |
|---|---|---|
| `hostname` | `hostname` | Displays system hostname. |
| `hostname -I` | `hostname -I` | Shows assigned IP addresses. |
| `ip` | `ip [options]` | Modern tool for network configuration. |
| `ip addr` | `ip addr` | Displays network interfaces and IP addresses. |
| `ip link` | `ip link` | Shows network interfaces status. |
| `ip route` | `ip route` | Displays routing table. |
| `ip neigh` | `ip neigh` | Shows ARP neighbor information. |

---

## Network Diagnostics

| Command | Syntax | Description |
|---|---|---|
| `ping` | `ping <host>` | Tests network connectivity. |
| `curl` | `curl <URL>` | Transfers data from or to a server. |
| `wget` | `wget <URL>` | Downloads files from the web. |
| `traceroute` | `traceroute <host>` | Shows network path to a destination. |
| `dig` | `dig <domain>` | Queries DNS information. |
| `nslookup` | `nslookup <domain>` | Performs DNS lookup. |

---

## Common Networking Examples

Check local IP:

```bash
hostname -I
```

Check network interface:

```bash
ip addr
```

Test connectivity:

```bash
ping google.com
```

Check DNS:

```bash
dig google.com
```

Download a file:

```bash
wget https://example.com/file.zip
```

---

# Network Connections & Ports

| Command | Syntax | Description |
|---|---|---|
| `ss` | `ss [options]` | Displays network sockets and connections. |
| `ss -tuln` | `ss -tuln` | Shows listening TCP/UDP ports. |
| `ss -tulpn` | `ss -tulpn` | Shows ports and related processes. |

> [!NOTE]
> `netstat` is a legacy command. Use `ss` instead.

---

# Legacy Network Commands

Older commands replaced by modern tools.

| Legacy Command | Replacement |
|---|---|
| `ifconfig` | `ip addr` |
| `netstat` | `ss` |
| `route` | `ip route` |
| `arp` | `ip neigh` |

---

# 15. Remote Access

Commands for connecting and transferring files between systems.

---

## SSH

Secure remote shell access.

| Command | Description |
|---|---|
| `ssh user@host` | Connects to a remote machine. |
| `ssh -p <port> user@host` | Connects using a custom port. |
| `ssh-keygen` | Generates SSH authentication keys. |
| `ssh-copy-id` | Copies SSH public key to a server. |

Example:

```bash
ssh yavor@192.168.1.10
```

---

## Secure File Transfer

| Command | Description |
|---|---|
| `scp` | Copies files securely over SSH. |
| `rsync` | Synchronizes files efficiently. |

Examples:

Copy file:

```bash
scp file.txt user@server:/home/user/
```

Synchronize directory:

```bash
rsync -av folder/ user@server:/backup/
```

---

# 16. Environment Variables

Environment variables store system and user configuration values.

| Command | Description |
|---|---|
| `env` | Displays all environment variables. |
| `printenv` | Prints environment variables. |
| `echo $VARIABLE` | Displays a specific variable. |
| `export` | Creates or modifies variables. |
| `unset` | Removes a variable. |

Examples:

Display PATH:

```bash
echo $PATH
```

Create variable:

```bash
export NAME="Linux"
```

---

# 17. Aliases & Shell Configuration

Aliases create shortcuts for frequently used commands.

| Command | Description |
|---|---|
| `alias` | Displays existing aliases. |
| `alias name='command'` | Creates a temporary alias. |
| `unalias` | Removes an alias. |

Example:

```bash
alias ll="ls -lah"
```

---

## Permanent Aliases

Add aliases to:

```bash
~/.bashrc
```

Example:

```bash
echo "alias ll='ls -lah'" >> ~/.bashrc
```

Reload configuration:

```bash
source ~/.bashrc
```

---

# 18. Scheduling Tasks (Cron)

Cron runs commands automatically at scheduled times.

---

## Cron Syntax

```
* * * * * command
│ │ │ │ │
│ │ │ │ └── Day of week
│ │ │ └──── Month
│ │ └────── Day of month
│ └──────── Hour
└────────── Minute
```

---

## Cron Commands

| Command | Description |
|---|---|
| `crontab -e` | Edit current user's cron jobs. |
| `crontab -l` | List cron jobs. |
| `crontab -r` | Remove cron jobs. |

Example:

Run script every day at midnight:

```bash
0 0 * * * /home/user/script.sh
```

---

# 19. Bash Scripting

Bash scripts automate repetitive tasks using Linux commands.

---

## Script Structure

Example:

```bash
#!/bin/bash

echo "Hello Linux"
```

Make executable:

```bash
chmod +x script.sh
```

Run:

```bash
./script.sh
```

---

# Variables

Create variable:

```bash
NAME="Linux"
```

Use variable:

```bash
echo $NAME
```

---

# User Input

```bash
read USERNAME

echo "Hello $USERNAME"
```

---

# Script Arguments

Arguments are accessed by position.

| Variable | Description |
|---|---|
| `$0` | Script name |
| `$1` | First argument |
| `$2` | Second argument |
| `$@` | All arguments |
| `$#` | Number of arguments |

Example:

```bash
./script.sh file.txt
```

Inside script:

```bash
echo $1
```

---

# Conditions

Example:

```bash
if [[ $USER == "root" ]]; then
    echo "Administrator"
else
    echo "Regular user"
fi
```

---

# Loops

## For Loop

```bash
for file in *.txt
do
    echo $file
done
```

---

## While Loop

```bash
while true
do
    echo "Running"
done
```

---

# Functions

Example:

```bash
backup()
{
    echo "Creating backup"
}

backup
```

---

# 20. Useful Administrative Commands

| Command | Description |
|---|---|
| `sudo reboot` | Restarts the system. |
| `sudo shutdown now` | Shuts down the system. |
| `date` | Displays current date and time. |
| `cal` | Displays calendar. |
| `man <command>` | Opens command manual. |
| `help` | Shows Bash built-in command help. |
| `history` | Shows command history. |
| `alias` | Shows command shortcuts. |

---

# 21. Command Help & Documentation

Linux provides multiple ways to get command information.

| Command | Description |
|---|---|
| `man <command>` | Complete manual page. |
| `<command> --help` | Short command help. |
| `info <command>` | Detailed documentation. |
| `apropos <keyword>` | Searches manual pages. |

Examples:

```bash
man ls
```

```bash
ls --help
```

---

# 22. Common Command-Line Tools

Useful utilities commonly available on Linux systems.

| Command | Purpose |
|---|---|
| `tee` | Writes output to file and terminal simultaneously. |
| `xargs` | Builds command arguments from input. |
| `watch` | Repeats a command periodically. |
| `time` | Measures command execution time. |
| `nohup` | Runs commands after logout. |

Examples:

Monitor command:

```bash
watch df -h
```

Measure execution time:

```bash
time ls
```

Save output while displaying:

```bash
ls -la | tee output.txt
```

