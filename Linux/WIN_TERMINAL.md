# Windows Command Reference Guide

A structured reference guide for Microsoft Windows command-line utilities, system administration, networking, and troubleshooting.

Designed for Windows 10 and Windows 11.

---

# 1. Command Prompt Basics

The Command Prompt (`cmd.exe`) is the traditional command-line interpreter for Windows.

Open Command Prompt:

- Press **Win + R**
- Type:

```text
cmd
```

Open as Administrator:

- Search for **Command Prompt**
- Select **Run as administrator**

> [!TIP]
> Many administrative commands require an elevated Command Prompt.

---

# 2. System Information

Commands used to identify the current user, computer, operating system, and environment.

| Command | Syntax | Description |
|---|---|---|
| `hostname` | `hostname` | Displays the computer name. |
| `whoami` | `whoami` | Displays the current logged-in user. |
| `systeminfo` | `systeminfo` | Displays detailed system information. |
| `ver` | `ver` | Displays the Windows version. |
| `date` | `date` | Displays or changes the current date. |
| `time` | `time` | Displays or changes the current time. |
| `echo %USERNAME%` | `echo %USERNAME%` | Displays the current username. |
| `echo %COMPUTERNAME%` | `echo %COMPUTERNAME%` | Displays the computer name. |
| `echo %OS%` | `echo %OS%` | Displays the operating system name. |

---

## Examples

Display Windows version:

```cmd
ver
```

Display system information:

```cmd
systeminfo
```

Display current user:

```cmd
whoami
```

---

# 3. File & Directory Navigation

Commands for navigating the Windows filesystem.

