# Git Documentation: A Comprehensive Guide

## Table of Contents

1. [Introduction](#1-introduction)
2. [Getting Started with Git](#2-getting-started-with-git)
   - 2.1 [Initializing a New Repository](#21-initializing-a-new-repository)
   - 2.2 [Cloning an Existing Repository](#22-cloning-an-existing-repository)
3. [Basic Git Commands](#3-basic-git-commands)
   - 3.1 [Checking Repository Status](#31-checking-repository-status)
   - 3.2 [Branch Management](#32-branch-management)
   - 3.3 [Staging and Committing Changes](#33-staging-and-committing-changes)
   - 3.4 [Working with Remotes](#34-working-with-remotes)
4. [Git Configuration](#4-git-configuration)
   - 4.1 [Viewing Git Configuration](#41-viewing-git-configuration)
   - 4.2 [Changing User Information](#42-changing-user-information)
   - 4.3 [Handling Line Endings](#43-handling-line-endings)
5. [Understanding Git History](#5-understanding-git-history)
   - 5.1 [Viewing Commit History](#51-viewing-commit-history)
   - 5.2 [Amending Commit Messages](#52-amending-commit-messages)
   - 5.3 [Reverting Amended Commits](#53-reverting-amended-commits)
6. [Managing Remote Repositories](#6-managing-remote-repositories)
   - 6.1 [Changing Remote URLs](#61-changing-remote-urls)
   - 6.2 [Restoring Deleted Repositories](#62-restoring-deleted-repositories)
   - 6.3 [Force Pushing Changes](#63-force-pushing-changes)
7. [Managing Files with .gitignore](#7-managing-files-with-gitignore)
   - 7.1 [What is .gitignore?](#71-what-is-gitignore)
   - 7.2 [Setting Up .gitignore](#72-setting-up-gitignore)
   - 7.3 [Untracking Already Added Files](#73-untracking-already-added-files)
   - 7.4 [Handling Tracked Files with .gitignore](#74-handling-tracked-files-with-gitignore)
   - 7.5 [Common .gitignore Mistakes and Fixes](#75-common-gitignore-mistakes-and-fixes)
   - 7.6 [Best Practices for .gitignore](#76-best-practices-for-gitignore)
8. [Staging Area Management](#8-staging-area-management)
   - 8.1 [Removing Files from Staging](#81-removing-files-from-staging)
   - 8.2 [Staging Files from Parent Directories](#82-staging-files-from-parent-directories)
   - 8.3 [Removing Specific Files from Staging](#83-removing-specific-files-from-staging)
9. [Git History Manipulation](#9-git-history-manipulation)
   - 9.1 [Resetting to Previous Commits](#91-resetting-to-previous-commits)
   - 9.2 [Interactive Rebase](#92-interactive-rebase)
   - 9.3 [Removing Commits from History](#93-removing-commits-from-history)
   - 9.4 [Reverting Changes](#94-reverting-changes)
10. [Git Tagging](#10-git-tagging)
    - 10.1 [What are Git Tags?](#101-what-are-git-tags)
    - 10.2 [Creating Tags](#102-creating-tags)
    - 10.3 [Managing Tags](#103-managing-tags)
11. [Troubleshooting Common Git Issues](#11-troubleshooting-common-git-issues)
    - 11.1 [Updates Rejected Due to Remote Changes](#111-updates-rejected-due-to-remote-changes)
    - 11.2 [Handling Diverged Branches During Pull](#112-handling-diverged-branches-during-pull)
    - 11.3 [GitHub File Not Showing](#113-github-file-not-showing)
    - 11.4 [Resolving SSH Key Errors](#114-resolving-ssh-key-errors)
    - 11.5 [Resolving .DS_Store Issues](#115-resolving-ds_store-issues)
    - 11.6 [Resolving .idea/ and Build Directory Issues](#116-resolving-idea-and-build-directory-issues)
    - 11.7 [Staged File Removal Issues](#117-staged-file-removal-issues)
    - 11.8 [Undoing Git Operations](#118-undoing-git-operations)
12. [Advanced Topics](#12-advanced-topics)
    - 12.1 [Cleaning Git History (Removing Sensitive Data)](#121-cleaning-git-history-removing-sensitive-data)
    - 12.2 [SSH Key Setup for GitHub](#122-ssh-key-setup-for-github)
13. [Summary of Key Git Commands](#13-summary-of-key-git-commands)

---

## 1. Introduction

This document serves as a comprehensive guide to Git, a powerful distributed version control system. It covers fundamental Git commands, configuration, history management, and advanced topics such as handling sensitive data and troubleshooting common issues. This guide is designed for developers of all experience levels, providing clear explanations and practical examples to enhance your understanding and proficiency with Git.

---

## 2. Getting Started with Git

To begin working with Git, you can either initialize a new repository for a new project or clone an existing repository from a remote source.

### 2.1 Initializing a New Repository

When starting a new project that you wish to track with Git, you will typically initialize a new Git repository in your project directory. This command creates a new `.git` subdirectory, which contains all the necessary Git metadata for the repository.

```bash
git init
```

After initialization, you might want to create a `README.md` file to describe your project and add it to your repository.

```bash
echo "# Your_Project_Name" >> README.md
git add README.md
git commit -m "first commit"
```

To connect your local repository to a remote repository (e.g., on GitHub), you need to add a remote origin. Replace `your-remote-repository-url` with the actual URL of your remote repository.

```bash
git remote add origin your-remote-repository-url
```

Finally, push your initial commit to the remote repository. The `-u` flag sets the upstream branch, so you can simply use `git push` in the future.

```bash
git push -u origin main
```

### 2.2 Cloning an Existing Repository

If you are joining an existing project or want to work on a project hosted remotely, you can clone the repository. Cloning downloads a complete copy of the repository, including all files, branches, and commit history, to your local machine.

There are two primary methods for cloning: HTTPS and SSH.

**Cloning with HTTPS:**

This method is generally simpler for read-only access and does not require SSH key setup. However, you will need to provide your username and password (or a personal access token) for write operations.

```bash
git clone https://github.com/your-username/your-repo.git
```

**Cloning with SSH:**

SSH provides a more secure way to interact with remote repositories, especially for frequent write operations, as it uses SSH keys for authentication. This requires prior setup of SSH keys on your system and adding them to your Git hosting service (e.g., GitHub).

```bash
git clone git@github.com:your-username/your-repo.git
```

After cloning, you can verify the remote origin to ensure it's correctly set up:

```bash
git remote -v
```

**Cloning a Specific Branch:**

Sometimes, you might want to clone a specific branch of a repository directly, rather than the default branch (usually `main` or `master`). This is particularly useful for projects that maintain different branches for active development and stable releases.

To clone a specific branch (e.g., `stable`):

```bash
git clone -b stable https://github.com/your-username/your-repo.git
```

The `-b` (or `--branch`) flag tells Git which branch to check out immediately after cloning. This avoids the need to manually switch branches after the initial clone.

---

## 3. Basic Git Commands

Understanding and utilizing basic Git commands is crucial for effective version control. These commands allow you to manage your project's history, collaborate with others, and maintain a clean and organized codebase.

### 3.1 Checking Repository Status

The `git status` command provides a summary of the current state of your working directory and the staging area. It shows which changes have been staged, which haven't, and which files aren't being tracked by Git.

```bash
git status
```

### 3.2 Branch Management

Branches are fundamental to Git, allowing you to work on different features or bug fixes in isolation from the main codebase. This section covers essential commands for managing branches.

To list all local branches:

```bash
git branch
```

To list all remote branches:

```bash
git branch -r
```

To list all local and remote branches:

```bash
git branch -a
```

To switch to the last branch you were on:

```bash
git checkout -
```

To switch to a specific existing branch:

```bash
git checkout your-branch-name
```

To create a new branch and immediately switch to it:

```bash
git checkout -b new-branch-name
```

If a branch exists on the remote but not locally, you can create and switch to it based on the remote branch:

```bash
git checkout -b your-branch-name origin/your-branch-name
```

To find the currently active Git branch:

```bash
git branch --show-current
# Alternatively:
git rev-parse --abbrev-ref HEAD
```

### 3.3 Staging and Committing Changes

After making changes to your files, you need to stage them and then commit them to your repository's history.

To stage all changes in the current directory (including new files, modifications, and deletions):

```bash
git add .
```

To stage specific files:

```bash
git add file1.js file2.py
```

To commit staged changes with a descriptive message:

```bash
git commit -m "Your descriptive commit message"
```

To stage all modified files and commit in one command (does not include new untracked files):

```bash
git commit -am "Your commit message"
```

### 3.4 Working with Remotes

Remote repositories are versions of your project that are hosted on the internet or network. They are essential for collaboration and backing up your work.

To verify the remote repositories configured for your project:

```bash
git remote -v
```

To fetch the latest changes from the remote repository and then switch to a specific branch (useful for updating your local branch with remote changes):

```bash
git fetch && git checkout your-branch-name
```

To push your local commits to the remote repository. The `-u` flag sets the upstream branch, which is useful for subsequent pushes.

```bash
git push -u origin main
# Or for a new remote and branch:
git push new_remote_name branch_name
```

For pushing to a specific GitHub repository using a Personal Access Token (PAT) for authentication (replace placeholders):

```bash
git push https://YOUR_GITHUB_USERNAME:YOUR_PERSONAL_ACCESS_TOKEN@github.com/your-username/your-repo.git
```

To pull changes from a specific remote and branch:

```bash
git pull origin main
```

To fetch all branches and their respective commits from the remote repository:

```bash
git fetch origin
```

---

## 4. Git Configuration

Git allows extensive configuration to tailor its behavior to your preferences and project needs. These configurations can be set at different levels: system, global (user), and local (repository).

### 4.1 Viewing Git Configuration

To view your Git configuration settings, you can use the `git config` command with various flags.

To display all Git configuration settings for your user account on the current system:

```bash
git config --list
```

To show only global settings (those applied to all your repositories):

```bash
git config --global --list
```

To show only local repository settings (those specific to the current repository):

```bash
git config --local --list
```

### 4.2 Changing User Information

It is essential to configure your Git username and email address, as this information is embedded in every commit you make. This helps identify who made which changes.

To change your global Git username:

```bash
git config --global user.name "Your Name"
```

To change your global Git email address:

```bash
git config --global user.email "your-email@example.com"
```

### 4.3 Handling Line Endings

Line ending inconsistencies between different operating systems (Windows uses CRLF, macOS/Linux use LF) can cause issues in collaborative projects. Git provides the `core.autocrlf` setting to manage this automatically.

To configure Git to convert CRLF to LF on commit (for macOS or Linux users), ensuring Unix-style line endings in the repository, but leaving line endings unchanged on checkout:

```bash
git config --global core.autocrlf input
```

To configure Git to convert LF to CRLF on checkout and CRLF to LF on commit (for Windows users):

```bash
git config --global core.autocrlf true
```

To disable automatic conversion and leave line endings unchanged:

```bash
git config --global core.autocrlf false
```

For most macOS and Linux users, setting `core.autocrlf` to `input` is recommended. This helps maintain consistent line endings across different development environments.

---

## 5. Understanding Git History

Git maintains a detailed history of all changes made to your repository, allowing you to track, review, and revert modifications. Understanding how to navigate and interpret this history is crucial for effective version control.

### 5.1 Viewing Commit History

The `git log` command is your primary tool for exploring the commit history. It displays a list of commits in reverse chronological order, showing the commit hash, author, date, and commit message.

To view the full commit history with detailed information:

```bash
git log
```

For a more compact view, displaying each commit on a single line with an abbreviated commit hash and message:

```bash
git log --oneline
```

To limit the display to a specific number of commits (e.g., last 10 commits):

```bash
git log --oneline -10
```

To visualize branches and their commit history graphically:

```bash
git log --graph --oneline --all
```

To see commits along with the patches or changes introduced by each commit:

```bash
git log -p
```

To see commits by a specific author:

```bash
git log --author="Your Author Name"
```

To see commits within a specific date range:

```bash
git log --since="YYYY-MM-DD" --until="YYYY-MM-DD"
```

To list all the files modified or added in a specific commit (replace `commit-hash` with the actual commit hash):

```bash
git diff-tree --no-commit-id --name-only -r commit-hash
```

To view recent Git operations (useful for finding lost commits):

```bash
git reflog
```

### 5.2 Amending Commit Messages

Sometimes you might need to modify the message of your most recent commit. The `git commit --amend` command allows you to do this.

To change the most recent commit message:

```bash
git commit --amend -m "Your new commit message"
```

This command replaces the last commit with a new one that includes the previous commit's contents and any newly staged changes. If you have already staged new changes with `git add .`, they will be included in the amended commit.

**Important Consideration:** If the commit has already been pushed to a remote repository, amending it will create a new commit that diverges from the remote history. You will need to force push to update the remote:

```bash
git push --force-with-lease origin main
```

**If force-with-lease fails due to stale reference:**

```bash
# Fetch latest remote references
git fetch origin

# Then force push
git push --force-with-lease origin main
```

### 5.3 Reverting Amended Commits

If you amend a commit and then decide you want to split it into two separate commits, you can do so by resetting the last commit and then re-committing your changes.

1. **Reset the last commit but keep changes staged:**

```bash
git reset --soft HEAD~1
```

This command moves the `HEAD` pointer back one commit, but keeps the changes from that commit in your staging area.

2. **Make two new commits:**

Now your changes will be staged again. You can selectively commit them.

```bash
git commit -m "First part of the commit message"
```

If some changes still remain staged after the first commit, unstage them:

```bash
git reset
```

Then, selectively add the remaining changes and commit them:

```bash
git add .  # or specific files
git commit -m "Second part of the commit message"
```

This process allows you to refine your commit history by breaking down a single amended commit into more granular, logically separated commits.

---

## 6. Managing Remote Repositories

Remote repositories are essential for collaboration and backup. This section covers how to manage and interact with remote repositories effectively.

### 6.1 Changing Remote URLs

If you need to change the remote URL after cloning, you can use the `set-url` command. This is useful if the repository's remote URL changes or if you initially cloned using HTTPS and now wish to switch to SSH, or vice-versa.

**To update an existing remote URL:**

```bash
git remote set-url origin your-new-remote-repository-url
```

**To completely remove and re-add a remote:**

```bash
# Remove the old remote
git remote remove origin

# Add the new remote
git remote add origin https://github.com/new-username/new-repo.git
```

**Example: Switching from one repository to another:**

If you're working on a forked repository and need to switch to a different one:

```bash
# Update remote URL to point to new repository
git remote set-url origin https://github.com/studiointeriorm/StudioM.git

# Verify the change
git remote -v

# Fetch from new remote
git fetch origin
```

### 6.2 Restoring Deleted Repositories

If a remote repository is accidentally deleted and you have a local copy with all commits intact, you can restore it to a newly created repository.

**Steps to restore:**

1. **Verify your local repository is intact:**

```bash
# Check your commit history is still there
git log --oneline -10

# Check current remote
git remote -v
```

2. **Update the remote URL to point to the new repository:**

```bash
git remote set-url origin https://github.com/your-username/new-repo.git
```

3. **Push everything including all commits:**

```bash
# Push with full history
git push -u origin main --force

# If you have multiple branches
git push --all origin --force
git push --tags origin --force
```

This restores your entire project with complete commit history to the new repository.

### 6.3 Force Pushing Changes

Force pushing overwrites the remote branch with your local version. Use with extreme caution as it can delete other people's work.

**Safer option - force push with lease:**

```bash
git push --force-with-lease origin main
```

This will fail if someone else has pushed to the branch since your last fetch, protecting against accidentally overwriting others' work.

**Regular force push (use only when absolutely necessary):**

```bash
git push --force origin main
```

**Understanding the consequences:**

When you force push, you completely replace the remote branch history with your local history. Any commits that exist on the remote but not locally will be permanently deleted. Always:
- Communicate with your team before force pushing
- Use `--force-with-lease` instead of `--force` when possible
- Consider if there's a safer alternative (like reverting commits)

---

## 7. Managing Files with .gitignore

Effective use of `.gitignore` is crucial for maintaining a clean and manageable Git repository. This file tells Git which files or folders to intentionally ignore, preventing them from being tracked or included in commits.

### 7.1 What is .gitignore?

A `.gitignore` file is a plain text file where each line contains a pattern for files or directories that Git should ignore. This is particularly useful for excluding temporary files, build artifacts, dependency directories (like `node_modules`), environment-specific configuration files, and operating system-generated files (like `.DS_Store`). By ignoring these files, you ensure that your repository only contains relevant source code and project assets, reducing repository size and avoiding unnecessary conflicts.

### 7.2 Setting Up .gitignore

To set up a `.gitignore` file, you typically create it in the root directory of your Git repository. Each line in the file specifies a pattern for files or directories to ignore.

1. **Create the `.gitignore` file:**

```bash
touch .gitignore
```

2. **Add patterns to the file.** Below is a suggested `.gitignore` template for projects that might involve both Node.js and Python components, along with common system and log files. You should adapt this to your specific project needs.

```
# Node.js specific ignores
node_modules/
npm-debug.log
# Optional: npm lock file if you prefer to not track it
package-lock.json

# Python specific ignores
__pycache__/
*.py[cod]
*.pyo
*.pyc

# Environment files
.env
.venv/
env/
venv/

# IDE specific files
.idea/
.vscode/
*.swp
*.swo

# Build directories
build/
dist/
*.egg-info/

# System Files (macOS, Windows)
.DS_Store
**/.DS_Store
Thumbs.db

# Log files
*.log
nohup.out
```

3. **Save and commit the `.gitignore` file:**

After adding your desired patterns, save the file and commit it to your repository. This ensures that all collaborators will use the same ignore rules.

```bash
git add .gitignore
git commit -m "Add .gitignore"
```

GitHub maintains extensive `.gitignore` templates for various programming languages and frameworks at `https://github.com/github/gitignore`.

### 7.3 Untracking Already Added Files

A common scenario is that you might have mistakenly added and committed files (e.g., `node_modules/`, `.DS_Store`, `.env`) before setting up your `.gitignore` file. In such cases, Git will continue to track these files even after you add them to `.gitignore`.

To remove these files from Git's tracking (but keep them locally in your working directory), you need to use the `git rm --cached` command.

**To untrack specific files or directories:**

```bash
# Untrack a single file
git rm --cached .DS_Store

# Untrack a directory recursively
git rm -r --cached node_modules

# Untrack multiple items
git rm --cached .env
git rm -r --cached build/
git rm -r --cached .gradle/
git rm -r --cached .idea/

# Commit the changes
git commit -m "Remove unwanted tracked files and apply .gitignore"
git push
```

**To untrack all ignored files at once:**

```bash
# Untrack everything
git rm -r --cached .

# Re-add only files that should be tracked
git add .

# Commit
git commit -m "Clean up unwanted tracked files using .gitignore"
```

This sequence first untracks everything in your repository, then re-adds only the files that are not matched by any pattern in your `.gitignore` file.

### 7.4 Handling Tracked Files with .gitignore

**Important:** Adding a file to `.gitignore` ONLY prevents untracked files from being added. It does NOT stop tracking files that are already tracked by Git.

**The Issue:**

If `a.txt` is already tracked by Git, adding it to `.gitignore` will NOT prevent future changes from being committed. The file will continue to be tracked and any modifications will still show up in `git status` and be included in commits.

**The Solution - Remove from Tracking:**

```bash
# Add to .gitignore first
echo "a.txt" >> .gitignore

# Remove from Git tracking but keep local file
git rm --cached a.txt

# Commit the changes
git add .gitignore
git commit -m "Stop tracking a.txt and update .gitignore"
git push
```

**What this does:**
- `a.txt` will be deleted from the GitHub repository
- The file remains in your local directory
- Future changes to `a.txt` will be ignored by Git

**Note:** There is no way to keep a file in the repository while preventing future updates to it. You must choose between:
- Keep file in repo + accept future updates
- Remove file from repo + ignore future changes

### 7.5 Common .gitignore Mistakes and Fixes

One common mistake is accidentally removing the `.gitignore` file from Git tracking. If you run `git rm -r --cached .gitignore`, the file will remain on your disk but Git will no longer track it.

To fix this, simply re-add the `.gitignore` file to Git:

```bash
git add .gitignore
git commit -m "Re-add .gitignore"
```

### 7.6 Best Practices for .gitignore

Adhering to these best practices will help you maintain a clean and efficient Git repository:

- **Create `.gitignore` early:** Always create and configure your `.gitignore` file at the very beginning of your project. This prevents unwanted files from ever being tracked.
- **Never commit sensitive or unnecessary files:** Ensure that directories like `node_modules`, `.env` files (containing sensitive environment variables), and OS-specific junk files are always ignored.
- **Use `git rm --cached`:** If files are accidentally committed, use `git rm --cached` to stop tracking them without deleting them locally.
- **Leverage GitHub's `.gitignore` templates:** Utilize the official `.gitignore` templates provided by GitHub for project-specific setups.

---

## 8. Staging Area Management

Understanding how to manage the staging area is crucial for controlling what gets included in your commits.

### 8.1 Removing Files from Staging

If you've staged files but want to unstage them before committing, use `git restore --staged`.

**To unstage specific files:**

```bash
git restore --staged filename.txt
```

**To unstage multiple files:**

```bash
git restore --staged file1.js file2.py file3.css
```

**To unstage entire directories:**

```bash
git restore --staged build/ .gradle/ .idea/
```

**To unstage all staged files:**

```bash
git restore --staged .
```

### 8.2 Staging Files from Parent Directories

When working in subdirectories, files in parent directories won't be staged by `git add .` because `.` refers to the current directory.

**Problem scenario:**

```bash
# You're in android/ subdirectory
cd android/
git add .
git status
# Shows: modified: ../package.json (not staged)
```

**Solutions:**

**Option 1: Navigate to project root (recommended):**

```bash
# Go to parent directory
cd ..

# Now stage all changes
git add .
git commit -m "Your message"
```

**Option 2: Stage from current location using parent path:**

```bash
# Stage specific parent directory files
git add ../package.json ../src/

# Or stage all changes from parent
git add ..
```

### 8.3 Removing Specific Files from Staging

If you've staged multiple files but want to remove some specific ones from the staging area:

```bash
# Check what's staged
git status

# Remove specific files from staging
git restore --staged gpg-wrapper.sh gradle.properties

# Verify
git status
```

---

## 9. Git History Manipulation

Git provides powerful tools for manipulating commit history. Use these carefully, especially on shared branches.

### 9.1 Resetting to Previous Commits

Resetting allows you to move your branch pointer to a different commit, optionally keeping or discarding changes.

**To reset to a specific commit and discard all changes after it:**

```bash
# Reset to commit hash (e.g., 547a7c7)
git reset --hard 547a7c7

# Force push to update remote
git push --force-with-lease origin main
```

**To reset but keep changes staged:**

```bash
git reset --soft HEAD~1
```

**To reset but keep changes unstaged:**

```bash
git reset HEAD~1
```

**Creating a backup before resetting:**

```bash
# Create backup branch first
git branch backup-before-reset

# Then reset
git reset --hard 547a7c7

# Force push
git push --force-with-lease origin main
```

### 9.2 Interactive Rebase

Interactive rebase allows you to modify, reorder, squash, or remove commits in your history.

**To start interactive rebase:**

```bash
# Rebase from the beginning of the repository
git rebase -i --root

# Rebase last N commits
git rebase -i HEAD~5

# Rebase from a specific commit
git rebase -i commit-hash
```

**In the interactive rebase editor:**

- **pick** - Use commit as-is
- **drop** - Remove commit entirely
- **reword** - Change commit message
- **edit** - Stop for amending
- **squash** - Combine with previous commit
- **fixup** - Like squash but discard commit message

**Editor navigation (Vim):**
1. Press `i` to enter INSERT mode
2. Edit the commands (change "pick" to "drop", etc.)
3. Press `Esc` to exit INSERT mode
4. Type `:wq` and press `Enter` to save and quit

### 9.3 Removing Commits from History

To remove specific commits (e.g., those containing sensitive data) from Git history:

**Method 1: Interactive Rebase**

```bash
# Start interactive rebase
git rebase -i --root

# In the editor, change "pick" to "drop" for commits to remove
# Example:
# drop 0697f23 first commit
# drop 04ea732 temp
# pick c558987 gradle build issue fixed

# Save and exit
# Then force push
git push --force-with-lease origin main
```

**Method 2: Using git revert (safer for shared branches)**

Instead of removing commits, create new commits that undo the changes:

```bash
# Revert a range of commits
git revert --no-edit commit-hash..HEAD

# Or revert specific commits
git revert --no-edit commit-hash1
git revert --no-edit commit-hash2

# Push normally (no force needed)
git push origin main
```

### 9.4 Reverting Changes

**To undo a specific commit without removing it from history:**

```bash
git revert commit-hash
```

**To create a new commit with a specific old commit's content:**

```bash
# Checkout files from an old commit
git checkout commit-hash -- .

# Commit as new state
git commit -m "Revert to working state from commit-hash"
git push origin main
```

**To jump to a specific commit and make it the new HEAD:**

```bash
# Option 1: Create new commit with old state
git checkout f4bde0e -- .
git commit -m "Revert to working state from f4bde0e"
git push origin main

# Option 2: Reset and force push (rewrites history)
git reset --hard f4bde0e
git push --force-with-lease origin main
```

---

## 10. Git Tagging

Tags are references to specific points in Git history, commonly used for marking release versions.

### 10.1 What are Git Tags?

Git tags are used to mark specific commits as important, typically for:
- **Version Releases:** Mark release points (v1.0.0, v2.1.5, etc.)
- **GitHub Releases:** Tags appear in the "Releases" section on GitHub
- **Reference Points:** Easy way to checkout specific versions later

### 10.2 Creating Tags

**Create an annotated tag (recommended):**

```bash
git tag -a v1.0.0 -m "Initial release of PVM for macOS"
```

**Create a lightweight tag:**

```bash
git tag v1.0.0
```

**Push a specific tag to remote:**

```bash
git push origin v1.0.0
```

**Push all tags to remote:**

```bash
git push origin --tags
```

### 10.3 Managing Tags

**List all tags:**

```bash
git tag
```

**View tag details:**

```bash
git show v1.0.0
```

**Delete a local tag:**

```bash
git tag -d v1.0.0
```

**Delete a remote tag:**

```bash
git push origin --delete v1.0.0
```

**Checkout a specific tag:**

```bash
git checkout v1.0.0
```

**Example versioning workflow:**

```bash
# First stable release
git tag -a v1.0.0 -m "First stable release"
git push origin v1.0.0

# Bug fix release
git tag -a v1.0.1 -m "Bug fixes for login issue"
git push origin v1.0.1

# Major update
git tag -a v2.0.0 -m "Complete UI redesign"
git push origin v2.0.0
```

---

## 11. Troubleshooting Common Git Issues

Even with a good understanding of Git, you might encounter common issues. This section provides solutions and explanations for frequently faced problems.

### 11.1 Updates Rejected Due to Remote Changes

**Error:** `Updates were rejected because the remote contains work that you do not have locally`

This means the remote repository has commits that are not present in your local branch.

**Solution 1: Merge Remote Changes (Recommended)**

```bash
# Set upstream branch
git branch --set-upstream-to=origin/main main

# Pull and merge remote changes
git pull origin main --allow-unrelated-histories

# Push your changes
git push origin main
```

**Solution 2: Force Push (⚠️ Use with caution)**

This will delete everything in the remote and replace it with your local version:

```bash
git push origin main --force
```

### 11.2 Handling Diverged Branches During Pull

If your local and remote branches have diverged, Git needs to know how to combine them.

**Fix Option 1: Merge (Safe and Common)**

```bash
git config pull.rebase false
git pull
```

**Fix Option 2: Rebase (Cleaner History)**

```bash
git config pull.rebase true
git pull --rebase
```

**Fix Option 3: One-time Override**

```bash
# Merge for this pull only
git pull --no-rebase

# Rebase for this pull only
git pull --rebase

# Fast-forward only
git pull --ff-only
```

**Set as Global Default:**

```bash
# Merge (recommended for simplicity)
git config --global pull.rebase false

# Rebase (cleaner history)
git config --global pull.rebase true

# Fast-forward only
git config --global pull.ff only
```

### 11.3 GitHub File Not Showing

**Problem:** File doesn't appear after `git add`, `git commit`, and `git push`.

**Common Causes:**

1. **Incorrect file creation** - Using `mkdir` instead of `touch`
2. **File ignored by .gitignore** - A rule is blocking it

**Step-by-Step Fix:**

**Step 1: Create the file correctly**

```bash
# Create directory structure
mkdir -p .github/workflows

# Create the file (not directory)
touch .github/workflows/deploy.yml

# Add initial content
echo "# GitHub Actions workflow" > .github/workflows/deploy.yml
```

**Step 2: Check which .gitignore rule is blocking it**

```bash
git check-ignore -v .github/workflows/deploy.yml
```

**Step 3: Fix the .gitignore rules**

Option A - Refine the rule:

```
# Before (too broad):
.github/

# After (more specific):
.github/*
!.github/workflows/
!.github/workflows/deploy.yml
```

Option B - Force add the file:

```bash
git add -f .github/workflows/deploy.yml
git commit -m "Add GitHub Actions deploy workflow"
git push
```

**Step 4: Verify the file was added**

```bash
git status
git log --name-status
```

### 11.4 Resolving SSH Key Errors

**Error:** `Permission denied (publickey)` or `no such identity: /Users/username/.ssh/id_ed25519`

**Solution 1: Use HTTPS Instead (Simpler)**

```bash
git remote set-url origin https://github.com/your-username/your-repo.git
```

**Solution 2: Fix SSH Key Setup**

1. **Check for existing keys:**

```bash
ls -la ~/.ssh/
```

2. **Generate new SSH key:**

```bash
ssh-keygen -t ed25519 -C "your-email@example.com"
```

3. **Add key to SSH agent:**

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

4. **Add SSH key to GitHub:**

```bash
# Copy public key
cat ~/.ssh/id_ed25519.pub

# Go to GitHub → Settings → SSH and GPG keys → New SSH key
# Paste the key
```

5. **Test connection:**

```bash
ssh -T git@github.com
```

### 11.5 Resolving .DS_Store Issues

**Problem:** `.DS_Store` files (macOS system files) keep appearing in Git.

**Solution:**

**Remove all .DS_Store files from staging:**

```bash
git restore --staged **/.DS_Store
```

**Delete actual .DS_Store files:**

```bash
find . -name ".DS_Store" -type f -delete
```

**Remove from Git tracking:**

```bash
# Remove from Git but keep local
git rm --cached .DS_Store

# Or force remove if Git complains
git rm -f --cached .DS_Store
```

**Prevent future tracking:**

```bash
# Add to .gitignore
echo ".DS_Store" >> .gitignore
echo "**/.DS_Store" >> .gitignore

# Commit changes
git add .gitignore
git commit -m "Remove .DS_Store files and update .gitignore"
git push
```

### 11.6 Resolving .idea/ and Build Directory Issues

**Problem:** IDE configuration folders (`.idea/`) or build directories (`build/`, `dist/`) are being tracked.

**Solution:**

**Remove from staging:**

```bash
git restore --staged build/ .gradle/ .idea/
```

**Remove from Git tracking:**

```bash
# For directories, use -r flag
git rm -r --cached .idea/
git rm -r --cached build/
git rm -r --cached dist/

# Add to .gitignore
echo ".idea/" >> .gitignore
echo "build/" >> .gitignore
echo "dist/" >> .gitignore

# Commit
git add .gitignore
git commit -m "Remove IDE and build files from tracking"
git push
```

**If Git complains about non-existent paths:**

The directory might not be tracked. Just add it to `.gitignore`:

```bash
echo "dist/" >> .gitignore
git add .gitignore
git commit -m "Add dist/ to .gitignore"
```

### 11.7 Staged File Removal Issues

**Problem:** Git refuses to remove a staged file with error about "staged content different from both file and HEAD."

**Solution:**

**Option 1: Unstage first, then remove (recommended):**

```bash
# Unstage the file
git restore --staged .DS_Store

# Remove from tracking
git rm --cached .DS_Store

# Delete actual file
rm .DS_Store
```

**Option 2: Force removal:**

```bash
# Force remove (also deletes file)
git rm -f .DS_Store
```

### 11.8 Undoing Git Operations

**Undo last commit but keep changes:**

```bash
git reset --soft HEAD~1
```

**Undo last commit and discard changes:**

```bash
git reset --hard HEAD~1
```

**Undo a git rm --cached operation:**

```bash
# If not committed yet
git add filename.txt

# If already committed
git reset --soft HEAD~1
git add filename.txt
```

**Undo force push / rebase disaster:**

```bash
# View recent operations
git reflog

# Reset to before the operation (e.g., HEAD@{1})
git reset --hard HEAD@{1}

# Force push to restore
git push --force-with-lease origin main
```

**Undo changes made by git revert:**

```bash
# Find the commit hash before the revert in reflog
git reflog

# Reset to that commit
git reset --hard commit-hash-before-revert

# Force push
git push --force-with-lease origin main
```

---

## 12. Advanced Topics

This section delves into more advanced Git topics for power users.

### 12.1 Cleaning Git History (Removing Sensitive Data)

If sensitive credentials, API keys, or other confidential information are accidentally committed, you need to rewrite Git history to truly remove them.

**⚠️ Warning:** Rewriting Git history changes commit hashes. Communicate with your team before performing these operations.

**Using git-filter-repo:**

1. **Install git-filter-repo:**

```bash
pip install git-filter-repo
```

2. **Remove sensitive file from all commits:**

```bash
git filter-repo --path path/to/sensitive-file.txt --invert-paths --force
```

3. **Force push cleaned history:**

```bash
git push --force-with-lease origin main
```

**Alternative: Using BFG Repo-Cleaner**

BFG Repo-Cleaner is another powerful tool for cleaning repositories. Refer to its official documentation for usage.

### 12.2 SSH Key Setup for GitHub

SSH keys provide secure authentication with GitHub without exposing passwords.

**Complete SSH Setup:**

1. **Check for existing keys:**

```bash
ls -al ~/.ssh
```

2. **Generate new SSH key:**

```bash
ssh-keygen -t ed25519 -C "your-email@example.com"
```

Or for older systems:

```bash
ssh-keygen -t rsa -b 4096 -C "your-email@example.com"
```

3. **Start SSH agent and add key:**

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

4. **Copy public key:**

```bash
cat ~/.ssh/id_ed25519.pub
```

5. **Add to GitHub:**
   - Go to GitHub → Settings → SSH and GPG keys → New SSH key
   - Paste the public key
   - Give it a descriptive title

6. **Test connection:**

```bash
ssh -T git@github.com
```

---

## 13. Summary of Key Git Commands

| Command | Description | Example |
|---------|-------------|---------|
| `git init` | Initialize new repository | `git init` |
| `git clone URL` | Clone existing repository | `git clone https://github.com/user/repo.git` |
| `git status` | Show repository status | `git status` |
| `git add .` | Stage all changes | `git add .` |
| `git add file` | Stage specific file | `git add README.md` |
| `git commit -m "msg"` | Commit staged changes | `git commit -m "Add feature"` |
| `git commit --amend` | Modify last commit | `git commit --amend -m "New message"` |
| `git push` | Push to remote | `git push origin main` |
| `git push --force-with-lease` | Safe force push | `git push --force-with-lease origin main` |
| `git pull` | Pull from remote | `git pull origin main` |
| `git fetch` | Fetch remote changes | `git fetch origin` |
| `git branch` | List branches | `git branch` |
| `git branch -r` | List remote branches | `git branch -r` |
| `git checkout branch` | Switch branch | `git checkout develop` |
| `git checkout -b branch` | Create and switch branch | `git checkout -b feature/new` |
| `git merge branch` | Merge branch | `git merge feature/new` |
| `git log` | View commit history | `git log --oneline -10` |
| `git reflog` | View reference log | `git reflog` |
| `git reset --soft HEAD~1` | Undo commit keep changes | `git reset --soft HEAD~1` |
| `git reset --hard commit` | Reset to commit | `git reset --hard abc123` |
| `git revert commit` | Revert commit | `git revert abc123` |
| `git rebase -i --root` | Interactive rebase | `git rebase -i --root` |
| `git restore --staged file` | Unstage file | `git restore --staged app.js` |
| `git rm --cached file` | Untrack file | `git rm --cached .env` |
| `git rm -r --cached dir/` | Untrack directory | `git rm -r --cached node_modules/` |
| `git remote -v` | List remotes | `git remote -v` |
| `git remote set-url origin URL` | Change remote URL | `git remote set-url origin https://...` |
| `git tag -a v1.0.0 -m "msg"` | Create annotated tag | `git tag -a v1.0.0 -m "Release"` |
| `git push origin v1.0.0` | Push tag | `git push origin v1.0.0` |
| `git check-ignore -v file` | Check ignore rule | `git check-ignore -v app.log` |
| `git config --global user.name` | Set username | `git config --global user.name "John"` |
| `git config --global user.email` | Set email | `git config --global user.email "a@b.com"` |

---

**End of Documentation**

For more information, visit the official Git documentation at `https://git-scm.com/doc`.
