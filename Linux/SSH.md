# SSH Reference

> [!NOTE]
> **SSH (Secure Shell)** is a cryptographic network protocol used to securely access and manage remote systems over an untrusted network.
>
> SSH encrypts all communication between the client and the server, protecting authentication credentials, terminal sessions and transferred data.

> [!IMPORTANT]
> Unless otherwise specified, all commands in this document are executed from the **local machine** (SSH Client).

---

# Table of Contents

- Overview
- SSH Architecture
- Connecting to Remote Hosts
- Authentication
- SSH Keys
- SSH Agent
- File Transfer
- Configuration Files
- SSH Server
- Port Forwarding
- Security Best Practices
- Troubleshooting
- Command Reference

---

# Overview

SSH replaces insecure protocols such as:

- Telnet
- Rlogin
- RSH
- FTP (when interactive access is required)

SSH provides:

- Secure remote terminal access
- File transfer
- Port forwarding
- Tunneling
- Authentication using passwords or public keys
- Remote command execution

---

# SSH Architecture

SSH communication always consists of two components.

| Component | Description |
|------------|-------------|
| SSH Client | The computer initiating the connection. |
| SSH Server | The computer accepting incoming SSH connections. |

Example

```
┌──────────────┐
│ Local Laptop │
│ SSH Client   │
└──────┬───────┘
       │
Encrypted SSH Connection
       │
       ▼
┌──────────────┐
│ Raspberry Pi │
│ SSH Server   │
└──────────────┘
```

Typical examples

| Client | Server |
|----------|---------|
| Windows PC | Raspberry Pi |
| Linux Laptop | Ubuntu Server |
| macOS | VPS |
| Desktop PC | NAS |

---

# Connecting to Remote Hosts

## Overview

The primary SSH command is:

```bash
ssh
```

This command opens an encrypted terminal session with a remote server.

---

# Commands

| Command | Syntax | Description |
|----------|--------|-------------|
| `ssh` | `ssh USER@HOST` | Connect to a remote host. |
| `ssh` | `ssh USER@IP` | Connect using an IP address. |
| `ssh` | `ssh -p PORT USER@HOST` | Connect using a custom port. |
| `ssh` | `ssh -i KEY USER@HOST` | Connect using a specific private key. |
| `ssh` | `ssh -v USER@HOST` | Display verbose connection information. |
| `ssh` | `ssh -vv USER@HOST` | More detailed debugging output. |
| `ssh` | `ssh -vvv USER@HOST` | Maximum debugging information. |

---

# Command

## ssh

Creates an encrypted terminal session with a remote SSH server.

---

### Syntax

```bash
ssh [OPTIONS] USER@HOST
```

---

### Parameters

| Parameter | Description |
|------------|-------------|
| `USER` | Username on the remote machine. |
| `HOST` | Hostname or IP address. |
| `OPTIONS` | Optional SSH command-line options. |

---

### Common Options

| Option | Description |
|----------|-------------|
| `-p` | Specify the remote SSH port. |
| `-i` | Specify the private key file. |
| `-v` | Enable verbose output. |
| `-vv` | More verbose output. |
| `-vvv` | Maximum debug output. |
| `-X` | Enable X11 Forwarding. |
| `-Y` | Trusted X11 Forwarding. |
| `-A` | Enable SSH Agent Forwarding. |
| `-J` | Connect through a Jump Host. |
| `-L` | Local Port Forwarding. |
| `-R` | Remote Port Forwarding. |
| `-D` | Dynamic SOCKS Proxy. |

---

### Examples

Connect using hostname

```bash
ssh pi@raspberrypi.local
```

---

Connect using an IP address

```bash
ssh ubuntu@192.168.1.50
```

---

Connect using a custom port

```bash
ssh -p 2222 ubuntu@server.example.com
```

---

Connect using a private key

```bash
ssh -i ~/.ssh/id_ed25519 ubuntu@server
```

---

Enable verbose output

```bash
ssh -v ubuntu@server
```

---

Maximum debug information

```bash
ssh -vvv ubuntu@server
```

---

Execute a single command remotely

```bash
ssh ubuntu@server "hostname"
```

Output

```text
ubuntu-server
```

---

Restart a service remotely

```bash
ssh ubuntu@server "sudo systemctl restart nginx"
```

---

Check available disk space

```bash
ssh ubuntu@server "df -h"
```

---

### Notes

> [!NOTE]
> If no port is specified, SSH automatically connects to TCP port **22**.

> [!TIP]
> Hostnames (for example `server.local`) are usually easier to remember than IP addresses.

> [!IMPORTANT]
> The first time you connect to a server, SSH asks whether you trust the server's host key.
>
> Type:
>
> ```text
> yes
> ```
>
> The host key is then stored in:
>
> ```text
> ~/.ssh/known_hosts
> ```

---

### Related Commands

- ssh-keygen
- ssh-copy-id
- ssh-add
- ssh-agent
- scp
- sftp

---

# Connection Process

A typical SSH connection follows these steps.

```
User executes

ssh ubuntu@server

        │
        ▼

DNS lookup (optional)

        │
        ▼

TCP connection

        │
        ▼

Server presents Host Key

        │
        ▼

Client verifies Host Key

        │
        ▼

Authentication

        │
        ▼

Encrypted Session Established

        │
        ▼

Remote Shell
```

> [!TIP]
> If authentication succeeds, your terminal is now executing commands **on the remote machine**, not on your local computer.

---

