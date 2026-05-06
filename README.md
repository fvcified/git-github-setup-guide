# Git & GitHub Setup Guide
---
<br>

## 1️⃣ Create a repository on GitHub
- Go to **GitHub → New repository**
- Enter the repository name **same as your folder** (e.g., `my_repository`)
- **Do NOT** check README / .gitignore / License
- Copy the **repository URL**  
  Example: `https://github.com/<github_username>/<repository_name>.git`

## 2️⃣ Prepare your local folder
```bash
cd /path/to/your/folder
git init                  # Initialize git
git add .                 # Add all files
git commit -m "Initial commit"
```
⚠️ If the folder is empty → create a .gitkeep file
```bash
touch <folder_name>/.gitkeep
git add .
git commit -m "Upd!"
```

## 3️⃣ Connect to GitHub remote
```bash
git remote add origin https://github.com/<github_username>/<repository_name>.git
```
Check connection:
```bash
git remote -v
```

## 4️⃣ Rename local branch to main (GitHub default)
```bash
git branch -M main
```

## 5️⃣ Set upstream branch
```bash
git push -u origin main
```
```bash
git push
```

## 6️⃣ Embed credentials into remote URL (for auto-auth)
```bash
git clone https://github.com/<github_username>/<repository_name>.git
```
Open `.git/config` and update the remote URL:
<br>

```bash
url = https://<github_username>:<personal_access_token>@github.com/<github_username>/<repository_name>.git
```

<br>

## 7️⃣ Handle rejected push (remote has new commits)
If you see `rejected - fetch first` or `non-fast-forward`:
```bash
# Pull remote changes and rebase on top of local commits
git pull origin main --rebase
```
Then push:
```bash
git push origin main
```

## 8️⃣ Handle merge conflicts during rebase
If rebase stops with a conflict (e.g., in `README.md`):
```bash
# Keep your local version of the conflicted file
git checkout --ours <conflicted_file>
# Mark as resolved
git add <conflicted_file>
# Continue the rebase
git rebase --continue
```
If editor opens for commit message:
- **Vim** → type `:wq` then Enter
- **Nano** → press `Ctrl+X`

To abort the rebase entirely and go back to before:
```bash
git rebase --abort
```

## 9️⃣ Force push (last resort)
If history is completely out of sync and you want to overwrite remote with local:
```bash
git push origin main --force
```
⚠️ This overwrites everything on remote. Only use if you are the sole contributor or the repo is new.

## 🔟 Everyday workflow (after initial setup)
```bash
git add .
git commit -m "your commit message"
git push
```

##
If you ever see the message:
**`fatal: The upstream branch of your current branch does not match`**

Run this to link the local branch to the correct remote:
```bash
git branch --set-upstream-to=origin/main main
```

## 1️⃣1️⃣ Handle merge conflicts (non-rebase)
If `git pull` results in a conflict:
```bash
# See which files are conflicted
git status

# Option A — keep your local version
git checkout --ours <conflicted_file>

# Option B — keep remote version
git checkout --theirs <conflicted_file>

# Mark as resolved
git add <conflicted_file>
git commit -m "resolve merge conflict"
git push
```

## 1️⃣2️⃣ Undo last commit (keep changes)
```bash
git reset --soft HEAD~1
```

## 1️⃣3️⃣ Undo last commit (discard changes)
```bash
git reset --hard HEAD~1
```
⚠️ This permanently discards uncommitted changes.

## 1️⃣4️⃣ Check commit history
```bash
# Simple one-line log
git log --oneline

# Detailed log with graph
git log --oneline --graph --all

# Log with author and date
git log --pretty=format:"%h %an %ad %s" --date=short
```

## 1️⃣5️⃣ Stash changes temporarily
```bash
# Save current changes without committing
git stash

# List all stashes
git stash list

# Restore latest stash
git stash pop

# Restore specific stash
git stash apply stash@{0}

# Drop a stash
git stash drop stash@{0}

# Clear all stashes
git stash clear
```

## 1️⃣6️⃣ Branching
```bash
# Create a new branch
git branch <branch_name>

# Switch to a branch
git checkout <branch_name>

# Create and switch in one command
git checkout -b <branch_name>

# List all branches
git branch -a

# Delete a branch (local)
git branch -d <branch_name>

# Delete a branch (remote)
git push origin --delete <branch_name>

# Rename current branch
git branch -m <new_name>
```

## 1️⃣7️⃣ Merging branches
```bash
# Switch to target branch first
git checkout main

# Merge another branch into current
git merge <branch_name>

# Merge with a commit message (no fast-forward)
git merge --no-ff <branch_name> -m "merge: <branch_name> into main"

# Abort a merge in progress
git merge --abort
```

