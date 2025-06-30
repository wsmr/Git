# Git Workflow Documentation


## Summary of Key Git Commands

This section provides a quick reference for some of the most frequently used Git commands discussed in this document.

| Command | Description | Example Usage |
|---|---|---|
| `rd .git /S/Q` | Removes the `.git` directory (Windows). Use with caution. | `rd .git /S/Q` |
| `rm -rf .git` | Removes the `.git` directory (macOS/Linux). Use with caution. | `rm -rf .git` |
| `git init` | Initializes a new Git repository. | `git init` |
| `git add .` | Stages all changes in the current directory. | `git add .` |
| `git commit -m "Message"` | Records staged changes with a message. | `git commit -m "Initial commit"` |
| `git remote add origin URL` | Adds a new remote repository. | `git remote add origin https://github.com/user/repo.git` |
| `git push -u origin master` | Pushes local commits to a remote and sets upstream. | `git push -u origin master` |
| `git remote show origin` | Shows information about the remote. | `git remote show origin` |
| `git remote set-url origin URL` | Changes the URL of an existing remote. | `git remote set-url origin https://github.com/user/new-repo.git` |
| `git branch` | Lists local branches. | `git branch` |
| `git config --global user.name "Name"` | Sets global user name. | `git config --global user.name "John Doe"` |
| `git config --global user.email "Email"` | Sets global user email. | `git config --global user.email "john.doe@example.com"` |
| `ssh-keygen` | Generates SSH keys. | `ssh-keygen` |
| `git stash` | Temporarily shelves changes. | `git stash` |
| `git stash --help` | Displays help for `git stash`. | `git stash --help` |
| `git branch -r` | Lists remote-tracking branches. | `git branch -r` |
| `git checkout branch_name` | Switches to an existing branch. | `git checkout feature-branch` |
| `git checkout -b new_branch` | Creates and switches to a new branch. | `git checkout -b new-feature` |
| `git cherry-pick <hash>` | Applies a specific commit from another branch. | `git cherry-pick a1b2c3d` |
| `git cherry-pick --continue` | Continues cherry-pick after conflict resolution. | `git cherry-pick --continue` |
| `git cherry-pick --skip` | Skips the current patch during cherry-pick. | `git cherry-pick --skip` |
| `git cherry-pick --abort` | Cancels the cherry-pick operation. | `git cherry-pick --abort` |
| `git checkout -` | Switches to the previous branch. | `git checkout -` |
| `git pull` | Fetches and integrates remote changes. | `git pull` |
| `git pull origin main --allow-unrelated-histories` | Pulls and merges histories without common ancestor. | `git pull origin main --allow-unrelated-histories` |
| `git pull --rebase origin main` | Pulls and rebases local commits on top of remote. | `git pull --rebase origin main` |
| `git push origin main --force` | Force pushes to remote (use with extreme caution). | `git push origin main --force` |
| `git config --global pull.rebase false` | Sets `git pull` to merge by default. | `git config --global pull.rebase false` |
| `git config --global pull.rebase true` | Sets `git pull` to rebase by default. | `git config --global pull.rebase true` |
| `git config --global pull.ff only` | Sets `git pull` to fast-forward only by default. | `git config --global pull.ff only` |
| `git clone -b branch URL` | Clones a specific branch. | `git clone -b stable https://github.com/user/repo.git` |
| `git rm -f .DS_Store` | Forcefully removes `.DS_Store` from Git. | `git rm -f .DS_Store` |
| `git rm -f --cached .DS_Store` | Forcefully untracks `.DS_Store` (keeps locally). | `git rm -f --cached .DS_Store` |
| `echo .DS_Store >> .gitignore` | Adds `.DS_Store` to `.gitignore`. | `echo .DS_Store >> .gitignore` |
| `git rm -r --cached directory` | Untracks a directory (keeps locally). | `git rm -r --cached android/.idea/` |
| `git rm -rf directory` | Removes a directory from Git and locally. | `git rm -rf android/.idea/` |



## 1. Introduction

