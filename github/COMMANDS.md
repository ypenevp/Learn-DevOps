# Git Commands Reference

> [!IMPORTANT]
> Commands are grouped by purpose rather than alphabetically.
> This makes the document easier to use while working with Git.

# Cheat Sheet: Core Git & GitHub Commands

| Command | Description |
|----------|-------------|
| `git init` | Initialize a new Git repository locally. |
| `git clone <repository-url>` | Download a remote repository to your local machine. |
| `gh repo fork <owner/repository>` | Create a fork of a GitHub repository under your account. |
| `git status` | Show the current state of the working directory and staging area. |
| `git log --oneline` | Show commit history in a compact single-line format. |
| `git add -A` / `git add --all` | Stage all changes (new, modified, deleted files). |
| `git commit -m "message"` | Create a commit with a message describing the changes. |
| `git push` | Upload local commits to a remote repository (e.g., GitHub). |
| `git pull` | Fetch and merge changes from a remote repository. |
| `git branch` | List, create, or manage branches. |
| `git switch <branch>` | Switch to another branch. |
| `git merge <branch> -m "Merge message"` | Merge another branch into the current branch with a merge commit message. |
| `git reset` | Unstage changes while keeping them in the working directory. |
| `git reset HEAD~1` | Move branch one commit back (undo last commit locally). |
| `git stash` | Temporarily save uncommitted changes. |
| `git stash list` | Show all saved stashes. |
| `git stash pop` | Restore the latest stash and remove it from stash list. |
| `git rm --cached <file>` | Remove a file from Git tracking while keeping it locally. |

---

# Comprehensive Git & GitHub commands reference

# 1. Configuration

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

# 2. Logs & Inspection

> [!IMPORTANT]
> Use 'q' to exit page menu.

| Command | Description |
|----------|-------------|
| `git log` | Show commit history. |
| `git log --oneline` | Compact history + commits githash. |
| `git log --graph --all --decorate` | Visual history graph. |
| `git show` / `git show <githash>`| Display a details of the commit. |
| `git diff` | Compare working directory to staging area. |
| `git diff --staged` | Compare staging area to HEAD. |
| `git blame <file>` | Show line authorship. |

---

# 3. Repository Management

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

# 6. Synchronization with Remote

Commands for synchronizing the local repository with a remote repository.

| Command | Description |
|----------|-------------|
| `git push` | Push the current branch to its remote counterpart. |
| `git push origin <branch>` | Push the specified local branch to the remote repository. |
| `git push origin main` | Push the local `main` branch to the remote `main` branch. |
| `git push --tags` | Push all local tags to the remote repository. |
| `git fetch` | Download changes from all configured remote repositories without modifying the working directory. |
| `git fetch origin` | Download changes from the `origin` remote only. |
| `git fetch origin <branch>` | Download updates for a specific branch from `origin`. |
| `git pull` | Fetch and automatically merge changes into the current branch. |
| `git pull origin <branch>` | Fetch and merge a specific remote branch into the current branch. |
| `git pull --rebase` | Fetch changes and rebase the current branch instead of creating a merge commit. |

> [!IMPORTANT]
> `git fetch` downloads **remote commits** into your local repository **without modifying your working directory**.

> [!IMPORTANT]
> `git pull` downloads **and immediately integrates** remote changes into your current branch.

> [!TIP]
> `git pull` is equivalent to:
> **`git fetch` + `git merge`**

> [!NOTE]
> Before pushing a feature branch for the first time, use:
>
> ```bash
> git push -u origin <branch>
> ```
>
> The `-u` (`--set-upstream`) option links the local branch with the remote branch, allowing future pushes and pulls to be performed simply with `git push` and `git pull`.

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

# 8. Merge

| Command | Description |
|----------|-------------|
| `git merge <branch>` | Merge the specified branch into the **current branch**. |
| `git merge <branch> -m "Merge message"` | Merge a branch using a custom merge commit message. |
| `git merge --no-ff <branch>` | Force Git to create a merge commit. |
| `git merge --abort` | Abort an in-progress merge. |

> [!NOTE]
> If type `git merge main`, while you are in another branch. Only 
> the current branch(not main) will be updated with latest changes.
> In main the latest updates from the other branch will not be 
> visible. 
 
---

# 9. Working Directory


| Command | Description |
|----------|-------------|
| `git restore <file>` | Restore a modified file. |
| `git restore .` | Restore every modified file. |
| `git reset HEAD~1` | Moves your branch one commit back, making the previous commit the latest one while keeping or changing your current file state depending on the reset mode. |

> [!IMPORTANT]
> In `HEAD~1`, the number 1 **defines how many commits Git moves backwards from the current commit (HEAD)**. For example, `HEAD~1` means one commit back, `HEAD~2` means two commits back, and so on. The number is simply the distance in the commit history.

> [!NOTE]
> `git reset HEAD~1` is used to go one commit back in history. If your commits are A → B → C, after running this command, commit C is removed from the branch and B becomes the latest commit. The exact effect on your files depends on the reset mode: by default it unstages changes, but the working directory is not automatically restored unless you use `--hard`.

---

# 10. Stash

Commands for temporarily saving uncommitted changes without creating a commit.