## 1️⃣8️⃣ Tagging
```bash
# Create a lightweight tag
git tag v1.0.0

# Create an annotated tag
git tag -a v1.0.0 -m "Release version 1.0.0"

# List all tags
git tag

# Push a tag to remote
git push origin v1.0.0

# Push all tags to remote
git push origin --tags

# Delete a tag (local)
git tag -d v1.0.0

# Delete a tag (remote)
git push origin --delete tag v1.0.0
```

## 1️⃣9️⃣ Diff & Inspect
```bash
# Show unstaged changes
git diff

# Show staged changes
git diff --staged

# Compare two branches
git diff main..<branch_name>

# Show changes in a specific commit
git show <commit_hash>

# Show who changed what in a file
git blame <file>
```

## 2️⃣0️⃣ Cherry-pick (apply a specific commit)
```bash
# Apply a specific commit from another branch
git cherry-pick <commit_hash>

# Cherry-pick without auto-committing
git cherry-pick <commit_hash> --no-commit

# Abort cherry-pick
git cherry-pick --abort
```

## 2️⃣1️⃣ Revert a commit (safe undo)
```bash
# Create a new commit that undoes a specific commit
git revert <commit_hash>

# Revert without auto-committing
git revert <commit_hash> --no-commit
```
Unlike `reset`, `revert` is safe for shared/remote branches because it does not rewrite history.

## 2️⃣2️⃣ Clean untracked files
```bash
# Preview what will be deleted
git clean -n

# Delete untracked files
git clean -f

# Delete untracked files and directories
git clean -fd

# Delete untracked + ignored files
git clean -fdx
```

## 2️⃣3️⃣ Submodules
```bash
# Add a submodule
git submodule add https://github.com/<user>/<repo>.git <path>

# Clone a repo with submodules
git clone --recurse-submodules https://github.com/<user>/<repo>.git

# Update all submodules
git submodule update --remote

# Remove a submodule
git submodule deinit <path>
git rm <path>
```

## 2️⃣4️⃣ Aliases (shortcuts)
```bash
# Set up useful aliases
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.lg "log --oneline --graph --all"

# Usage
git st
git co main
git br
git lg
```

## 2️⃣5️⃣ Global config setup
```bash
# Set your identity
git config --global user.name "Your Name"
git config --global user.email "you@example.com"

# Set default editor
git config --global core.editor "code --wait"   # VSCode
git config --global core.editor "vim"            # Vim
git config --global core.editor "nano"           # Nano

# Set default branch name
git config --global init.defaultBranch main

# View all config
git config --list
```

## 2️⃣6️⃣ .gitignore
```bash
# Create a .gitignore file
touch .gitignore
```
Common entries:
```
node_modules/
.env
.env.local
.DS_Store
dist/
build/
*.log
.next/
.vercel/
```
Force untrack a file already committed:
```bash
git rm --cached <file>
git add .
git commit -m "remove <file> from tracking"
```

## 2️⃣7️⃣ Fix detached HEAD state
```bash
# You are in detached HEAD — save your work first
git checkout -b <new_branch_name>

# Then merge back to main if needed
git checkout main
git merge <new_branch_name>
```

## 2️⃣8️⃣ Recover deleted branch
```bash
# Find the commit hash of the deleted branch
git reflog

# Recreate the branch from that commit
git checkout -b <branch_name> <commit_hash>
```

## 2️⃣9️⃣ Interactive rebase (rewrite history)
```bash
# Rebase last N commits interactively
git rebase -i HEAD~<N>
```
In the editor, you can:
- `pick` — keep the commit as is
- `reword` — edit the commit message
- `squash` — combine with previous commit
- `drop` — delete the commit

⚠️ Never interactive rebase commits that have already been pushed to a shared branch.

## 3️⃣0️⃣ Squash commits before pushing
```bash
# Squash last 3 commits into one
git reset --soft HEAD~3
git commit -m "your combined commit message"
git push origin main --force
```

##
<br>

## ⚠️ Notes
- The old `master` branch usually does not exist → no need to delete
- On Windows, you might see `credential-manager-core` warning → safe to ignore
- Git ignores empty folders → add `.gitkeep` to track the folder
- `--allow-unrelated-histories` flag is needed when local and remote have separate init commits
- `--ours` keeps your local file during conflict; `--theirs` keeps the remote version
- Never force push to a shared/production branch
- `git reset --soft` keeps your changes staged; `--hard` wipes them completely
- `git stash` is useful when you need to switch branches without committing
- `git revert` is safer than `git reset` on shared branches — it does not rewrite history
- Always `git pull` before starting new work to avoid conflicts
- Use `.gitignore` early — removing tracked files later requires `git rm --cached`
- `git reflog` is your safety net — almost nothing is truly lost in Git