This document provides a concise guide to common Git commands and workflows, focusing on practical scenarios for managing your local and remote repositories. It covers initial setup, basic operations, and solutions to common issues encountered during development.

## 2. Getting Started

### 2.1 Initializing and Pushing a New Repository

To start a new Git repository and push its contents to a remote server:

1.  **Remove existing Git metadata (if any):**

    If you have a `.git` directory from a previous initialization that you want to discard, you can remove it. **Use this command with caution**, as it permanently deletes the Git history for the current directory.

```bash
rd .git /S/Q # For Windows
rm -rf .git # For macOS/Linux
```

2.  **Initialize a new Git repository:**

    This command creates a new `.git` subdirectory in your current working directory, making it a Git repository.

```bash
git init
```

3.  **Add all files to the staging area:**

    This command stages all changes in your current directory, preparing them for the next commit.

```bash
git add .
```

4.  **Commit the staged changes:**

    This records the staged changes to your local repository with a descriptive message.

```bash
git commit -m "Initial commit message"
```

5.  **Add a remote repository:**

    Connect your local repository to a remote repository (e.g., on GitHub). Replace `URL` with the actual URL of your remote repository.

```bash
git remote add origin URL
```

6.  **Push your local commits to the remote repository:**

    The `-u` flag sets the upstream branch, allowing you to use `git push` without specifying the remote and branch in subsequent pushes.

```bash
git push -u origin master
```

### 2.2 Pushing an Existing Repository

If you have an existing local repository that you want to push to a new remote, or to a different remote:

1.  **Add the remote repository:**

```bash
git remote add origin URL
```

2.  **Push your local commits to the remote:**

```bash
git push -u origin master
```

### 2.3 Managing Remote URLs

To view the configured remote URLs for your repository:

```bash
git remote show origin
```

To change the URL of an existing remote (e.g., if the repository moved or you want to switch between HTTPS and SSH):

```bash
git remote set-url origin https://github.com/your-username/your-repo.git
```

## 3. Git Configuration

### 3.1 Setting User Information

It is crucial to configure your Git username and email, as this information is embedded in every commit you make.

To set your global Git username:

```bash
git config --global user.name "YOUR_USERNAME"
```

To verify your global Git username:

```bash
git config --global user.name
```

To set your global Git email address:

```bash
git config --global user.email "your_email_address@example.com"
```

To verify your global Git email address:

```bash
git config --global user.email
```

## 4. Branch Management

To list all local branches in your repository:

```bash
git branch
```

## 5. Stashing Changes

Git stash temporarily shelves (or stashes) changes you've made to your working copy so you can work on something else, and then come back and re-apply them later.

To stash your current changes:

```bash
git stash
```

To view help documentation for `git stash`:

```bash
git stash --help
```

## 6. Working with Remote Branches and Cherry-Picking

This section describes a workflow for pushing code changes from your `main` branch to another specific branch without directly pushing to `main`.

1.  **Stage your changes:**

```bash
git add .
```

2.  **Check repository status:**

```bash
git status
```

3.  **Commit your staged changes:**

```bash
git commit -m "Your commit message"
```

4.  **List remote branches:**

    Check for existing remote branches to ensure the target branch exists.

```bash
git branch -r
```

5.  **Switch to the target branch:**

    If the branch already exists locally:

```bash
git checkout branch_name
```

    If you need to create a new branch and switch to it:

```bash
git checkout -b branch_name
```

6.  **Cherry-pick the commit:**

    Apply a specific commit from your `main` branch to the `branch_name`. Replace `<commit-hash>` with the actual hash of the commit you want to apply.

```bash
git cherry-pick <commit-hash>
```

    During cherry-picking, you might encounter conflicts. Git will prompt you to resolve them. After resolving conflicts, use `git cherry-pick --continue`. Other options include `git cherry-pick --skip` to skip the current patch or `git cherry-pick --abort` to cancel the operation.

7.  **Push the changes to the remote target branch:**

```bash
git push -u origin branch_name
```

8.  **Switch back to your previous branch and pull latest changes:**

```bash
git checkout -
git pull
```

## 7. Pulling Local Project Code into a New GitHub Repository

