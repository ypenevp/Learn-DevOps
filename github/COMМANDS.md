# Git and GitHub CLI Technical Reference

This document provides a comprehensive overview of essential Git commands and GitHub CLI operations for version control, project management, and collaborative workflows.

---

## 1. Identity and Global Configuration
Before initiating version control, the environment must be configured with author identity to ensure traceability in the project history.

| Command | Parameter Example | Description |
| :--- | :--- | :--- |
| `git config --global user.name` | `"First Last"` | Sets the author name for all commits on the machine. |
| `git config --global user.email` | `"me@example.com"` | Sets the author email address for project history. |
| `git config --global --list` | (none) | Displays the current global Git configuration settings. |
| `git --version` | (none) | Verifies the installed version of Git. |
| `git --help` | (none) | Opens the official Git help documentation. |

> [!NOTE]
> Use the `--local` flag instead of `--global` on an existing project to apply identity settings exclusively to that repository.

---

## 2. Local Repository Lifecycle
The Git workflow manages transitions between the Working Directory, Staging Area (Index), and the Repository.

| Command | Parameter Example | Description |
| :--- | :--- | :--- |
| `git init` | (none) | Initializes a new local Git repository in the current directory. |
| `git status` | (none) | Shows the state of the working directory and staging area. |
| `git add` | `<file_path>` or `.` | Stages specific files or all changes for the next commit. |
| `git commit -m` | `"Commit message"` | Records staged changes to the repository history. |
| `chmod +x` | `<script_path>` | Makes a script file executable (e.g., for dev containers). |

---

## 3. Branch Management and Navigation
Branches are lightweight pointers used for parallel development and isolation of features.

| Command | Parameter Example | Description |
| :--- | :--- | :--- |
| `git branch` | `<branch_name>` | Creates a new branch from the current commit. |
| `git branch --list` | (none) | Displays a list of all existing local branches. |
| `git branch --delete` | `<branch_name>` | Removes the pointer to a branch after it has been merged. |
| `git checkout` | `<branch_name>` | Switches the working directory to the specified branch. |
| `git checkout -b` | `<new_branch_name>` | Creates a new branch and switches to it immediately. |
| `git switch` | `<branch_name>` | A simplified command dedicated to switching branches. |

---

## 4. Inspection and History Analysis
Git maintains a complete history of project changes, including author info and timestamps.

| Command | Parameter Example | Description |
| :--- | :--- | :--- |
| `git log` | `--oneline --graph` | Displays the commit history in a condensed, visual format. |
| `git checkout` | `<commit_id>` | Temporarily reverts the working directory to a specific past version. |
| `git diff` | `<file_path>` | Shows differences between the working directory and the staging area. |
| `git diff --staged` | (none) | Shows differences between the staging area and the last commit [20, 21]. |
| `git diff HEAD~1` | (none) | Compares the current state with the previous commit. |

---

## 5. Merging and Synchronization
Merging integrates changes from different branches into a target branch.

| Command | Parameter Example | Description |
| :--- | :--- | :--- |
| `git merge` | `<branch_name>` | Integrates changes from the specified branch into the current branch. |
| `git merge --no-ff` | `<branch_name> -m "msg"` | Forces a merge commit to preserve the visibility of the branch history. |
| `git push` | `origin <branch_name>` | Uploads local branch commits to the remote repository on GitHub. |
| `git pull` | (none) | Fetches and integrates changes from the remote repository. |

---

## 6. GitHub CLI (`gh`) Operations
The GitHub CLI streamlines interactions with the remote platform directly from the terminal.

| Command | Parameter Example | Description |
| :--- | :--- | :--- |
| `gh auth login` | (none) | Authenticates the CLI with your GitHub account. |
| `gh repo clone` | `<owner/repo>` | Clones a remote GitHub repository to your local machine. |
| `gh pr create` | `--title "Title"` | Initiates a new Pull Request for review and collaboration. |
| `gh pr list` | (none) | Lists all active Pull Requests in the current repository. |
| `gh pr checkout` | `<pr_number>` | Checks out the branch of a specific Pull Request locally. |
| `gh pr merge` | `<pr_number> --merge` | Finalizes and merges a Pull Request via the command line. |

---

## 7. Standards for Collaboration and Security
Standard files required for professional repository maintenance to ensure healthy and safe growth.

1.  **.gitignore:** Defines files and directories Git should not track (e.g., secrets, temp files).
2.  **CONTRIBUTING.md:** Outlines the process for external contributions and setup.
3.  **CODEOWNERS:** Automates reviewer assignment based on specific file paths.
4.  **CODE_OF_CONDUCT.md:** Establishes standards for professional and respectful behavior.
5.  **SECURITY.md:** Provides instructions for responsible vulnerability reporting.