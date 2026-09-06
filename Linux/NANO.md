# Nano

> [!NOTE]
> **GNU nano** is a small, terminal-based text editor designed for straightforward text editing directly from the command line.
>
> Unlike modal editors such as Vim, Nano is **modeless**: typing normally inserts text, while editing operations are performed using keyboard shortcuts.
>
> Nano displays its most important shortcuts directly at the bottom of the editor, making it particularly suitable for quick file editing and for users who are not familiar with modal editors.
>
> The current GNU nano documentation lists **nano 9.2** as the latest version. Some shortcut bindings differ between older and newer releases, so this reference follows the current default bindings where applicable.

---

# Table of Contents
- [Opening Files](#opening-files)
- [Command Reference](#command-reference)
- [Command-Line Reference](#command-line-reference)
- [Nano Interface](#nano-interface)
- [Keyboard Shortcut Notation](#keyboard-shortcut-notation)
- [Basic Workflow](#basic-workflow)
- [Navigation](#navigation)
- [File Operations](#file-operations)
- [Editing Text](#editing-text)
- [Selection and Marking](#selection-and-marking)
- [Copy, Cut and Paste](#copy-cut-and-paste)
- [Searching](#searching)
- [Replacing Text](#replacing-text)
- [Go To Line and Position](#go-to-line-and-position)
- [Undo and Redo](#undo-and-redo)
- [Multiple Buffers](#multiple-buffers)
- [Justifying Text](#justifying-text)
- [Brackets and Matching](#brackets-and-matching)
- [Command Execution](#command-execution)
- [Mouse Support](#mouse-support)
- [Configuration](#configuration)
- [Command-Line Options](#command-line-options)
- [Help](#help)

---

# Opening Files

## Syntax

```bash
nano [options] [file]
```

Nano opens the specified file directly in the terminal.

If the file exists, Nano loads it for editing.

If the file does not exist, Nano opens an empty buffer using that filename. The file is created when the buffer is written to disk.

## Commands

| Command | Description |
|----------|-------------|
| `nano file.txt` | Open or create `file.txt`. |
| `nano file1 file2` | Open multiple files as buffers. |
| `nano +10 file.txt` | Open `file.txt` at line 10. |
| `nano file.txt:10` | Open `file.txt` at line 10. |
| `nano -v file.txt` | Open the file in view-only mode. |
| `nano -w file.txt` | Disable automatic line wrapping. |
| `nano -c file.txt` | Continuously display cursor position information. |

> [!NOTE]
> Current versions of Nano support both:
>
> ```bash
> nano +10 file.txt
> ```
>
> and:
>
> ```bash
> nano file.txt:10
> ```
>
> for opening a file at a particular line.

---


# Command-Line Reference

| Option | Syntax | Description |
|----------|--------|-------------|
| Help | `nano --help` | Display command-line help. |
| Version | `nano --version` | Display Nano version. |
| View | `nano -v FILE` | Open file in view mode. |
| No wrap | `nano -w FILE` | Disable line wrapping. |
| Auto indent | `nano -i FILE` | Enable automatic indentation. |
| Cursor position | `nano -c FILE` | Continuously show cursor position. |
| Mouse | `nano -m FILE` | Enable mouse support. |
| Line numbers | `nano -l FILE` | Display line numbers. |
| Tab size | `nano -T NUM FILE` | Set tab size. |
| Config file | `nano -f FILE` | Use a specific nanorc file. |
| Regex | `nano -R FILE` | Enable regular-expression search/replace. |

---

### Examples

Open a file:

```bash
nano notes.txt
```

Open a configuration file:

```bash
nano /etc/hosts
```

Open a file at line 50:

```bash
nano +50 server.conf
```

Open a file at line 50 using the filename form:

```bash
nano server.conf:50
```

---

# Nano Interface

When Nano is running, the terminal is divided into several logical areas.

```text
┌───────────────────────────────────────────────┐
│ nano 9.2                    notes.txt         │ ← Title
├───────────────────────────────────────────────┤
│                                               │
│                 File content                  │
│                                               │
│                                               │
├───────────────────────────────────────────────┤
│ [status / prompt / messages]                  │
├───────────────────────────────────────────────┤
│ ^G Help  ^O Write Out  ^F Where Is ...        │ ← Shortcut menu
│ ^X Exit  ^R Read File   ^\ Replace ...        │
└───────────────────────────────────────────────┘
```

## Interface Elements

| Area | Purpose |
|------|---------|
| Title bar | Displays Nano version and current file/buffer information. |
| Editing area | Displays and edits the file contents. |
| Status area | Displays prompts, messages, errors and operation results. |
| Shortcut area | Displays commonly used keyboard commands. |

> [!TIP]
> The shortcut list at the bottom is part of Nano's normal interface. You do not need to memorize every command before using the editor.

---

# Keyboard Shortcut Notation

Nano uses two main symbols for keyboard shortcuts.

## Control (`^`)

A caret means the **Ctrl** key.

For example:

```text
^X
```

means:

```text
Ctrl+X
```

Similarly:

```text
^O
```

means:

```text
Ctrl+O
```

## Meta (`M-`)

`M-` represents the **Meta** key.

On most modern systems, this is:

```text
Alt
```

For example:

```text
M-U
```

usually means:

```text
Alt+U
```

> [!NOTE]
> Depending on the terminal emulator and keyboard configuration, `Esc` may also be used as an alternative way to enter some Meta sequences.

---

# Basic Workflow

Nano does not require switching between Insert and Normal modes.

The basic workflow is:

```text
Open file
    │
    ▼
Edit text directly
    │
    ▼
Ctrl+O
    │
    ▼
Confirm filename with Enter
    │
    ▼
Continue editing or press Ctrl+X
```

## Example

Open:

```bash
nano notes.txt
```

Type:

```text
Hello Linux
This is a Nano example.
```

Save:

```text
Ctrl+O
```

Confirm:

```text
Enter
```

Exit:

```text
Ctrl+X
```

> [!IMPORTANT]
> Nano is **not modal** like Vim.
>
> You can normally type text immediately after opening a file. There is no separate Insert mode that you need to enter or leave.

---

# Navigation

Nano uses familiar cursor movement keys.

## Arrow Keys

| Key | Action |
|----------|--------|
| `↑` | Move up one line. |
| `↓` | Move down one line. |
| `←` | Move left one character. |
| `→` | Move right one character. |

---

## Navigation Shortcuts

| Shortcut | Description |
|----------|-------------|
| `Ctrl+B` | Move one character backward. |
| `Ctrl+F` | Move one character forward. |
| `Ctrl+P` | Move one line up. |
| `Ctrl+N` | Move one line down. |
| `Ctrl+A` | Move to the beginning of the line. |
| `Ctrl+E` | Move to the end of the line. |

> [!NOTE]
> In current Nano, `Ctrl+F` and `Ctrl+B` are bound to forward/backward character movement in the current default interface, and are also associated with search actions depending on Nano's bindings/configuration. When a shortcut starts a prompt, follow the prompt shown by Nano.

---

# Page and Buffer Navigation

## Commands

| Shortcut | Description |
|----------|-------------|
| `Ctrl+V` | Move down one screen/page. |
| `Ctrl+Y` | Move up one screen/page. |
| `Alt+\` | Go to the beginning of the buffer. |
| `Alt+/` | Go to the end of the buffer. |
| `Alt+<` | Switch to the previous buffer. |
| `Alt+>` | Switch to the next buffer. |

> [!NOTE]
> Nano's shortcut set has evolved between versions. The exact displayed shortcut menu in your installed version should be treated as authoritative for that installation.

---

# File Operations

## Save

### Syntax

```text
Ctrl+O
```

### Description

Writes the current buffer to disk.

The command is commonly called **Write Out** in Nano.

### Workflow

```text
Ctrl+O
```

Nano displays a prompt similar to:

```text
File Name to Write: notes.txt
```

Press:

```text
Enter
```

to confirm the filename.

### Example

```text
Ctrl+O
Enter
```

> [!NOTE]
> `Ctrl+O` does not normally close Nano. It saves the current buffer and returns you to the editor.

---

## Exit

### Syntax

```text
Ctrl+X
```

### Description

Exits Nano.

If the file has not been modified, Nano exits immediately.

If there are unsaved changes, Nano asks whether they should be saved.

Example prompt:

```text
Save modified buffer?
Y Yes
N No
^C Cancel
```

Press:

```text
Y
```

to save.

Press:

```text
N
```

to discard changes.

Press:

```text
Ctrl+C
```

to cancel the exit operation.

---

## Open Another File

### Syntax

```text
Ctrl+R
```

### Description

Reads a file into the current buffer at the current cursor position.

It can be used to insert the contents of another file into the document.

### Example

Suppose the current file contains:

```text
Start
End
```

Move the cursor between the two lines and press:

```text
Ctrl+R
```

Select another file:

```text
header.txt
```

Its content is inserted into the current buffer.

> [!IMPORTANT]
> `Ctrl+R` in Nano means **Read File**. It does not open a completely separate graphical editor window.

---

# Editing Text

Because Nano is modeless, normal typing directly inserts text.

## Delete Character Before Cursor

### Syntax

```text
Backspace
```

### Description

Deletes the character immediately before the cursor.

---

## Delete Character Under Cursor

### Syntax

```text
Ctrl+D
```

### Description

Deletes the character currently under the cursor.

---

## Delete Word to the Left

### Syntax

```text
Alt+Backspace
```

### Description

Deletes the word immediately to the left of the cursor.

---

## Delete Word to the Right

### Syntax

```text
Ctrl+Delete
```

### Description

Deletes the word immediately to the right of the cursor.

---

## Delete Current Line

### Syntax

```text
Alt+Delete
```

### Description

Deletes the current line.

---

# Copy, Cut and Paste

Nano uses a **cutbuffer** for cut and paste operations.

---

## Cut Current Line

### Syntax

```text
Ctrl+K
```

### Description

Cuts the current line into Nano's cutbuffer.

The line is removed from the document and can later be pasted.

### Example

Before:

```text
line 1
line 2
line 3
```

Place the cursor on:

```text
line 2
```

Press:

```text
Ctrl+K
```

Result:

```text
line 1
line 3
```

The removed line is stored in the cutbuffer.

---

## Copy Current Line

### Syntax

```text
Alt+6
```

### Description

Copies the current line into the cutbuffer without removing it.

### Example

```text
line 1
line 2
line 3
```

Place the cursor on `line 2`.

Press:

```text
Alt+6
```

The buffer remains:

```text
line 1
line 2
line 3
```

The contents of `line 2` can then be pasted elsewhere.

---

## Paste

### Syntax

```text
Ctrl+U
```

### Description

Pastes the contents of the cutbuffer at the current cursor position.

### Example

After copying or cutting:

```text
Ctrl+U
```

inserts the stored text.

> [!TIP]
> A common copy-and-paste workflow is:
>
> ```text
> Alt+6
> ↓
> Move cursor
> ↓
> Ctrl+U
> ```

---

# Selection and Marking

Nano uses a **mark** to define a selected region of text.

## Set Mark

### Syntax

```text
Ctrl+6
```

### Description

Sets the beginning of a selection.

Move the cursor after setting the mark to extend the selected region.

The selected region is highlighted.

---

## Selection Workflow

```text
Move cursor to beginning
        │
        ▼
    Ctrl+6
        │
        ▼
Move cursor
        │
        ▼
Selected region
```

After selecting text, operations such as cut or copy can be applied.

---

## Cut Selected Text

Press:

```text
Ctrl+K
```

The selected region is removed and placed into the cutbuffer.

---

## Copy Selected Text

Press:

```text
Alt+6
```

The selected region is copied without deleting it.

---

## Cancel Selection

Move the cursor normally or press:

```text
Ctrl+6
```

again to change the marking state.

> [!NOTE]
> Nano's exact mark-related shortcuts can be confirmed through:
>
> ```text
> Ctrl+G
> ```
>
> and the shortcut list displayed by the current Nano version.

---

# Searching

Nano provides interactive forward and backward searching.

## Search Forward

### Syntax

```text
Ctrl+W
```

### Description

Starts a forward search.

Depending on the current Nano bindings/version, forward search may also be bound differently. The bottom help menu shows the active binding. Current GNU nano defaults include forward-search functionality directly in the editor.

### Workflow

```text
Ctrl+W
```

Nano displays a prompt:

```text
Search:
```

Type:

```text
server
```

Press:

```text
Enter
```

Nano moves to the matching occurrence.

---

# Searching Forward and Backward

Current Nano versions provide dedicated search-direction commands.

| Shortcut | Description |
|----------|-------------|
| `Ctrl+F` | Start forward search. |
| `Ctrl+B` | Start backward search. |
| `Alt+F` | Find next occurrence forward. |
| `Alt+B` | Find next occurrence backward. |

> [!NOTE]
> Search bindings have changed across Nano releases. For example, GNU nano 8.0 changed the default bindings so `Ctrl+F` starts forward search and `Ctrl+B` starts backward search, while `Alt+F` and `Alt+B` repeat searches in the corresponding directions.

---

# Replacing Text

## Replace

### Syntax

```text
Alt+R
```

### Description

Starts an interactive search-and-replace operation.

### Workflow

1. Press:

```text
Alt+R
```

2. Enter the text to search for.

3. Press:

```text
Enter
```

4. Enter the replacement text.

5. Press:

```text
Enter
```

Nano then steps through matching occurrences and allows them to be replaced.

---

# Go To Line and Position

## Go To Line

### Syntax

```text
Ctrl+/
```

or, depending on the current Nano binding:

```text
Ctrl+_
```

### Description

Opens the line/column prompt.

Example:

```text
Line number, column number:
```

Enter:

```text
25,10
```

Nano moves the cursor to line 25, column 10.

> [!NOTE]
> The exact displayed key for the Go To Line operation may depend on the Nano version and active bindings. Use the shortcut shown in the bottom menu or `Ctrl+G` help.

---

# Undo and Redo

Nano maintains an undo history for editing operations.

## Undo

### Syntax

```text
Alt+U
```

### Description

Undoes the most recent editing operation.

Example:

```text
Type:
hello
```

Press:

```text
Alt+U
```

The previous operation is undone.

---

## Redo

### Syntax

```text
Alt+E
```

### Description

Redoes the most recently undone operation.

### Workflow

```text
Alt+U
```

Undo.

```text
Alt+E
```

Redo.

> [!TIP]
> Undo and redo operate on Nano's editing history and can be used repeatedly to move backward and forward through recent changes.

The current GNU nano shortcut reference lists `Alt+U` for Undo and `Alt+E` for Redo.

---

# Multiple Buffers

Nano can keep multiple files open as buffers.

## Open Multiple Files

From the terminal:

```bash
nano file1.txt file2.txt file3.txt
```

Nano loads the files as separate buffers.

---

## Switch to Previous Buffer

### Syntax

```text
Alt+<
```

### Description

Switches to the preceding open buffer.

---

## Switch to Next Buffer

### Syntax

```text
Alt+>
```

### Description

Switches to the following open buffer.

---

# Justifying Text

Nano includes commands for formatting paragraphs.

## Justify Current Paragraph or Region

### Syntax

```text
Ctrl+J
```

### Description

Justifies the current paragraph or selected region.

---

## Justify Entire Buffer

### Syntax

```text
Alt+J
```

### Description

Justifies the entire buffer.

> [!NOTE]
> Justification is primarily useful for prose rather than source code or configuration files.

---

# Brackets and Matching

Nano can help locate matching brackets.

## Go To Matching Bracket

### Syntax

```text
Alt+]
```

### Description

Moves the cursor to the matching bracket.

Supported bracket types include:

```text
()
[]
{}
```

### Example

For:

```c
if (value > 10) {
    printf("Hello");
}
```

Place the cursor on `{` and press:

```text
Alt+]
```

Nano moves to the corresponding `}`.

---

# Command Execution

Nano can execute commands through its command execution functionality.

## Execute Command

### Syntax

```text
Ctrl+T
```

### Description

Opens Nano's command-execution functionality.

Depending on the configured command and Nano version, this can be used for operations such as running external tools.

> [!NOTE]
> The exact prompt and available execution features depend on the Nano version and configuration.

Current Nano documentation also lists command execution and combinations for operations such as spell checking, syntax checking and formatting.

---

# Mouse Support

Nano supports mouse interaction when running in a compatible terminal.

Typical mouse actions include:

| Action | Description |
|----------|-------------|
| Left click | Move the cursor. |
| Mouse wheel | Scroll the viewport. |
| Selection | Select text using terminal mouse support where supported. |

> [!NOTE]
> Mouse behavior depends on the terminal emulator and its mouse configuration.

Current GNU nano releases use the mouse wheel to scroll the viewport rather than moving the cursor.

---

# Configuration

Nano can be configured using a `nanorc` configuration file.

## User Configuration

Typical location:

```text
~/.nanorc
```

## System Configuration

Typical system-wide configuration:

```text
/etc/nanorc
```

The exact system path can vary by distribution.

---

# Example Configuration

```text
set linenumbers
set mouse
set autoindent
set tabsize 4
set tabstospaces
set constantshow
```

---

# Common Configuration Options

| Option | Description |
|----------|-------------|
| `set linenumbers` | Display line numbers. |
| `set mouse` | Enable mouse support. |
| `set autoindent` | Automatically indent new lines. |
| `set tabsize 4` | Set tab width to four spaces/columns. |
| `set tabstospaces` | Convert typed tabs to spaces. |
| `set constantshow` | Continuously display cursor position. |
| `set softwrap` | Enable soft wrapping of long lines. |
| `set nowrap` | Disable wrapping. |

> [!NOTE]
> Nano configuration syntax is version-dependent. Check the installed `nanorc` manual for options supported by your version.

---

# Syntax Highlighting

Nano supports syntax highlighting through `nanorc` configuration.

Example:

```text
include "/usr/share/nano/*.nanorc"
```

This allows Nano to load syntax definitions supplied by the system.

Depending on the distribution, syntax definitions may be stored under paths such as:

```text
/usr/share/nano/
```

---

# Command-Line Options

Nano supports many command-line options.

## Common Options

| Option | Description |
|----------|-------------|
| `-h` | Display help. |
| `-V` | Display version information. |
| `-v` | View file without editing. |
| `-w` | Disable line wrapping. |
| `-i` | Enable automatic indentation. |
| `-c` | Continuously display cursor position. |
| `-m` | Enable mouse support. |
| `-l` | Display line numbers. |
| `-T NUM` | Set tab size. |
| `-f FILE` | Use specified nanorc file. |
| `-Y STR` | Syntax highlighting language. |
| `-R` | Enable regular expression search/replace. |

> [!IMPORTANT]
> Command-line options depend on the Nano version. Use:
>
> ```bash
> nano --help
> ```
>
> to see the options supported by the version installed on your system.

---

# Command-Line Examples

Display Nano help:

```bash
nano --help
```

Display version:

```bash
nano --version
```

Open a file without line wrapping:

```bash
nano -w notes.txt
```

Open a file with line numbers:

```bash
nano -l source.c
```

Open a file with automatic indentation:

```bash
nano -i source.c
```

Set tab width:

```bash
nano -T 4 source.c
```

---

# Help

Nano includes built-in documentation.

## Open Help

### Syntax

```text
Ctrl+G
```

### Description

Displays Nano's built-in help screen.

The help system is especially useful when you forget a shortcut.

---

## Help Workflow

```text
Ctrl+G
```

Read the documentation.

Return to the editor using the indicated exit command.

---

# Common Editing Workflow

## Create a New File

```bash
nano test.txt
```

Type:

```text
Hello Linux
Nano is a terminal text editor.
```

Save:

```text
Ctrl+O
Enter
```

Exit:

```text
Ctrl+X
```

---

# Editing an Existing Configuration File

Example:

```bash
nano ~/.bashrc
```

Make the desired changes.

Save:

```text
Ctrl+O
Enter
```

Exit:

```text
Ctrl+X
```

---

# Editing a System File

For files requiring administrator privileges:

```bash
sudo nano /etc/hosts
```

or:

```bash
sudo nano /etc/ssh/sshd_config
```

> [!WARNING]
> Editing system configuration files as root can affect system operation.
>
> Verify the configuration before saving changes.

---

# Typical Remote Server Workflow

Nano is especially useful over SSH because it runs completely inside the terminal.

Example:

```bash
ssh user@server
```

Then:

```bash
nano ~/config.txt
```

Edit the file:

```text
Type changes
```

Save:

```text
Ctrl+O
Enter
```

Exit:

```text
Ctrl+X
```

Return to the remote shell.

Exit the SSH session:

```bash
exit
```

---

# Quick Reference

## Essential Shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl+O` | Write/save file |
| `Ctrl+X` | Exit Nano |
| `Ctrl+G` | Open help |
| `Ctrl+K` | Cut line/selection |
| `Ctrl+U` | Paste cutbuffer |
| `Alt+6` | Copy line/selection |
| `Ctrl+6` | Set/unset mark |
| `Alt+U` | Undo |
| `Alt+E` | Redo |
| `Ctrl+D` | Delete character under cursor |
| `Ctrl+A` | Beginning of line |
| `Ctrl+E` | End of line |
| `Ctrl+Y` | Page up |
| `Ctrl+V` | Page down |
| `Alt+\` | Beginning of buffer |
| `Alt+/` | End of buffer |
| `Alt+<` | Previous buffer |
| `Alt+>` | Next buffer |
| `Alt+R` | Replace |
| `Alt+]` | Matching bracket |
| `Ctrl+T` | Execute command |

---

# Search Reference

| Shortcut | Action |
|----------|--------|
| `Ctrl+F` | Forward search |
| `Ctrl+B` | Backward search |
| `Alt+F` | Next match forward |
| `Alt+B` | Next match backward |
| `Alt+R` | Search and replace |

> [!NOTE]
> Search shortcuts changed in GNU nano 8.0. Older Nano versions may display different bindings. Always use the shortcut menu and `Ctrl+G` help of the installed version as the final reference.

---

# File Reference

| File | Purpose |
|----------|-------------|
| `~/.nanorc` | User-specific Nano configuration |
| `/etc/nanorc` | System-wide Nano configuration |
| `/usr/share/nano/` | Common location for syntax definitions |

---

# Nano vs Vim

| Feature | Nano | Vim |
|----------|------|-----|
| Editing model | Modeless | Modal |
| Initial learning curve | Low | Higher |
| Basic typing | Immediate | Requires Insert mode |
| On-screen shortcuts | Yes | No |
| Plugins | Limited | Extensive |
| Terminal editing | Yes | Yes |
| Configuration | `nanorc` | `.vimrc` |
| Best suited for | Quick editing | Advanced editing workflows |

---

# Command Reference

## File Handling

| Command | Syntax | Description |
|----------|--------|-------------|
| `nano` | `nano [options] [file]` | Start Nano and optionally open a file. |
| `Ctrl+O` | `Ctrl+O` | Write the current buffer to disk. |
| `Ctrl+X` | `Ctrl+X` | Exit Nano. |
| `Ctrl+R` | `Ctrl+R` | Read another file into the current buffer. |

## Navigation

| Command | Syntax | Description |
|----------|--------|-------------|
| Move left | `←` / `Ctrl+B` | Move cursor left. |
| Move right | `→` / `Ctrl+F` | Move cursor right. |
| Move up | `↑` / `Ctrl+P` | Move cursor up. |
| Move down | `↓` / `Ctrl+N` | Move cursor down. |
| Line start | `Ctrl+A` | Move to beginning of line. |
| Line end | `Ctrl+E` | Move to end of line. |
| Page up | `Ctrl+Y` | Move up one screen. |
| Page down | `Ctrl+V` | Move down one screen. |
| Buffer start | `Alt+\` | Go to beginning of buffer. |
| Buffer end | `Alt+/` | Go to end of buffer. |

## Editing

| Command | Syntax | Description |
|----------|--------|-------------|
| Delete previous character | `Backspace` | Delete character before cursor. |
| Delete character | `Ctrl+D` | Delete character under cursor. |
| Delete previous word | `Alt+Backspace` | Delete word to the left. |
| Delete next word | `Ctrl+Delete` | Delete word to the right. |
| Delete line | `Alt+Delete` | Delete current line. |
| Cut | `Ctrl+K` | Cut line or selected region. |
| Copy | `Alt+6` | Copy line or selected region. |
| Paste | `Ctrl+U` | Paste cutbuffer. |
| Mark | `Ctrl+6` | Set selection starting point. |

## Search and Replace

| Command | Syntax | Description |
|----------|--------|-------------|
| Forward search | `Ctrl+F` | Search forward. |
| Backward search | `Ctrl+B` | Search backward. |
| Next forward match | `Alt+F` | Find next occurrence forward. |
| Next backward match | `Alt+B` | Find next occurrence backward. |
| Replace | `Alt+R` | Start interactive search and replace. |

## Undo and Redo

| Command | Syntax | Description |
|----------|--------|-------------|
| Undo | `Alt+U` | Undo previous operation. |
| Redo | `Alt+E` | Redo previously undone operation. |

## Other Operations

| Command | Syntax | Description |
|----------|--------|-------------|
| Help | `Ctrl+G` | Open Nano help. |
| Execute | `Ctrl+T` | Execute an external command/function. |
| Justify | `Ctrl+J` | Justify paragraph or selected region. |
| Matching bracket | `Alt+]` | Jump to matching bracket. |
| Previous buffer | `Alt+<` | Switch to previous buffer. |
| Next buffer | `Alt+>` | Switch to next buffer. |

