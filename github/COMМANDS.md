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

Commands used to create or clone repositories.

| Command | Description |
|----------|-------------|
| `git init` | Create a new local repository. |
| `git clone <repository-url>` | Clone an existing remote repository. |
| `git clone --depth 1 <repository-url>` | Create a shallow clone. |
| `git status` | Display repository status. |

---

# 3. Working Directory

Commands for manipulating working tree files.

| Command | Description |
|----------|-------------|
| `git restore <file>` | Restore a modified file. |
| `git restore .` | Restore every modified file. |
| `git clean -n` | Preview files that would be removed. |
| `git clean -fd` | Delete untracked files and folders. |
| `git rm <file>` | Remove a tracked file. |
| `git mv <old> <new>` | Rename or move a file. |

---

# 4. Staging Area

Commands for preparing the next commit.

| Command | Description |
|----------|-------------|
| `git add <file>` | Stage a single file. |
| `git add .` | Stage everything. |
| `git add -A` | Stage all tracked and untracked changes. |
| `git add -p` | Stage changes interactively. |
| `git restore --staged <file>` | Remove a file from the staging area. |

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

# 6. Branch Management

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

# 7. History & Inspection

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

# 8. Remote Repositories

| Command | Description |
|----------|-------------|
| `git remote -v` | Show remotes. |
| `git remote add origin <url>` | Add a remote. |
| `git remote remove origin` | Remove a remote. |
| `git remote rename origin github` | Rename a remote. |
| `git remote show origin` | Show remote information. |

---

# 9. Synchronization

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

# 10. Merge

| Command | Description |
|----------|-------------|
| `git merge <branch>` | Merge another branch. |
| `git merge --no-ff <branch>` | Force a merge commit. |
| `git merge --abort` | Abort a merge. |

---

# 11. Rebase

| Command | Description |
|----------|-------------|
| `git rebase main` | Rebase current branch onto main. |
| `git rebase --continue` | Continue rebase. |
| `git rebase --abort` | Abort rebase. |

---

# 12. Stash

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

# 13. Tags

| Command | Description |
|----------|-------------|
| `git tag` | List tags. |
| `git tag v1.0.0` | Create a lightweight tag. |
| `git tag -a v1.0.0 -m "Release"` | Create an annotated tag. |
| `git push origin v1.0.0` | Push one tag. |
| `git push --tags` | Push all tags. |

---

# 14. Undo & Recovery

| Command | Description |
|----------|-------------|
| `git reset --soft HEAD~1` | Undo commit, keep staged changes. |
| `git reset --mixed HEAD~1` | Undo commit, keep files. |
| `git reset --hard HEAD~1` | Completely discard changes. |
| `git restore <file>` | Restore a file. |
| `git restore --staged <file>` | Unstage a file. |

---

# 15. Revert

| Command | Description |
|----------|-------------|
| `git revert <commit>` | Create a commit that reverses another commit. |

---

# 16. Cherry-pick

| Command | Description |
|----------|-------------|
| `git cherry-pick <commit>` | Apply one commit to the current branch. |

---

# 17. GitHub CLI

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