# Quick Reference

| Task | Command |
|--------|----------|
| Connect to server | `ssh USER@HOST` |
| Connect by IP | `ssh USER@IP` |
| Custom port | `ssh -p PORT USER@HOST` |
| Private key | `ssh -i KEY USER@HOST` |
| Verbose mode | `ssh -v USER@HOST` |
| Maximum debugging | `ssh -vvv USER@HOST` |
| Execute remote command | `ssh USER@HOST "COMMAND"` |

---

# Authentication

> [!NOTE]
> Authentication is the process of verifying the identity of a user before access to a remote system is granted.
>
> SSH supports multiple authentication methods, the most common being **password authentication** and **public key authentication**.

---

# Authentication Process

Every SSH connection follows the same authentication sequence.

```
┌──────────────┐
│ SSH Client   │
└──────┬───────┘
       │
       │ Connect to server
       ▼
┌──────────────┐
│ SSH Server   │
└──────┬───────┘
       │
       │ Exchange encryption keys
       ▼
Verify Server Identity
       │
       ▼
Authenticate User
       │
       ▼
Access Granted
```

Authentication begins **after** the encrypted connection has been established.

---

# Authentication Methods

SSH supports several authentication methods.

| Method | Description | Recommended |
|----------|-------------|-------------|
| Password Authentication | Authenticate using the user's password. | ⚠️ No |
| Public Key Authentication | Authenticate using an SSH key pair. | ✅ Yes |
| Keyboard Interactive | Authentication through PAM or MFA. | Depends |
| Host-Based Authentication | Authenticate trusted hosts. | Rare |
| GSSAPI / Kerberos | Enterprise authentication. | Enterprise |

> [!IMPORTANT]
> Modern Linux servers should use **Public Key Authentication** whenever possible.

---

# Password Authentication

## Overview

Password authentication requires the user to enter the password of the remote account.

Example

```bash
ssh ubuntu@192.168.1.50
```

Output

```text
ubuntu@192.168.1.50's password:
```

Enter the password.

If the password is correct, the SSH session starts.

---

## Advantages

- Simple
- No setup required
- Supported by every SSH server

---

## Disadvantages

- Vulnerable to brute-force attacks
- Passwords may be weak
- Requires entering the password for every connection
- Less secure than SSH keys

---

# Public Key Authentication

## Overview

Public Key Authentication replaces passwords with a cryptographic key pair.

Instead of proving your identity by entering a password, your computer proves ownership of a private key.

No password is transmitted over the network.

---

## Key Pair

Every key pair consists of two files.

| Key | Description | Keep Secret |
|------|-------------|-------------|
| Public Key | Shared with servers. | No |
| Private Key | Stored only on the client. | Yes |

Example

```
~/.ssh/
│
├── id_ed25519
└── id_ed25519.pub
```

| File | Description |
|------|-------------|
| `id_ed25519` | Private key |
| `id_ed25519.pub` | Public key |

> [!WARNING]
> Never share your private key.

---

# Authentication Using SSH Keys

The authentication process is completely automatic after the initial setup.

```
Client
│
│ Has Private Key
│
▼
Server
│
│ Has Public Key
│
▼
Server sends challenge
│
▼
Client signs challenge
│
▼
Server verifies signature
│
▼
Authentication successful
```

The private key never leaves the client computer.

---

# Host Keys

SSH also verifies the identity of the **server**.

This prevents attackers from impersonating another machine.

When connecting for the first time, SSH displays a message similar to:

```text
The authenticity of host 'server' can't be established.

Are you sure you want to continue connecting (yes/no)?
```

Type

```text
yes
```

The server's public host key is then stored locally.

---

# known_hosts

Previously trusted host keys are stored in

```text
~/.ssh/known_hosts
```

Purpose

- Remember trusted servers
- Detect server identity changes
- Prevent Man-in-the-Middle attacks

---

# authorized_keys

Servers store authorized public keys inside

```text
~/.ssh/authorized_keys
```

Purpose

- List users allowed to authenticate using SSH keys
- One public key per line

Example

```
~/.ssh/
│
└── authorized_keys
```

> [!NOTE]
> This file contains **public keys only**.
>
> Private keys are never copied to the server.

---

# Comparison

| Feature | Password | Public Key |
|----------|----------|------------|
| Security | Medium | High |
| Brute-force resistant | No | Yes |
| Convenient | Medium | High |
| Requires setup | No | Yes |
| Recommended | ❌ | ✅ |

---

# Best Practices

- Use **Ed25519** keys whenever possible.
- Disable password authentication after SSH keys are configured.
- Protect private keys with a passphrase.
- Never share private keys.
- Regularly remove unused public keys from `authorized_keys`.
- Verify unknown host fingerprints before accepting them.

---

# Related Commands

| Command | Purpose |
|----------|---------|
| `ssh-keygen` | Generate SSH key pairs |
| `ssh-copy-id` | Install a public key on a server |
| `ssh-add` | Add a key to the SSH agent |
| `ssh-agent` | Manage loaded private keys |

---

# Summary

| Concept | Description |
|----------|-------------|
| Authentication | Verifies the user's identity. |
| Password Authentication | Uses the user's password. |
| Public Key Authentication | Uses an SSH key pair. |
| Private Key | Secret key stored on the client. |
| Public Key | Key copied to the server. |
| Host Key | Identifies the server. |
| `authorized_keys` | Stores allowed public keys. |
| `known_hosts` | Stores trusted server identities. |

---