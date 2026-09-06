# Linux Package Management, Sudo & Python Virtual Environments

> [!NOTE]
> This reference covers package management on Debian-based systems, `sudo` and root privileges, and Python virtual environments using `venv` and `pip`. The package-management examples primarily target Debian, Ubuntu and Raspberry Pi OS.

---

# Table of Contents

- [Package Management](#package-management)
  - [APT](#apt)
  - [DPKG](#dpkg)
  - [Repositories](#apt-repositories)
- [Sudo](#sudo)
  - [Sudoers](#sudoers)
  - [Root User](#root-user)
- [Python Virtual Environments](#python-virtual-environments)
  - [venv](#venv)
  - [pip](#pip)
  - [Requirements Files](#requirements-files)
  - [pipx](#pipx)
- [Common Workflows](#common-workflows)
- [Troubleshooting](#troubleshooting)
- [Best Practices](#best-practices)
- [Command Reference](#command-reference)

---

# Package Management

Linux distributions use package managers to install, update, remove and inspect software. On Debian-based systems, software is primarily distributed as `.deb` packages and managed through **APT** and **DPKG**.

| Tool | Syntax | Description |
|---|---|---|
| `apt` | `apt [command] [package]` | High-level package management and dependency resolution. |
| `apt-get` | `apt-get [command] [package]` | Lower-level APT interface commonly used in scripts and administration. |
| `apt-cache` | `apt-cache [command] [package]` | Query package metadata and cache information. |
| `dpkg` | `dpkg [options]` | Low-level Debian package management. |

```text
apt
 │
 ├── Repository metadata
 ├── Dependency resolution
 └── Package installation
        │
        ▼
      dpkg
        │
        ▼
    .deb package
```

> [!IMPORTANT]
> `apt` should normally be preferred for installing and managing packages because it handles dependencies and repositories. `dpkg` is primarily used when working directly with `.deb` files or inspecting the local package database.

## APT

APT is the primary high-level package-management tool on Debian-based systems.

| Command | Syntax | Description |
|---|---|---|
| Update | `sudo apt update` | Refresh repository package metadata. |
| Upgrade | `sudo apt upgrade` | Upgrade installed packages. |
| Full upgrade | `sudo apt full-upgrade` | Upgrade packages while allowing dependency changes. |
| Install | `sudo apt install PKG` | Install a package and dependencies. |
| Remove | `sudo apt remove PKG` | Remove a package while generally preserving configuration. |
| Purge | `sudo apt purge PKG` | Remove a package and its package configuration. |
| Search | `apt search TERM` | Search available packages. |
| Show | `apt show PKG` | Display package information. |
| Installed | `apt list --installed` | List installed packages. |
| Autoremove | `sudo apt autoremove` | Remove automatically installed unused dependencies. |
| Clean | `sudo apt clean` | Remove downloaded package files from the cache. |
| Autoclean | `sudo apt autoclean` | Remove obsolete package files from the cache. |
| Repair | `sudo apt --fix-broken install` | Attempt to repair broken dependencies. |

### Update Package Metadata

```bash
sudo apt update
```

Downloads current package indexes from configured repositories. It does **not** normally upgrade installed packages.

### Upgrade Packages

```bash
sudo apt upgrade
```

Installs available updates for installed packages without intentionally removing packages to satisfy dependency changes.

### Install Packages

```bash
sudo apt install git
```

Multiple packages:

```bash
sudo apt install git curl wget
```

### Remove Packages

```bash
sudo apt remove nginx
```

Remove package and its configuration:

```bash
sudo apt purge nginx
```

> [!NOTE]
> `remove` and `purge` are different:
>
> ```text
> remove → package removed, configuration may remain
> purge  → package and package configuration removed
> ```

### Search and Inspect Packages

```bash
apt search nginx
apt show nginx
```

List installed packages:

```bash
apt list --installed
```

Filter the output:

```bash
apt list --installed | grep python
```

### Upgrade With Dependency Changes

```bash
sudo apt full-upgrade
```

> [!WARNING]
> `full-upgrade` may install or remove packages to resolve dependency changes. Review the proposed changes before confirming.

### Unused Dependencies

```bash
sudo apt autoremove
```

Removes packages that were automatically installed as dependencies and are no longer required.

## DPKG

`dpkg` is the lower-level Debian package-management tool. It works directly with installed-package metadata and `.deb` files.

| Command | Syntax | Description |
|---|---|---|
| Install | `sudo dpkg -i FILE.deb` | Install a local `.deb` package. |
| List | `dpkg -l` | List package information. |
| Status | `dpkg -s PKG` | Show status of an installed package. |
| Files | `dpkg -L PKG` | List files installed by a package. |
| Owner | `dpkg -S PATH` | Find which package owns a file. |

Install a local package:

```bash
sudo dpkg -i application.deb
```

If dependencies are missing:

```bash
sudo apt --fix-broken install
```

Find which package owns a file:

```bash
dpkg -S /usr/bin/curl
```

List files installed by a package:

```bash
dpkg -L curl
```

## APT Repositories

APT obtains package metadata and packages from configured repositories. Configuration is commonly located in:

```text
/etc/apt/sources.list
/etc/apt/sources.list.d/
```

Typical flow:

```text
Repository
    │
    ▼
apt update
    │
    ▼
Package metadata
    │
    ▼
apt install
```

> [!WARNING]
> Third-party repositories should only be added when their origin and compatibility with the current distribution release are trusted and understood.

---

# Sudo

`sudo` allows an authorized user to execute a command with elevated privileges without logging in directly as `root`.

| Command | Syntax | Description |
|---|---|---|
| `sudo` | `sudo COMMAND` | Execute a command with elevated privileges. |
| `sudo -u` | `sudo -u USER COMMAND` | Execute a command as another user. |
| `sudo -i` | `sudo -i` | Start a root login shell. |
| `sudo -s` | `sudo -s` | Start a shell with elevated privileges. |
| `sudo -l` | `sudo -l` | List the user's sudo permissions. |
| `sudo -k` | `sudo -k` | Invalidate cached sudo credentials. |
| `sudo -v` | `sudo -v` | Validate or refresh sudo credentials. |
| `visudo` | `sudo visudo` | Safely edit sudoers configuration. |

Example:

```bash
sudo apt update
```

When authentication is required, `sudo` normally requests the **current user's password**.

```text
[sudo] password for yavor:
```

The password is not displayed while typing.

### Execute as Another User

```bash
sudo -u postgres psql
```

Runs `psql` as the `postgres` user.

### Root Login Shell

```bash
sudo -i
```

This creates an interactive root login shell.

Exit:

```bash
exit
```

> [!WARNING]
> Commands executed from a root shell have extensive system privileges. Prefer `sudo COMMAND` for individual administrative operations when possible.

### List Sudo Permissions

```bash
sudo -l
```

Displays the commands the current user is permitted to execute through `sudo`.

---

# Sudoers

Sudo permissions are controlled through:

```text
/etc/sudoers
/etc/sudoers.d/
```

> [!IMPORTANT]
> Always use `visudo` to modify sudoers configuration:
>
> ```bash
> sudo visudo
> ```
>
> `visudo` validates the configuration syntax before applying the changes.

A basic sudoers rule follows the general form:

```text
USER HOST=(RUNAS) COMMAND
```

Example:

```text
yavor ALL=(ALL) ALL
```

A more restricted rule:

```text
yavor ALL=(root) /usr/bin/systemctl restart nginx
```

The second example grants permission for a specific command rather than unrestricted root access.

> [!TIP]
> Follow the **principle of least privilege**: grant only the permissions required for the task.

---

# Root User

`root` is the Linux superuser account with extensive control over the system.

| Item | Value |
|---|---|
| Username | `root` |
| Home directory | `/root` |
| Default prompt commonly ends with | `#` |

A normal user typically has a prompt such as:

```text
user@server:~$
```

Root commonly appears as:

```text
root@server:~#
```

`sudo` provides a mechanism for authorized users to execute commands with root or another user's privileges without permanently changing the login identity.

---

# Python Virtual Environments

Python virtual environments isolate project dependencies from the system Python installation and from other projects.

```text
System Python
     │
     ├── Project A
     │     └── .venv
     │
     └── Project B
           └── .venv
```

This allows projects to use different package versions without interfering with one another.

> [!IMPORTANT]
> A virtual environment is normally a local, disposable directory. Do not commit `.venv/` to Git and do not copy an existing environment between machines; recreate it from the project's dependency definition instead.

---

# venv

`venv` is Python's standard-library module for creating virtual environments.

| Command | Syntax | Description |
|---|---|---|
| Create | `python3 -m venv DIR` | Create a virtual environment. |
| Activate | `source DIR/bin/activate` | Activate it in Bash/Zsh. |
| Deactivate | `deactivate` | Leave the active environment. |
| System packages | `python3 -m venv --system-site-packages DIR` | Allow access to system site-packages. |
| Clear | `python3 -m venv --clear DIR` | Clear an existing environment before creation. |

## Create

```bash
python3 -m venv .venv
```

Typical project:

```text
project/
├── .venv/
├── src/
└── requirements.txt
```

## Activate

```bash
source .venv/bin/activate
```

The prompt commonly changes to:

```text
(.venv) user@host:~/project$
```

Activation places the environment's executable directory first in `PATH`.

## Verify the Environment

```bash
which python
```

Typical output:

```text
/home/user/project/.venv/bin/python
```

You can also check:

```bash
python -c "import sys; print(sys.prefix)"
```

To determine whether the interpreter is inside a virtual environment:

```bash
python -c "import sys; print(sys.prefix != sys.base_prefix)"
```

`True` indicates that the interpreter is running inside a virtual environment.

## Deactivate

```bash
deactivate
```

This restores the shell to the previous environment.

## Delete

A virtual environment can normally be removed by deleting its directory:

```bash
rm -rf .venv
```

Then recreate it:

```bash
python3 -m venv .venv
```

> [!WARNING]
> Verify the path before using `rm -rf`.

---

# pip

`pip` is the standard Python package installer.

| Command | Syntax | Description |
|---|---|---|
| Install | `python -m pip install PKG` | Install a package. |
| Specific version | `python -m pip install PKG==VERSION` | Install a specific version. |
| Upgrade | `python -m pip install --upgrade PKG` | Upgrade a package. |
| Uninstall | `python -m pip uninstall PKG` | Remove a package. |
| List | `python -m pip list` | List installed packages. |
| Show | `python -m pip show PKG` | Show package information. |
| Freeze | `python -m pip freeze` | Output installed packages and versions. |
| Requirements | `python -m pip install -r FILE` | Install from a requirements file. |
| Version | `python -m pip --version` | Show pip version and location. |

> [!TIP]
> Prefer:
>
> ```bash
> python -m pip
> ```
>
> instead of simply:
>
> ```bash
> pip
> ```
>
> This makes it explicit which Python interpreter is being used.

## Install Package

```bash
python -m pip install requests
```

Multiple packages:

```bash
python -m pip install requests flask numpy
```

## Install Specific Version

```bash
python -m pip install requests==2.32.0
```

## Upgrade

```bash
python -m pip install --upgrade requests
```

## Uninstall

```bash
python -m pip uninstall requests
```

## List Packages

```bash
python -m pip list
```

## Package Information

```bash
python -m pip show requests
```

---

# Requirements Files

A `requirements.txt` file records project dependencies.

Example:

```text
requests==2.32.0
flask>=3.0
numpy
```

Install all requirements:

```bash
python -m pip install -r requirements.txt
```

A common way to capture an existing environment is:

```bash
python -m pip freeze > requirements.txt
```

> [!NOTE]
> `pip freeze` records the currently installed packages and versions. It is useful for reproducing an environment, but a project's requirements file may instead be maintained manually to describe its intended direct dependencies.

---

# pipx

`pipx` is designed primarily for installing standalone Python command-line applications into isolated environments.

| Tool | Purpose |
|---|---|
| `venv` | Isolate a Python project environment. |
| `pip` | Install Python packages. |
| `pipx` | Install standalone Python CLI applications in isolated environments. |

Example:

```bash
pipx install black
```

Conceptually:

```text
pipx
 ├── black environment
 ├── tool environment
 └── ...
```

This keeps standalone CLI applications isolated while making their executables available through `PATH`.

---

# Common Workflows

## Install System Software

```bash
sudo apt update
sudo apt install git
```

## Update Debian/Ubuntu System

```bash
sudo apt update
sudo apt upgrade
```

## Install Python Environment Support

```bash
sudo apt install python3 python3-venv python3-pip
```

> [!NOTE]
> Exact package names can vary between distributions and releases.

## Create a Python Project

```bash
mkdir my-project
cd my-project
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
```

Install dependencies:

```bash
python -m pip install requests
```

Save the environment:

```bash
python -m pip freeze > requirements.txt
```

Leave the environment:

```bash
deactivate
```

## Recreate the Environment

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
```

---

# Troubleshooting

| Problem | Command / Solution |
|---|---|
| Package not found | `sudo apt update` then `apt search PKG` |
| Broken APT dependencies | `sudo apt --fix-broken install` |
| Missing `venv` | Install `python3-venv` |
| Missing `pip` | Install `python3-pip` where appropriate |
| Wrong Python | `which python` / `python --version` |
| Wrong pip | `python -m pip --version` |
| Permission error installing system package | Use `sudo` when administrative access is required |
| Python package conflicts | Create and use a `.venv` |

### `Unable to locate package`

```bash
sudo apt update
apt search <package>
```

### Broken Dependencies

```bash
sudo apt --fix-broken install
```

### Missing `venv`

On Debian-based systems:

```bash
sudo apt install python3-venv
```

Then:

```bash
python3 -m venv .venv
```

### Check Python and pip

```bash
which python
python --version
python -m pip --version
```

Inside a virtual environment, the executable paths should normally point into:

```text
.venv/bin/
```

---

# Best Practices

> [!TIP]
> **APT**
>
> Use `apt` for normal package management, update package metadata before upgrades or installations when appropriate, and review package changes before confirming removals or full upgrades.

> [!TIP]
> **Sudo**
>
> Use elevated privileges only when required, prefer specific `sudo COMMAND` invocations over long-lived root shells, edit `/etc/sudoers` only through `visudo`, and follow least privilege.

> [!TIP]
> **Python**
>
> Use a separate `.venv` per project, keep `.venv/` out of Git, prefer `python -m pip`, avoid `sudo pip install` for project dependencies, and recreate environments instead of copying them between systems.

---

# Command Reference

## APT

| Command | Syntax | Description |
|---|---|---|
| Update | `sudo apt update` | Refresh package metadata. |
| Upgrade | `sudo apt upgrade` | Upgrade installed packages. |
| Full upgrade | `sudo apt full-upgrade` | Upgrade with dependency changes. |
| Install | `sudo apt install PKG` | Install a package. |
| Remove | `sudo apt remove PKG` | Remove a package. |
| Purge | `sudo apt purge PKG` | Remove package and configuration. |
| Search | `apt search TERM` | Search available packages. |
| Show | `apt show PKG` | Display package information. |
| Installed | `apt list --installed` | List installed packages. |
| Autoremove | `sudo apt autoremove` | Remove unused dependencies. |
| Clean | `sudo apt clean` | Clear package cache. |
| Autoclean | `sudo apt autoclean` | Remove obsolete cached packages. |
| Repair | `sudo apt --fix-broken install` | Repair broken dependencies. |

## DPKG

| Command | Syntax | Description |
|---|---|---|
| Install | `sudo dpkg -i FILE.deb` | Install local `.deb` package. |
| List | `dpkg -l` | List package information. |
| Status | `dpkg -s PKG` | Show installed package status. |
| Files | `dpkg -L PKG` | List package files. |
| Owner | `dpkg -S PATH` | Find package owning a file. |

## Sudo

| Command | Syntax | Description |
|---|---|---|
| Elevated command | `sudo COMMAND` | Run command with elevated privileges. |
| Other user | `sudo -u USER COMMAND` | Run command as another user. |
| Root shell | `sudo -i` | Start root login shell. |
| Privileged shell | `sudo -s` | Start elevated shell. |
| Permissions | `sudo -l` | Show sudo permissions. |
| Invalidate | `sudo -k` | Clear cached credentials. |
| Validate | `sudo -v` | Validate sudo credentials. |
| Sudoers | `sudo visudo` | Safely edit sudoers configuration. |

## Python `venv`

| Command | Syntax | Description |
|---|---|---|
| Create | `python3 -m venv .venv` | Create virtual environment. |
| Activate | `source .venv/bin/activate` | Activate environment. |
| Deactivate | `deactivate` | Leave environment. |
| System packages | `python3 -m venv --system-site-packages .venv` | Allow system site-packages. |
| Clear | `python3 -m venv --clear .venv` | Clear existing environment. |

## pip

| Command | Syntax | Description |
|---|---|---|
| Install | `python -m pip install PKG` | Install package. |
| Specific version | `python -m pip install PKG==VERSION` | Install specific version. |
| Upgrade | `python -m pip install --upgrade PKG` | Upgrade package. |
| Uninstall | `python -m pip uninstall PKG` | Remove package. |
| List | `python -m pip list` | List installed packages. |
| Show | `python -m pip show PKG` | Show package information. |
| Freeze | `python -m pip freeze` | Output installed packages and versions. |
| Requirements | `python -m pip install -r requirements.txt` | Install requirements. |
| Version | `python -m pip --version` | Show pip version and location. |

---

# Essential Workflows

### Debian Package

```bash
sudo apt update
sudo apt install <package>
```

### System Upgrade

```bash
sudo apt update
sudo apt upgrade
```

### Python Environment

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install <package>
deactivate
```

### Recreate Python Environment

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
```