| Command | Description |
|----------|-------------|
| `git stash` | Save all uncommitted changes and restore a clean working directory. |
| `git stash list` | Display all saved stashes. |
| `git stash show` | Show a summary of the latest stash. |
| `git stash show stash@{n}` | Show a summary of a specific stash. |
| `git stash apply` | Restore the latest stash while keeping it in the stash list. |
| `git stash pop` | Restore the latest stash and remove it from the stash list. |
| `git stash drop` | Delete the latest stash (`stash@{0}`). |
| `git stash clear` | Delete all stashes. |

> [!TIP]
> `git stash` is useful when you're **not ready to commit your work** but need to temporarily switch branches, pull new changes, or work on something else. It safely stores your unfinished changes so you can restore them later.

> [!IMPORTANT]
> **`git stash pop`** restores your changes **and removes the stash** from the stash list. **`git stash apply`** restores your changes **but keeps the stash**, allowing you to reuse it later if needed.

> [!NOTE]
> Git can store **multiple stashes**. Use `git stash list` to view them. Each stash has an identifier such as `stash@{0}`, `stash@{1}`, etc. To use a specific stash with commands like **`show`**, **`apply`**, **`pop`**, or **`drop`**, simply append its identifier (for example, `stash@{1}`). If no identifier is specified, Git uses the **latest stash (`stash@{0}`)** by default.

---

# 11. Deleting Files

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

# 12. Undo & Recovery

Commands for undoing local changes, unstaging files, and recovering previous repository states.

| Command | Description |
|----------|-------------|
| `git restore <file>` | Restore a file to its state from the latest commit. |
| `git restore <directory>` | Restore all files within the specified directory. |
| `git restore .` | Restore all modified files in the working directory. |
| `git restore --staged <file>` | Unstage a specific file while keeping its changes in the working directory. |
| `git restore --staged .` | Unstage all staged files while preserving their changes. |
| `git reset` | Unstage all staged changes while keeping modifications in the working directory. |
| `git reset --soft HEAD~1` | Undo the last commit while keeping all changes staged. |
| `git reset --mixed HEAD~1` | Undo the last commit and unstage its changes (default behavior). |
| `git reset --hard HEAD~1` | Undo the last commit and permanently discard all associated changes. |

> [!IMPORTANT]
> `git restore` is designed to undo **local, uncommitted changes** by restoring files to their state from the latest commit.

> [!NOTE]
> `git restore --staged` removes files from the **Staging Area** only. The file contents remain unchanged in the working directory.


> [!WARNING]
> `git restore` permanently discards uncommitted changes. Once restored, those changes cannot be recovered through Git.

> [!WARNING]
> `git reset --hard HEAD~1` permanently removes the last commit **and** deletes all associated changes from your working directory.


### Example: Undo the Last Commit

```bash
git reset --mixed HEAD~1
```

Removes the most recent commit while keeping all changes locally as unstaged modifications.

---

# 13. Revert

This commands are only for good practice.

> [!TIP]
> `git revert` is commonly used when a **commit has already been pushed or shared with others**. Instead of deleting the commit, Git creates a new commit that safely undoes its changes while preserving the project history.

| Command | Description |
|----------|-------------|
| `git revert <commit>` | Create a new commit that reverses the changes introduced by the specified commit. |
| `git revert HEAD` | Revert the latest commit by creating a new commit. |

> [!IMPORTANT]
> Unlike **`git reset`**, **`git revert` does not remove commits from history**. It creates a **new commit** that reverses the changes made by the selected commit, keeping the commit history complete and traceable.

> [!NOTE]
> To revert a commit, you need its **commit hash (ID)**. You can find it using commands such as `git log` or `git log --oneline`.

---

# 14. GitHub CLI

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

---



# Less likely to use

## 15. Rebase

Commands for rewriting commit history to create a clean, linear project history.

> [!TIP]
> `git rebase` is used when you want to **integrate changes from another branch while keeping history clean and linear**. Instead of creating a merge commit, Git re-applies your commits on top of the latest version of the target branch.

| Command | Description |
|----------|-------------|
| `git rebase main` | Move current branch commits on top of the latest `main` branch, creating a linear history. |
| `git rebase <branch>` | Rebase current branch onto another branch. |
| `git rebase --continue` | Continue the rebase after resolving conflicts. |
| `git rebase --abort` | Cancel the rebase and return to the original state before it started. |


> [!IMPORTANT]
> Unlike `merge`, **`git rebase rewrites commit history`**. It moves your commits to a new base, which also changes their commit IDs (hashes). This creates a cleaner history but means the commits are technically new versions of the originals.

> [!WARNING]
> `git rebase` should **not be used on shared/public branches**, because rewriting history can cause conflicts for other developers. If someone has already pulled the original commits, their history will no longer match after a rebase.

---

## 16. Tags

| Command | Description |
|----------|-------------|
| `git tag` | List tags. |
| `git tag v1.0.0` | Create a lightweight tag. |
| `git tag -a v1.0.0 -m "Release"` | Create an annotated tag. |
| `git push origin v1.0.0` | Push one tag. |
| `git push --tags` | Push all tags. |

---

## 17. Remote Repositories

| Command | Description |
|----------|-------------|
| `git remote -v` | Show remotes. |
| `git remote add origin <url>` | Add a remote. |
| `git remote remove origin` | Remove a remote. |
| `git remote rename origin github` | Rename a remote. |
| `git remote show origin` | Show remote information. |

---

## 18. Cherry-pick

| Command | Description |
|----------|-------------|
| `git cherry-pick <commit>` | Apply one commit to the current branch. |