This workflow describes how to take an existing local project and push it to a newly created, empty GitHub repository.

1.  **Initialize the local directory as a Git repository (if not already done):**

```bash
git init
```

2.  **Add the remote GitHub repository as "origin":**

    Replace `<your-username>` and `<repo-name>` with your GitHub username and the name of your new repository.

```bash
git remote add origin https://github.com/<your-username>/<repo-name>.git
```

3.  **Add all your project files to the staging area:**

```bash
git add .
```

4.  **Commit the files with an initial commit message:**

```bash
git commit -m "Initial project commit"
```

5.  **Push your code to the remote repository on GitHub:**

```bash
git push -u origin main
```

**Troubleshooting `! [rejected] main -> main (fetch first)`:**

    This error occurs because the remote GitHub repository already has commits (e.g., a `LICENSE` file or `README.md` created during repository initialization on GitHub) that your local repository doesn't have. Git prevents you from pushing directly to avoid overwriting remote work.

    The hint suggests you should pull the changes from GitHub first before pushing.

```bash
git pull origin main
```

    After pulling, you should then be able to push your local commits:

```bash
git push origin main
```

**Troubleshooting `! [rejected] main -> main (non-fast-forward)`:**

    This error indicates that your local and remote branches have diverged; both have new commits that the other doesn't have. Git needs explicit instructions on how to reconcile these differences when pulling.

    You need to explicitly configure how you want Git to reconcile the divergence. The main options are:

    *   `--rebase`: Rebase your local changes on top of the updated remote branch. This replays your commits after fetching, resulting in a linear history.
    *   `--merge`: Merge the remote changes into your local branch. This creates a merge commit.
    *   `--ff-only`: Only allow fast-forward updates, meaning the pull will only succeed if the remote is ahead and your local branch has no additional commits.

**Recommended Solution: Rebase (for cleaner history)**

    To fetch the remote changes and then replay your local commits on top, avoiding merge commits:

```bash
git pull --rebase origin main
```

    Once the rebase completes cleanly (you might need to resolve conflicts if any), you should then be able to push your local branch to the remote:

```bash
git push origin main
```

## 8. Resolving SSH Key Errors (Permission Denied)

If you encounter `Permission denied (publickey)` or `no such identity: ~/.ssh/id_ed25519: No such file or directory` errors, it means Git is configured to use SSH to connect to GitHub, but it cannot find or use your SSH private key.

**Root Cause:**

Your Git configuration (e.g., `remote.origin.url=git@github.com:your-username/your-repo.git`) specifies SSH for remote operations, but the SSH private key file it expects either does not exist or is not accessible. Consequently, GitHub denies access because it cannot authenticate your connection.

**🛠️ Solution Options:**

**Option 1: Use HTTPS Instead of SSH (Simpler)**

If you prefer not to deal with SSH keys, you can switch your remote URL to use HTTPS. This will prompt you for your GitHub credentials (username and password, or a Personal Access Token) when performing operations that require authentication.

```bash
git remote set-url origin https://github.com/your-username/your-repo.git
```

**Option 2: Fix SSH Key (Advanced / Recommended for Power Users)**

If you prefer to use SSH for its security and convenience, you need to ensure your SSH key is correctly set up and accessible.

1.  **Generate a New SSH Key:**

    If you don't have an existing key or want to create a new one, use `ssh-keygen`. Replace `your-email@example.com` with your GitHub email address.

```bash
ssh-keygen -t ed25519 -C "your-email@example.com"
```

    Press `Enter` to accept the default file path (e.g., `~/.ssh/id_ed25519`). You can optionally set a strong passphrase for added security.

2.  **Add the Key to SSH Agent:**

    The `ssh-agent` manages your SSH keys and passphrases.

    *   Start the `ssh-agent`:

```bash
eval "$(ssh-agent -s)"
```

    *   Add your private key to the agent:

```bash
ssh-add ~/.ssh/id_ed25519
```

        (Replace `id_ed25519` with your actual private key filename if different.) You will be prompted for your passphrase if you set one.