| Command | Syntax | Description |
|---|---|---|
| `cd` | `cd [path]` | Changes the current directory. |
| `cd ..` | `cd ..` | Moves to the parent directory. |
| `cd \` | `cd \` | Moves to the root directory of the current drive. |
| `dir` | `dir [path]` | Lists directory contents. |
| `tree` | `tree [path]` | Displays the directory tree. |
| `tree /F` | `tree /F` | Displays files in the directory tree. |
| `cls` | `cls` | Clears the Command Prompt window. |

---

## Common `dir` Options

| Option | Description |
|---|---|
| `/A` | Displays hidden and system files. |
| `/B` | Bare format (file names only). |
| `/O` | Sorts output. |
| `/S` | Includes all subdirectories. |
| `/P` | Displays one page at a time. |

Example:

```cmd
dir /A
```

---

## Directory Examples

Current directory:

```cmd
cd
```

Change directory:

```cmd
cd C:\Users\Pesho\Desktop
```

Display directory tree:

```cmd
tree
```

---

# 4. File & Directory Management

Commands for creating, copying, moving, renaming, and deleting files.

| Command | Syntax | Description |
|---|---|---|
| `mkdir` | `mkdir <directory>` | Creates a directory. |
| `md` | `md <directory>` | Alias for `mkdir`. |
| `rmdir` | `rmdir <directory>` | Removes an empty directory. |
| `rmdir /S` | `rmdir /S <directory>` | Removes a directory recursively. |
| `copy` | `copy <source> <destination>` | Copies files. |
| `xcopy` | `xcopy <source> <destination>` | Copies directories and files. |
| `robocopy` | `robocopy <source> <destination>` | Advanced file copy utility. |
| `move` | `move <source> <destination>` | Moves files or directories. |
| `ren` | `ren <old> <new>` | Renames files or directories. |
| `del` | `del <file>` | Deletes files. |
| `erase` | `erase <file>` | Alias for `del`. |

---

## Examples

Create directory:

```cmd
mkdir Projects
```

Rename file:

```cmd
ren notes.txt notes_old.txt
```

Delete file:

```cmd
del notes.txt
```

Delete folder recursively:

```cmd
rmdir /S Projects
```

> [!WARNING]
> `rmdir /S` permanently removes the specified directory and all of its contents.

---

# 5. Viewing & Searching Files

Commands for displaying file contents and searching for text or files.

| Command | Syntax | Description |
|---|---|---|
| `type` | `type <file>` | Displays file contents. |
| `more` | `more <file>` | Displays content one page at a time. |
| `find` | `find "text" <file>` | Searches for text in a file. |
| `findstr` | `findstr "text" <file>` | Searches for strings using advanced patterns. |
| `fc` | `fc <file1> <file2>` | Compares two files. |
| `where` | `where <program>` | Locates executable files. |

---

## Examples

Display a text file:

```cmd
type notes.txt
```

Search for a word:

```cmd
find "error" log.txt
```

Search recursively:

```cmd
findstr /S "TODO" *.txt
```

Locate an executable:

```cmd
where python
```

---

# 6. Output & Environment Variables

Commands for displaying output and working with environment variables.

| Command | Syntax | Description |
|---|---|---|
| `echo` | `echo <text>` | Displays text. |
| `echo %VAR%` | `echo %VARIABLE%` | Displays an environment variable. |
| `set` | `set` | Displays all environment variables. |
| `set VAR=value` | `set <name>=<value>` | Creates or modifies a variable. |
| `setx` | `setx <name> <value>` | Creates a permanent environment variable. |

---

## Output Redirection

| Operator | Description | Example |
|---|---|---|
| `>` | Writes output and overwrites a file. | `echo Hello > file.txt` |
| `>>` | Appends output to a file. | `echo Hello >> file.txt` |
| `|` | Pipes output to another command. | `dir \| more` |

---

## Examples

Display PATH:

```cmd
echo %PATH%
```

Display current directory:

```cmd
echo %CD%
```

Create variable:

```cmd
set NAME=Windows
```

Display variable:

```cmd
echo %NAME%
```

Append text to a file:

```cmd
echo Backup completed >> log.txt
```

> [!NOTE]
> Variables created with `set` exist only for the current Command Prompt session.

# 7. Network Configuration

Commands for viewing and configuring network interfaces and IP settings.

| Command | Syntax | Description |
|---|---|---|
| `ipconfig` | `ipconfig [options]` | Displays IP configuration information. |
| `hostname` | `hostname` | Displays the computer name. |
| `getmac` | `getmac [options]` | Displays MAC addresses of network adapters. |
| `arp` | `arp [options]` | Displays or modifies the ARP cache. |
| `route` | `route [options]` | Displays or modifies the routing table. |
| `netsh` | `netsh <context> <command>` | Configures advanced network settings. |

---

## Common `ipconfig` Options

| Command | Description |
|---|---|
| `ipconfig` | Displays basic IP configuration. |
| `ipconfig /all` | Displays complete adapter information. |
| `ipconfig /release` | Releases the current IPv4 address. |
| `ipconfig /renew` | Requests a new IPv4 address from DHCP. |
| `ipconfig /flushdns` | Clears the DNS resolver cache. |
| `ipconfig /displaydns` | Displays cached DNS records. |
| `ipconfig /registerdns` | Refreshes DHCP leases and DNS registration. |

---

## Examples

View current IP configuration:

```cmd
ipconfig
```

Display detailed information:

```cmd
ipconfig /all
```

Clear DNS cache:

```cmd
ipconfig /flushdns
```

Renew DHCP lease:

```cmd
ipconfig /renew
```

---

> [!TIP]
> `ipconfig /flushdns` is commonly used when troubleshooting DNS resolution issues.

---

# 8. Network Diagnostics

Commands for testing connectivity and resolving network problems.

| Command | Syntax | Description |
|---|---|---|
| `ping` | `ping <host>` | Tests connectivity to another host. |
| `tracert` | `tracert <host>` | Displays the route packets take to a destination. |
| `pathping` | `pathping <host>` | Combines `ping` and `tracert` for detailed diagnostics. |
| `nslookup` | `nslookup <domain>` | Queries DNS servers. |
| `netstat` | `netstat [options]` | Displays active network connections. |

---

## Common `ping` Options

| Command | Description |
|---|---|
| `ping host` | Sends four ICMP echo requests. |
| `ping -t host` | Continuously pings until interrupted. |
| `ping -n <count> host` | Sends a specified number of requests. |
| `ping -l <size> host` | Specifies packet size. |

---

## Examples

Test Internet connectivity:

```cmd
ping google.com
```

Ping a specific IP:

```cmd
ping 8.8.8.8
```

Continuous ping:

```cmd
ping -t google.com
```

Stop continuous ping:

```text
Ctrl + C
```

---

## `tracert`

Shows each router (hop) between your computer and the destination.

Example:

```cmd
tracert google.com
```

---

## `pathping`

Performs route tracing and packet loss analysis.

Example:

```cmd
pathping google.com
```

> [!NOTE]
> `pathping` may take several minutes to complete because it collects statistics for every hop.

---

## `nslookup`

Query DNS records.

Examples:

Lookup a domain:

```cmd
nslookup google.com
```

Use a specific DNS server:

```cmd
nslookup google.com 8.8.8.8
```

---

# 9. Network Connections

Commands for viewing active connections and listening ports.

| Command | Syntax | Description |
|---|---|---|
| `netstat` | `netstat` | Displays active connections. |
| `netstat -a` | `netstat -a` | Displays all connections and listening ports. |
| `netstat -n` | `netstat -n` | Displays numeric addresses. |
| `netstat -o` | `netstat -o` | Displays associated process IDs (PID). |
| `netstat -b` | `netstat -b` | Displays executable names (Administrator required). |

---

## Examples

View listening ports:

```cmd
netstat -a
```

View ports with PIDs:

```cmd
netstat -ano
```

Find which process uses a port:

```cmd
netstat -ano
```

Then identify the process:

```cmd
tasklist | find "1234"
```

Replace `1234` with the PID shown by `netstat`.

---

> [!TIP]
> `netstat -ano` is one of the most useful commands for identifying which application is using a specific port.

---

# 10. Internet & File Transfer

Commands for downloading files and connecting to remote systems.

| Command | Syntax | Description |
|---|---|---|
| `curl` | `curl [options] <URL>` | Transfers data from or to a server. |
| `ftp` | `ftp <host>` | Connects to an FTP server. |
| `ssh` | `ssh <user>@<host>` | Connects to a remote computer using SSH. |
| `scp` | `scp <source> <destination>` | Securely copies files over SSH. |

---

## `curl` Examples

Download a file:

```cmd
curl -O https://example.com/file.zip
```

Display webpage content:

```cmd
curl https://example.com
```

Display only HTTP headers:

```cmd
curl -I https://example.com
```

---

## SSH Example

Connect to a remote Linux server:

```cmd
ssh user@192.168.1.10
```

Using a custom port:

```cmd
ssh -p 2222 user@192.168.1.10
```

---

## SCP Example

Copy a local file to a remote server:

```cmd
scp report.pdf user@192.168.1.10:/home/user/
```

Copy a file from a remote server:

```cmd
scp user@192.168.1.10:/home/user/report.pdf .
```

---

> [!NOTE]
> Modern versions of Windows 10 and Windows 11 include the OpenSSH client (`ssh` and `scp`) by default. Older versions may require installing the **OpenSSH Client** feature.

---

# 11. Network Troubleshooting Workflow

A typical sequence for diagnosing network issues:

1. Verify the local IP configuration:

```cmd
ipconfig
```

2. Test the local network:

```cmd
ping <gateway>
```

3. Test Internet connectivity:

```cmd
ping 8.8.8.8
```

4. Test DNS resolution:

```cmd
nslookup google.com
```

5. Trace the route:

```cmd
tracert google.com
```

6. Inspect active connections:

```cmd
netstat -ano
```

> [!TIP]
> This workflow covers the most common network troubleshooting scenarios, from local connectivity to DNS and routing issues.

# 12. Process Management

Commands for monitoring, managing, and terminating running processes.

| Command | Syntax | Description |
|---|---|---|
| `tasklist` | `tasklist [options]` | Displays all running processes. |
| `taskkill` | `taskkill [options] <PID \| image>` | Terminates a process. |
| `start` | `start [options] <program>` | Starts a new program or command window. |

---

## Common `tasklist` Options

| Command | Description |
|---|---|
| `tasklist` | Lists all running processes. |
| `tasklist /FI "filter"` | Filters processes. |
| `tasklist /SVC` | Displays hosted Windows services. |
| `tasklist /V` | Displays detailed process information. |

Examples:

Display running processes:

```cmd
tasklist
```

Find a process:

```cmd
tasklist | find "chrome"
```

---

## Common `taskkill` Options

| Command | Description |
|---|---|
| `taskkill /PID <pid>` | Terminates a process by PID. |
| `taskkill /IM <name>` | Terminates by executable name. |
| `taskkill /F` | Forces termination. |
| `taskkill /T` | Terminates child processes. |

Examples:

Terminate by PID:

```cmd
taskkill /PID 1234
```

Terminate by executable:

```cmd
taskkill /IM notepad.exe
```

Force termination:

```cmd
taskkill /F /IM chrome.exe
```

> [!WARNING]
> Forcing a process to terminate may result in unsaved data being lost.

---

# 13. Services

Windows services run in the background independently of user sessions.

| Command | Syntax | Description |
|---|---|---|
| `sc query` | `sc query` | Lists services. |
| `sc query <service>` | `sc query <service>` | Displays service status. |
| `sc start` | `sc start <service>` | Starts a service. |
| `sc stop` | `sc stop <service>` | Stops a service. |
| `sc config` | `sc config <service> ...` | Changes service configuration. |
| `net start` | `net start` | Lists running services. |
| `net start <service>` | `net start <service>` | Starts a service. |
| `net stop <service>` | `net stop <service>` | Stops a service. |

---

## Examples

List running services:

```cmd
net start
```

Check a service:

```cmd
sc query Spooler
```

Start Print Spooler:

```cmd
net start Spooler
```

Stop Print Spooler:

```cmd
net stop Spooler
```

---

> [!NOTE]
> Many service management commands require an elevated Command Prompt.

---

# 14. User & Session Management

Commands for managing users and active sessions.

| Command | Syntax | Description |
|---|---|---|
| `whoami` | `whoami` | Displays current user. |
| `net user` | `net user` | Lists local user accounts. |
| `net user <user>` | `net user <user>` | Displays user information. |
| `net user <user> *` | `net user <user> *` | Changes a user's password. |
| `query user` | `query user` | Displays active user sessions. |
| `logoff` | `logoff <session>` | Signs out a user session. |

---

## Examples

List users:

```cmd
net user
```

Display account information:

```cmd
net user Administrator
```

Change password:

```cmd
net user Yavor *
```

---

# 15. Disk & Storage Management

Commands for managing disks, partitions, and file systems.

| Command | Syntax | Description |
|---|---|---|
| `diskpart` | `diskpart` | Opens the DiskPart utility. |
| `chkdsk` | `chkdsk <drive>` | Checks disk integrity. |
| `format` | `format <drive>` | Formats a volume. |
| `label` | `label <drive>` | Changes a volume label. |
| `vol` | `vol <drive>` | Displays the volume label and serial number. |

---

## `chkdsk`

Common options:

| Command | Description |
|---|---|
| `chkdsk C:` | Checks the drive. |
| `chkdsk C: /F` | Fixes file system errors. |
| `chkdsk C: /R` | Locates bad sectors and recovers data. |

Example:

```cmd
chkdsk C: /F
```

---

> [!NOTE]
> `chkdsk` may require a system restart if the drive is currently in use.

---

## DiskPart

Start DiskPart:

```cmd
diskpart
```

Useful commands:

| Command | Description |
|---|---|
| `list disk` | Lists physical disks. |
| `list volume` | Lists volumes. |
| `select disk <n>` | Selects a disk. |
| `select volume <n>` | Selects a volume. |
| `detail disk` | Displays detailed disk information. |
| `exit` | Exits DiskPart. |

---

> [!WARNING]
> DiskPart can permanently erase partitions and data. Verify the selected disk before executing commands.

---

# 16. Power Management

Commands for shutting down, restarting, and managing power settings.

| Command | Syntax | Description |
|---|---|---|
| `shutdown` | `shutdown [options]` | Shuts down or restarts Windows. |
| `powercfg` | `powercfg [options]` | Configures power settings. |

---

## Common `shutdown` Options

| Command | Description |
|---|---|
| `shutdown /s` | Shut down the computer. |
| `shutdown /r` | Restart the computer. |
| `shutdown /l` | Log off the current user. |
| `shutdown /a` | Abort a pending shutdown. |
| `shutdown /t <sec>` | Specifies a delay. |

Examples:

Restart immediately:

```cmd
shutdown /r /t 0
```

Shutdown in one minute:

```cmd
shutdown /s /t 60
```

Cancel shutdown:

```cmd
shutdown /a
```

---

## Power Configuration

Display available power plans:

```cmd
powercfg /list
```

Generate battery report:

```cmd
powercfg /batteryreport
```

Display energy diagnostics:

```cmd
powercfg /energy
```

---

# 17. Drivers & Hardware

Commands for viewing installed drivers and hardware information.

| Command | Syntax | Description |
|---|---|---|
| `driverquery` | `driverquery` | Lists installed drivers. |
| `driverquery /V` | `driverquery /V` | Displays detailed driver information. |
| `driverquery /FO CSV` | `driverquery /FO CSV` | Exports output as CSV. |

Example:

```cmd
driverquery
```

---

# 18. Scheduled Tasks

Commands for managing Windows Task Scheduler.

| Command | Syntax | Description |
|---|---|---|
| `schtasks` | `schtasks [options]` | Manages scheduled tasks. |

---

## Common Examples

List scheduled tasks:

```cmd
schtasks
```

Display verbose information:

```cmd
schtasks /query /v
```

Run a scheduled task:

```cmd
schtasks /run /TN "TaskName"
```

Delete a task:

```cmd
schtasks /delete /TN "TaskName"
```

---

# 19. Command Help

Commands for obtaining documentation and usage information.

| Command | Syntax | Description |
|---|---|---|
| `help` | `help` | Lists available commands. |
| `help <command>` | `help <command>` | Displays help for a command. |
| `<command> /?` | `<command> /?` | Displays command syntax and options. |

Examples:

```cmd
help
```

```cmd
help xcopy
```

```cmd
ipconfig /?
```

---

> [!TIP]
> Almost every built-in Windows command supports the `/?` switch to display its syntax and available options.

# 20. System Repair & Troubleshooting

Commands used to diagnose and repair Windows system files, images, and boot configuration.

| Command | Syntax | Description |
|---|---|---|
| `sfc` | `sfc [options]` | Scans and repairs protected system files. |
| `DISM` | `DISM [options]` | Repairs and services the Windows image. |
| `bcdedit` | `bcdedit [options]` | Manages the Boot Configuration Data (BCD). |
| `bootrec` | `bootrec [options]` | Repairs boot records (Windows Recovery Environment). |
| `reagentc` | `reagentc [options]` | Configures the Windows Recovery Environment. |

---

## System File Checker (SFC)

Common options:

| Command | Description |
|---|---|
| `sfc /scannow` | Scans and repairs all protected system files. |
| `sfc /verifyonly` | Checks for integrity violations without repairing. |
| `sfc /scanfile=<file>` | Scans a specific system file. |

Example:

```cmd
sfc /scannow
```

> [!TIP]
> If SFC cannot repair corrupted files, run **DISM** first and then execute `sfc /scannow` again.

---

## Deployment Image Servicing and Management (DISM)

Common commands:

| Command | Description |
|---|---|
| `DISM /Online /Cleanup-Image /CheckHealth` | Checks if corruption exists. |
| `DISM /Online /Cleanup-Image /ScanHealth` | Performs a detailed corruption scan. |
| `DISM /Online /Cleanup-Image /RestoreHealth` | Repairs the Windows image. |

Example:

```cmd
DISM /Online /Cleanup-Image /RestoreHealth
```

---

## Typical Repair Workflow

```cmd
DISM /Online /Cleanup-Image /RestoreHealth
```

then

```cmd
sfc /scannow
```

---

# 21. File Compression

Windows includes built-in utilities for working with archive files.

| Command | Syntax | Description |
|---|---|---|
| `tar` | `tar [options]` | Creates or extracts archive files. |
| `compact` | `compact [options]` | Compresses NTFS files and folders. |
| `expand` | `expand <cab> <destination>` | Extracts Microsoft CAB files. |

---

## tar Examples

Extract archive:

```cmd
tar -xf archive.tar
```

Extract ZIP archive:

```cmd
tar -xf archive.zip
```

Create archive:

```cmd
tar -cf backup.tar Documents
```

---

## compact Examples

Compress a folder:

```cmd
compact /C Documents
```

Display compression status:

```cmd
compact
```

---

# 22. File Permissions

Commands for viewing and modifying NTFS permissions.

| Command | Syntax | Description |
|---|---|---|
| `icacls` | `icacls <path>` | Displays file permissions. |
| `icacls /grant` | `icacls <path> /grant <user>:<perm>` | Grants permissions. |
| `icacls /remove` | `icacls <path> /remove <user>` | Removes permissions. |
| `takeown` | `takeown /F <path>` | Takes ownership of files or folders. |

---

## Examples

Display permissions:

```cmd
icacls report.txt
```

Take ownership:

```cmd
takeown /F report.txt
```

Grant Full Control:

```cmd
icacls report.txt /grant Yavor:F
```

---

> [!WARNING]
> Incorrect NTFS permissions may prevent users or applications from accessing files.

---

# 23. Windows Package Management

Windows Package Manager (`winget`) installs and manages software from the command line.

| Command | Syntax | Description |
|---|---|---|
| `winget search` | `winget search <package>` | Searches for packages. |
| `winget install` | `winget install <package>` | Installs software. |
| `winget uninstall` | `winget uninstall <package>` | Removes software. |
| `winget upgrade` | `winget upgrade` | Lists available updates. |
| `winget upgrade --all` | `winget upgrade --all` | Updates all installed packages. |
| `winget list` | `winget list` | Lists installed packages. |

---

## Examples

Search for Git:

```cmd
winget search git
```

Install Visual Studio Code:

```cmd
winget install Microsoft.VisualStudioCode
```

Upgrade installed software:

```cmd
winget upgrade --all
```

---

> [!NOTE]
> `winget` is available by default on modern versions of Windows 10 and Windows 11.

---

# 24. Useful System Utilities

Frequently used Windows administration tools.

| Command | Description |
|---|---|
| `msconfig` | Opens System Configuration. |
| `taskmgr` | Opens Task Manager. |
| `eventvwr` | Opens Event Viewer. |
| `services.msc` | Opens the Services console. |
| `devmgmt.msc` | Opens Device Manager. |
| `diskmgmt.msc` | Opens Disk Management. |
| `compmgmt.msc` | Opens Computer Management. |
| `regedit` | Opens Registry Editor. |
| `gpedit.msc` | Opens Local Group Policy Editor (Pro editions). |
| `control` | Opens Control Panel. |
| `appwiz.cpl` | Opens Programs and Features. |
| `optionalfeatures` | Opens Windows Features. |
| `cleanmgr` | Opens Disk Cleanup. |
| `resmon` | Opens Resource Monitor. |
| `perfmon` | Opens Performance Monitor. |

---

## Examples

Open Device Manager:

```cmd
devmgmt.msc
```

Open Disk Management:

```cmd
diskmgmt.msc
```

Open Registry Editor:

```cmd
regedit
```

---

# 25. Common Keyboard Shortcuts

Useful shortcuts when working in Command Prompt.

| Shortcut | Description |
|---|---|
| `Tab` | Auto-complete file and folder names. |
| `↑ / ↓` | Browse command history. |
| `F7` | Display command history window. |
| `Ctrl + C` | Interrupt the current command. |
| `Ctrl + V` | Paste clipboard contents. |
| `Ctrl + A` | Select all text. |
| `cls` | Clear the Command Prompt window. |

---

# 26. Legacy Commands

The following commands are still available but have modern alternatives.

| Legacy Command | Modern Alternative |
|---|---|
| `xcopy` | `robocopy` |
| `ftp` | `scp` / `sftp` |
| `netstat` | PowerShell `Get-NetTCPConnection` |
| `wmic` | PowerShell CIM cmdlets |
| `at` | `schtasks` |

> [!NOTE]
> Legacy commands remain supported for compatibility but may be deprecated in future Windows releases.

---

# 27. Best Practices

- Run administrative commands from an **elevated Command Prompt** when required.
- Use `robocopy` instead of `xcopy` for large directory transfers.
- Use `winget` to install and update software.
- Verify the syntax of unfamiliar commands using:

```cmd
command /?
```

- Use `sfc` and `DISM` when troubleshooting Windows system corruption.
- Confirm the target path before using destructive commands such as:

```cmd
del
```

or

```cmd
rmdir /S
```

---

# 28. Command Reference Summary

| Category | Primary Commands |
|---|---|
| Navigation | `cd`, `dir`, `tree`, `cls` |
| File Management | `mkdir`, `copy`, `move`, `ren`, `del`, `robocopy` |
| File Viewing | `type`, `more`, `find`, `findstr`, `fc` |
| Environment | `echo`, `set`, `setx` |
| Networking | `ipconfig`, `ping`, `tracert`, `pathping`, `netstat`, `nslookup`, `arp`, `route` |
| Internet | `curl`, `ssh`, `scp` |
| Processes | `tasklist`, `taskkill`, `start` |
| Services | `sc`, `net start`, `net stop` |
| Users | `whoami`, `net user` |
| Storage | `diskpart`, `chkdsk`, `format`, `vol` |
| Power | `shutdown`, `powercfg` |
| Repair | `sfc`, `DISM`, `bootrec` |
| Permissions | `icacls`, `takeown` |
| Packages | `winget` |
| Documentation | `help`, `command /?` |
