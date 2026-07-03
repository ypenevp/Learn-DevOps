# Git Commands Reference

> [!IMPORTANT]
> Commands are grouped by purpose rather than alphabetically.
> This makes the document easier to use while working with Git.

---

# 1. Identity & Configuration

These commands configure Git and identify the author of future commits.

| Command | Description |
|----------|-------------|
| `git --version` | Display the installed Git version. |
| `git --help` | Display Git help. |
| `git config --global user.name "John Doe"` | Set the global author name. |
| `git config --global user.email "john@example.com"` | Set the global author email. |
| `git config --global init.defaultBranch main` | Change the default branch name for new repositories. |
| `git config --global core.editor "code --wait"` | Configure the default editor. |
| `git config --global credential.helper manager` | Enable Git Credential Manager. |
| `git config --global color.ui auto` | Enable colored output. |
| `git config --global --list` | Display all global configuration values. |
| `git config --local --list` | Display repository-specific configuration. |

> [!TIP]
> Use `--local` whenever you want settings to apply only to the current repository.

---

# 2. Repository Management

Commands used to create, clone, and manage local repositories.

| Command | Description |
|----------|-------------|
| `git init` | Create a new local Git repository. |
| `git clone <repository-url>` | Clone an existing remote repository. |
| `git clone --depth 1 <repository-url>` | Create a shallow clone containing only the latest commit history. |
| `git clone --branch <branch-name> <repository-url>` | Clone and immediately check out a specific branch. |
| `git status` | Display the current repository status. |
| `git remote -v` | Display all configured remote repositories. |

> [!NOTE]
> `git clone` creates a complete local copy of a remote repository, including its commit history, branches, and tags.

---

## Fork Workflow (GitHub)

A **Fork** is a GitHub feature that creates your own copy of another user's repository under your GitHub account.

> [!NOTE]
> Forks are commonly used when contributing to open-source projects where you do not have write access to the original repository.

> [!IMPORTANT]
> Forking is **not a Git command**. It is performed through the GitHub web interface or the GitHub CLI.

### Using the GitHub Web Interface

1. Open the repository.
2. Click **Fork**.
3. Select your GitHub account.
4. GitHub creates a copy under your account.

### Using GitHub CLI

| Command | Description |
|----------|-------------|
| `gh repo fork <owner/repository>` | Fork a repository into your GitHub account. |
| `gh repo fork <owner/repository> --clone` | Fork the repository and clone it locally. |
| `gh repo fork <owner/repository> --remote` | Add the original repository as the `upstream` remote. |

> [!IMPORTANT]
> `<owner>/<repository>` is the GitHub repository identifier, **not** the repository URL.

> [!TIP]
> The `--remote` option automatically adds the original repository as a remote named `upstream`. This allows you to easily fetch and synchronize changes from the original project while working on your fork.



---

# 3. Working Directory

Commands for manipulating working tree files.

| Command | Description |
|----------|-------------|
| `git restore <file>` | Restore a modified file. |
| `git restore .` | Restore every modified file. |
| `git clean -n` | Preview files that would be removed. |
| `git clean -fd` | Delete untracked files and folders. |
| `git mv <old> <new>` | Rename or move a file. |
| `git reset HEAD~1` | Moves your branch one commit back, making the previous commit the latest one while keeping or changing your current file state depending on the reset mode. |

> [!IMPORTANT]
> In `HEAD~1`, the number 1 **defines how many commits Git moves backwards from the current commit (HEAD)**. For example, `HEAD~1` means one commit back, `HEAD~2` means two commits back, and so on. The number is simply the distance in the commit history.

> [!NOTE]
> `git reset HEAD~1` is used to go one commit back in history. If your commits are A → B → C, after running this command, commit C is removed from the branch and B becomes the latest commit. The exact effect on your files depends on the reset mode: by default it unstages changes, but the working directory is not automatically restored unless you use `--hard`.
---

# 4. Staging Area

Commands for preparing the next commit.

| Command | Description |
|----------|-------------|
| `git add <file>` | Stage a specific file. |
| `git add .` | Stage all changes in the current directory and its subdirectories. |
| `git add -A` / `git add --all` | Stage all tracked and untracked changes in the repository. |
| `git add -p` | Interactively stage selected changes (hunks). |
| `git restore --staged <file>` | Unstage a specific file while keeping its changes in the working directory. |
| `git reset` | Unstage all staged changes while keeping the modifications in the working directory. |

> [!IMPORTANT]
> `git reset` (without additional options) **does not delete your work**. It only removes files from the Staging Area, leaving all modifications intact in your working directory.


---

# 5. Commits

Commands related to snapshots.

| Command | Description |
|----------|-------------|
| `git commit -m "message"` | Create a commit. |
| `git commit --amend` | Modify the last commit. |
| `git commit --amend --no-edit` | Amend without changing the message. |

> [!IMPORTANT]
> Every commit represents a snapshot of the project.

---

# 6. Deleting Files

Commands for removing files and directories from Git and the working directory.

> [!NOTE]
> `git rm <file>` is essentially a shortcut for:
>
> 1. Deleting the file from the working directory.
> 2. Running `git add` to stage the deletion.
>
> Instead of deleting a file manually and then staging the deletion, `git rm` performs both actions in a single command.


