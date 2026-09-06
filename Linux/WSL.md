
# Windows Subsystem for Linux (WSL)

> [!NOTE]
> WSL allows you to run a native Linux environment directly on Windows without using a virtual machine.

---

## Essential Commands

| Command | Description |
|----------|-------------|
| `wsl` | Start the default Linux distribution |
| `wsl -l -v` | List installed distributions |
| `wsl -d Ubuntu` | Start a specific distribution |
| `wsl --set-default Ubuntu` | Set the default distribution |
| `wsl --shutdown` | Stop all running WSL instances |
| `wsl --terminate Ubuntu` | Stop a specific distribution |
| `wsl --update` | Update the WSL kernel |
| `wsl --version` | Display the installed WSL version |

---

## Installation & Management

| Command | Purpose |
|----------|---------|
| `wsl --install` | Install WSL and the default Linux distribution |
| `wsl --install -d Ubuntu` | Install a specific distribution |
| `wsl --export Ubuntu backup.tar` | Export (backup) a distribution |
| `wsl --import Ubuntu D:\WSL backup.tar` | Import a distribution |
| `wsl --unregister Ubuntu` | Delete a distribution permanently |

> [!WARNING]
> `wsl --unregister` permanently removes the distribution and **all** its data.

---

## Windows ↔ Linux File System

WSL allows Windows and Linux to access each other's files.

### Windows → Linux

Open your Linux files directly from File Explorer:

```text
\\wsl$\Ubuntu
```

Example:

```text
\\wsl$\Ubuntu\home\yavor
```

---

### Linux → Windows

Windows drives are automatically mounted under `/mnt`.

| Windows Drive | Linux Path |
|--------------|------------|
| `C:\` | `/mnt/c` |
| `D:\` | `/mnt/d` |
| `E:\` | `/mnt/e` |

Example:

```bash
# write in Linux terminal
cd /mnt/c/Users/<username>/Desktop
```

---

### Open the Current Linux Directory in Windows

Launch File Explorer in the current Linux directory.

```bash
explorer.exe .
```

---

## Running Linux Commands from Windows

Execute Linux commands directly from **PowerShell** or **Command Prompt** without opening Ubuntu.

| Command | Description |
|---------|-------------|
| `wsl pwd` | Print the current directory |
| `wsl ls -la` | List files and directories |
| `wsl whoami` | Display the current Linux user |
| `wsl uname -a` | Show Linux system information |

Run a command as the **root** user:

```powershell
wsl -u root
```