3.  **Add the SSH Key to GitHub:**

    You need to add your public SSH key to your GitHub account.

    *   **Copy your public key to your clipboard:**

```bash
cat ~/.ssh/id_ed25519.pub
```

        Copy the entire output.

    *   **Go to GitHub:** Navigate to `Settings` -> `SSH and GPG keys` -> `New SSH key`. Paste the copied public key into the field and give it a descriptive title.

4.  **Test Your SSH Connection:**

    After adding the key to GitHub, test your connection:

```bash
ssh -T git@github.com
```

    A successful connection will display a message like: `Hi your-username! You've successfully authenticated, but GitHub does not provide shell access.`

**Bonus: Typo in Your Remote URL?**

Sometimes, the issue might be a simple typo in your remote URL. Double-check the actual repository name on GitHub and correct it if needed:

```bash
git remote set-url origin git@github.com:your-username/your-correct-repo-name.git
```

## 9. Resolving Staged File Removal Issues

Sometimes, Git might refuse to remove a file or directory because its contents are staged (added to Git's index but not yet committed), and Git requires explicit confirmation for the removal.

**Problem: Git refuses to remove a staged file (e.g., `.DS_Store`).**

If you encounter an error message indicating that a file like `.DS_Store` is staged and Git doesn't want to remove it, it means the file's content in the staging area differs from both your working directory and the last committed version. Git is being cautious and wants you to explicitly confirm the removal.

**Solution:**

To forcefully remove the file from Git's tracking (but keep it locally), use the `-f` (force) and `--cached` flags:

```bash
git rm -f --cached .DS_Store
```

**Next Steps (Recommended for `.DS_Store` files):**

After untracking, it's crucial to add `.DS_Store` to your `.gitignore` file to prevent it from being tracked again in the future. You can append the line to your `.gitignore` file:

```bash
echo .DS_Store >> .gitignore
```

Then, commit these changes to your `.gitignore`:

```bash
git commit -m "Remove .DS_Store from tracking and update .gitignore"
```

**Problem: Git refuses to remove a staged directory (e.g., `android/.idea/`).**

If Git refuses to remove a directory like `android/.idea/` because its files are staged, it means the files within that directory are in Git's index but not yet committed, and Git requires explicit confirmation for their removal.

**Solution Options:**

1.  **Remove the directory from Git but keep it locally (Most Common):**

    This is the typical approach for IDE-specific folders. It removes the directory from Git's tracking but leaves it in your local working directory.

```bash
git rm -r --cached android/.idea/
```

    Then, add it to your `.gitignore` file to prevent it from being tracked again:

```bash
echo android/.idea/ >> .gitignore
```

    Finally, commit these changes:

```bash
git commit -m "Remove android/.idea/ from git tracking and update .gitignore"
```

2.  **Remove the directory from Git AND your local machine:**

    If you want to completely remove the directory from both Git and your local filesystem:

```bash
git rm -rf android/.idea/
```

    Then commit the removal:

```bash
git commit -m "Remove android/.idea/ completely"
```

**💡 Important Tip:** `.idea/` folders are specific to IDEs (like Android Studio or IntelliJ) and generally should not be version controlled. Excluding them from your repository helps avoid conflicts and keeps your repository clean and focused on source code.




## 10. Common Git Pull Scenarios and Solutions

When pulling changes from a remote repository, you might encounter situations where your local and remote branches have diverged. Git provides several strategies to handle these divergences.

### 10.1 Diverged Branches During Pull

If your local and remote branches have diverged (meaning both have new commits that the other doesn't have), Git needs to know how to combine them during a pull. You might see a message indicating this divergence.

**What This Means:**

Your local branch and the remote branch both have new commits that the other doesn't have. Git needs to know whether to:

*   Merge the changes (default in older Git versions).
*   Rebase your changes on top of the remote.
*   Fast-forward only (only allow pull if the remote is ahead and no conflict exists).

**Fix Option 1: Merge (Safe and Common)**

This option merges the remote changes into your local branch with a merge commit.

```bash
git config pull.rebase false
git pull
```

**Fix Option 2: Rebase (Cleaner History, Advanced)**

This option re-applies your local commits on top of the latest remote commits. This results in a cleaner, linear history but can cause conflicts that you'll need to resolve.

```bash
git config pull.rebase true
git pull --rebase
```

**Fix Option 3: One-time Override**

If you don't want to change your global Git configuration, you can use these options for a one-time pull:

*   **Merge:**

```bash
git pull --no-rebase
```

*   **Rebase:**

```bash
git pull --rebase
```

*   **Fast-forward only:**

```bash
git pull --ff-only
```

**To Set as Global Default (Recommended for Future Clarity):**

Choose one of these to set your preferred default behavior for `git pull`:

*   **Merge (recommended for simplicity):**

```bash
git config --global pull.rebase false
```

*   **Rebase (recommended for cleaner history, if comfortable with conflict resolution):**

```bash
git config --global pull.rebase true
```

*   **Fast-forward only:**

```bash
git config --global pull.ff only
```

## 11. Cloning a Specific Branch

Sometimes, you might want to clone a specific branch of a repository directly, rather than the default branch (usually `main` or `master`). This is particularly useful for projects that maintain different branches for active development and stable releases.

To clone a specific branch (e.g., `stable`):

```bash
git clone -b stable https://github.com/your-username/your-repo.git
```

The `-b` (or `--branch`) flag tells Git which branch to check out immediately after cloning. This avoids the need to manually switch branches after the initial clone.

**Why Use `-b stable`?**

Many projects use `main` or `master` for active development and `stable` for a more tested and production-ready version. Using `-b stable` ensures you get a reliable starting point for your work without having to manually switch branches after cloning.





## 12. Common Git Pull Scenarios and Solutions

When pulling changes from a remote repository, you might encounter situations where your local and remote branches have diverged. Git provides several strategies to handle these divergences.

### 12.1 Diverged Branches During Pull

If your local and remote branches have diverged (meaning both have new commits that the other doesn't have), Git needs to know how to combine them during a pull. You might see a message indicating this divergence.

**What This Means:**

Your local branch and the remote branch both have new commits that the other doesn't have. Git needs to know whether to:

*   Merge the changes (default in older Git versions).
*   Rebase your changes on top of the remote.
*   Fast-forward only (only allow pull if the remote is ahead and no conflict exists).

**Fix Option 1: Merge (Safe and Common)**

This option merges the remote changes into your local branch with a merge commit.

```bash
git config pull.rebase false
git pull
```

**Fix Option 2: Rebase (Cleaner History, Advanced)**

This option re-applies your local commits on top of the latest remote commits. This results in a cleaner, linear history but can cause conflicts that you'll need to resolve.

```bash
git config pull.rebase true
git pull --rebase
```

**Fix Option 3: One-time Override**

If you don't want to change your global Git configuration, you can use these options for a one-time pull:

*   **Merge:**

```bash
git pull --no-rebase
```

*   **Rebase:**

```bash
git pull --rebase
```

*   **Fast-forward only:**

```bash
git pull --ff-only
```

**To Set as Global Default (Recommended for Future Clarity):**

Choose one of these to set your preferred default behavior for `git pull`:

*   **Merge (recommended for simplicity):**

```bash
git config --global pull.rebase false
```

*   **Rebase (recommended for cleaner history, if comfortable with conflict resolution):**

```bash
git config --global pull.rebase true
```

*   **Fast-forward only:**

```bash
git config --global pull.ff only
```

## 13. Cloning a Specific Branch

Sometimes, you might want to clone a specific branch of a repository directly, rather than the default branch (usually `main` or `master`). This is particularly useful for projects that maintain different branches for active development and stable releases.

To clone a specific branch (e.g., `stable`):

```bash
git clone -b stable https://github.com/your-username/your-repo.git
```

The `-b` (or `--branch`) flag tells Git which branch to check out immediately after cloning. This avoids the need to manually switch branches after the initial clone.

**Why Use `-b stable`?**

Many projects use `main` or `master` for active development and `stable` for a more tested and production-ready version. Using `-b stable` ensures you get a reliable starting point for your work without having to manually switch branches after cloning.