| Command | Description |
|----------|-------------|
| `git rm <file>` | Delete a tracked file from the working directory and stage the deletion for the next commit. |
| `git rm -f <file>` | **Force delete** a tracked file, even if it has **uncommitted local changes**, and stage the deletion. |
| `git rm --cached <file>` | Remove a file from Git tracking while keeping the file in your working directory. The removal is staged for the next commit. |
| `git rm -r <directory>` | Recursively delete a directory and all of its contents, then stage the deletion. |
| `git reset` | Unstage a deletion (or any staged change) while **leaving the working directory unchanged**. Deleted files remain deleted. |
| `git reset --hard` | Restore the working directory and Staging Area to the last commit, recovering deleted tracked files and discarding all uncommitted changes. |


> [!NOTE]
> If you delete a file and stage the deletion, `git reset` will **unstage** the change but the **file will still remain deleted** in your working directory. `git reset --hard` **removes the change** from staging and also restores the file back to the state of the last commit, meaning the **deleted file will reappear**.

> [!IMPORTANT]
> `git rm --cached <file>` is used with `.gitignore` when a file was accidentally committed but should stay only on your computer (e.g. `.env`). First you remove it from Git tracking with `git rm --cached`, then you add it to `.gitignore` so Git ignores it in the future. This keeps the file locally but removes it from the repository and prevents it from being committed again.


> [!NOTE]
> `git rm -r <directory>` uses the **recursive** (`-r`) option, meaning Git deletes the specified directory **and everything inside it**, including all files and subdirectories.

---

# 7. Branch Management

| Command | Description |
|----------|-------------|
| `git branch` | List local branches. |
| `git branch -a` | List all branches. |
| `git branch <branch>` | Create a branch. |
| `git branch -d <branch>` | Delete a merged branch. |
| `git branch -D <branch>` | Force delete a branch. |
| `git switch <branch>` | Switch branches. |
| `git switch -c <branch>` | Create and switch. |
| `git checkout <commit>` | Checkout a specific commit. |
| `git checkout -b <branch>` | Create and switch (legacy). |

---

# 8. History & Inspection

> [!IMPORTANT]
> Use 'q' to exit page menu.

| Command | Description |
|----------|-------------|
| `git log` | Show commit history. |
| `git log --oneline` | Compact history. |
| `git log --graph --all --decorate` | Visual history graph. |
| `git show` | Display a commit. |
| `git diff` | Compare working directory to staging area. |
| `git diff --staged` | Compare staging area to HEAD. |
| `git blame <file>` | Show line authorship. |

---

# 9. Remote Repositories

| Command | Description |
|----------|-------------|
| `git remote -v` | Show remotes. |
| `git remote add origin <url>` | Add a remote. |
| `git remote remove origin` | Remove a remote. |
| `git remote rename origin github` | Rename a remote. |
| `git remote show origin` | Show remote information. |

---

# 10. Synchronization

| Command | Description |
|----------|-------------|
| `git fetch` | Download remote changes. |
| `git fetch origin` | Fetch from origin. |
| `git pull` | Fetch and merge. |
| `git pull --rebase` | Fetch and rebase. |
| `git push` | Push current branch. |
| `git push origin main` | Push main branch. |
| `git push --tags` | Push tags. |

---

# 11. Merge

| Command | Description |
|----------|-------------|
| `git merge <branch>` | Merge another branch. |
| `git merge --no-ff <branch>` | Force a merge commit. |
| `git merge --abort` | Abort a merge. |

---

# 12. Rebase

| Command | Description |
|----------|-------------|
| `git rebase main` | Rebase current branch onto main. |
| `git rebase --continue` | Continue rebase. |
| `git rebase --abort` | Abort rebase. |

---

# 13. Stash

| Command | Description |
|----------|-------------|
| `git stash` | Save uncommitted work. |
| `git stash list` | List stashes. |
| `git stash show` | Inspect a stash. |
| `git stash apply` | Apply a stash. |
| `git stash pop` | Apply and remove a stash. |
| `git stash drop` | Delete one stash. |
| `git stash clear` | Delete all stashes. |

---

# 14. Tags

| Command | Description |
|----------|-------------|
| `git tag` | List tags. |
| `git tag v1.0.0` | Create a lightweight tag. |
| `git tag -a v1.0.0 -m "Release"` | Create an annotated tag. |
| `git push origin v1.0.0` | Push one tag. |
| `git push --tags` | Push all tags. |

---

# 15. Undo & Recovery

| Command | Description |
|----------|-------------|
| `git reset --soft HEAD~1` | Undo commit, keep staged changes. |
| `git reset --mixed HEAD~1` | Undo commit, keep files. |
| `git reset --hard HEAD~1` | Completely discard changes. |
| `git restore <file>` | Restore a file. |
| `git restore --staged <file>` | Unstage a file. |

---

# 16. Revert

| Command | Description |
|----------|-------------|
| `git revert <commit>` | Create a commit that reverses another commit. |

---

# 17. Cherry-pick

| Command | Description |
|----------|-------------|
| `git cherry-pick <commit>` | Apply one commit to the current branch. |

---

# 18. GitHub CLI

| Command | Description |
|----------|-------------|
| `gh auth login` | Authenticate GitHub CLI. |
| `gh repo clone owner/repo` | Clone a repository. |
| `gh repo create` | Create a new repository. |
| `gh issue list` | List issues. |
| `gh issue create` | Create an issue. |
| `gh pr list` | List pull requests. |
| `gh pr create` | Create a pull request. |
| `gh pr checkout <number>` | Checkout a PR locally. |
| `gh pr merge <number>` | Merge a PR. |