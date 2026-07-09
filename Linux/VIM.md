# Vim

> [!NOTE]
> Vim (Vi IMproved) is a modal text editor for Unix-like operating systems.
> Unlike traditional text editors, Vim separates editing into multiple modes.
> Understanding these modes is essential for efficient text editing.
---

# Opening Files

## Syntax

```bash
vim [options] <file>
```

## Commands

| Command | Description |
|----------|-------------|
| `vim file.txt` | Open or create file |
| `vim file1 file2` | Open multiple files |
| `vim +10 file.txt` | Open at line 10 |
| `vim +/main file.c` | Open at first match |
| `vim -R file.txt` | Read-only mode |

### Example

```bash
vim notes.txt
```

---

# Vim Modes

Vim operates in multiple modes.

> [!TIP]
> - **Normal mode** → Navigate and execute commands.
> - **Insert mode** → Write text.
> - **Visual mode** → Select text.
> - **Command mode (`:`)** → Save, quit, search, replace, and configure Vim.
>
> When in doubt, press **Esc** to return to **Normal mode**.

| Mode | Enter | Description |
|--------|--------|------------|
| Normal | `Esc` | Navigation and commands |
| Insert | `i` `I` `a` `A` `o` `O` | Insert text |
| Replace | `R` | Overwrite existing text |
| Visual | `v` | Character selection |
| Visual Line | `V` | Line selection |
| Visual Block | `Ctrl+v` | Column selection |
| Command | `:` | Execute Ex commands |

> [!IMPORTANT]
> Nearly every Vim command is executed from **Normal mode**.

## Switching Between Modes

Most editing in Vim follows the same workflow:

1. Open a file.
2. Vim starts in **Normal mode**.
3. Enter another mode (Insert, Visual, or Command).
4. Perform the desired action.
5. Return to **Normal mode** by pressing `Esc`.

> [!IMPORTANT]
> If a command such as `dd`, `yy`, or `:w` does not work, press **Esc** first. You are most likely not in **Normal mode**.

---

### Mode Transitions

| Current Mode | Action | Next Mode |
|--------------|--------|-----------|
| Normal | `i`, `a`, `o`, `R` | Insert / Replace |
| Normal | `v`, `V`, `Ctrl+v` | Visual |
| Normal | `:` | Command |
| Insert | `Esc` | Normal |
| Replace | `Esc` | Normal |
| Visual | `Esc` | Normal |
| Command | `Esc` or `Enter` | Normal |

---

# Insert Mode

Insert mode is used for typing and editing text.

Enter Insert mode from **Normal mode**.

| Key | Description |
|------|-------------|
| `i` | Insert before cursor |
| `I` | Insert at beginning of line |
| `a` | Insert after cursor |
| `A` | Insert at end of line |
| `o` | Insert a new line below |
| `O` | Insert a new line above |

Example:

```text
Normal Mode
      │
Press i
      │
      ▼
Insert Mode
      │
Type text
      │
Press Esc
      ▼
Normal Mode
```

> [!TIP]
> Pressing **Esc** does **not** close the file. It only returns Vim to **Normal mode**.

---

# Command Mode

Command mode is used to execute Vim commands such as saving files, quitting, searching, and replacing text.

Enter Command mode from **Normal mode** by pressing:

```text
:
```

The cursor moves to the bottom of the screen where you can type a command.

Execute the command by pressing:

```text
Enter
```

Examples:

Save the current file:

```vim
:w
```

Quit Vim:

```vim
:q
```

Save and quit:

```vim
:wq
```

Quit without saving:

```vim
:q!
```

> [!NOTE]
> Commands beginning with `:` are called **Ex commands**.

---

# Navigation

## Character Movement

| Key | Action |
|------|--------|
| `h` | Left |
| `j` | Down |
| `k` | Up |
| `l` | Right |

---

## Word Movement

| Command | Description |
|----------|-------------|
| `w` | Next word |
| `W` | Next WORD |
| `b` | Previous word |
| `B` | Previous WORD |
| `e` | End of word |
| `ge` | Previous word end |

---

## Line Movement

| Command | Description |
|----------|-------------|
| `0` | Beginning of line |
| `^` | First non-space |
| `$` | End of line |

---

## File Movement

| Command | Description |
|----------|-------------|
| `gg` | First line |
| `G` | Last line |
| `25G` | Line 25 |
| `Ctrl+d` | Half page down |
| `Ctrl+u` | Half page up |
| `Ctrl+f` | Full page down |
| `Ctrl+b` | Full page up |

---

# Editing

## Delete

| Command | Description |
|----------|-------------|
| `x` | Delete character |
| `X` | Delete previous character |
| `dd` | Delete line |
| `dw` | Delete word |
| `d$` | Delete to end of line |
| `d0` | Delete to beginning of line |
| `D` | Delete to end of line |

---

## Copy (Yank)

| Command | Description |
|----------|-------------|
| `yy` | Copy line |
| `yw` | Copy word |
| `y$` | Copy to end of line |

---

## Paste

| Command | Description |
|----------|-------------|
| `p` | Paste after cursor |
| `P` | Paste before cursor |

---

## Change

| Command | Description |
|----------|-------------|
| `cw` | Change word |
| `cc` | Change line |
| `C` | Change to end of line |
| `s` | Replace character and enter Insert mode |

---

## Undo / Redo

| Command | Description |
|----------|-------------|
| `u` | Undo |
| `Ctrl+r` | Redo |

---

# Visual Mode

| Command | Description |
|----------|-------------|
| `v` | Character selection |
| `V` | Line selection |
| `Ctrl+v` | Block selection |

Operations after selection:

| Key | Action |
|------|--------|
| `y` | Copy |
| `d` | Delete |
| `c` | Change |

> [!NOTE]
> Visual mode is similar to selecting text with a mouse in graphical editors.
> After selecting text, you can copy (`y`), delete (`d`), or change (`c`) the selection.

---

# Searching

| Command | Description |
|----------|-------------|
| `/text` | Search forward |
| `?text` | Search backward |
| `n` | Next result |
| `N` | Previous result |
| `*` | Search current word forward |
| `#` | Search current word backward |

---

# Replace

Current line

```vim
:s/old/new/
```

Entire file

```vim
:%s/old/new/g
```

Confirm every replacement

```vim
:%s/old/new/gc
```

---

# Saving

| Command | Description |
|----------|-------------|
| `:w` | Save |
| `:wa` | Save all files |
| `:q` | Quit |
| `:q!` | Quit without saving |
| `:wq` | Save and quit |
| `:x` | Save if modified |

## Typical Editing Session

Open a file:

```bash
vim notes.txt
```

Edit the file:

```text
Press i
Type your changes
Press Esc
```

Save and quit:

```vim
:wq
```

Quit without saving:

```vim
:q!
```

---

# Buffers

| Command | Description |
|----------|-------------|
| `:ls` | List buffers |
| `:bnext` | Next buffer |
| `:bprev` | Previous buffer |
| `:buffer N` | Switch to buffer N |

---

# Windows

Split windows

```vim
:split
:vsplit
```

Navigation

| Command | Description |
|----------|-------------|
| `Ctrl+w h` | Left window |
| `Ctrl+w j` | Lower window |
| `Ctrl+w k` | Upper window |
| `Ctrl+w l` | Right window |

---

# Tabs

| Command | Description |
|----------|-------------|
| `:tabnew` | New tab |
| `gt` | Next tab |
| `gT` | Previous tab |
| `:tabclose` | Close tab |

---

# Mouse Support

Enable mouse

```vim
:set mouse=a
```

Disable mouse

```vim
:set mouse=
```

| Action | Description |
|----------|-------------|
| Left Click | Move cursor |
| Drag | Select text |
| Scroll Wheel | Scroll document |

> [!NOTE]
> Mouse support depends on the terminal emulator.

---

# Configuration

Configuration file

```bash
~/.vimrc
```

Example

```vim
set number
set relativenumber
set autoindent
set tabstop=4
set shiftwidth=4
set expandtab
syntax on
set mouse=a
```

---

# Help

| Command | Description |
|----------|-------------|
| `:help` | Help |
| `:help dd` | Help for command |
| `:help motion.txt` | Motion documentation |



---

# Command Reference

| Category | Commands |
|-----------|----------|
| Movement | `hjkl` `w` `b` `e` `gg` `G` |
| Insert | `i` `a` `o` |
| Delete | `x` `dd` `dw` |
| Copy | `yy` `yw` |
| Paste | `p` `P` |
| Undo | `u` `Ctrl+r` |
| Search | `/` `?` `n` |
| Save | `:w` `:wq` `:q` |