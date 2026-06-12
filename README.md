# Git & GitHub Setup Guide

---

## 1️⃣ Create a repository on GitHub

* Go to **GitHub → New repository**
* Enter the repository name **same as your folder** (e.g., `my_repository`)
* **Do NOT** check README / .gitignore / License
* Copy the repository URL

Example:

```bash
https://github.com/<github_username>/<repository_name>.git
```

---

## 2️⃣ Prepare your local folder

```bash
cd /path/to/your/folder

git init
git add .
git commit -m "Initial commit"
```

If the folder is empty:

```bash
touch .gitkeep
git add .
git commit -m "Initial commit"
```

---

## 3️⃣ Connect to GitHub remote

```bash
git remote add origin https://github.com/<github_username>/<repository_name>.git
```

Verify:

```bash
git remote -v
```

Show detailed remote information:

```bash
git remote show origin
```

---

## 4️⃣ Rename local branch to main

```bash
git branch -M main
```

---

## 5️⃣ Set upstream branch

```bash
git push -u origin main
```

After first push:

```bash
git push
```

---

## 6️⃣ Authentication (Recommended)

Windows:

```bash
git config --global credential.helper manager
```

GitHub CLI:

```bash
gh auth login
```

Verify login:

```bash
gh auth status
```

---

## 7️⃣ Clone an existing repository

```bash
git clone https://github.com/<user>/<repo>.git

cd <repo>
```

Clone a specific branch:

```bash
git clone -b <branch_name> https://github.com/<user>/<repo>.git
```

---

## 8️⃣ Handle rejected push

If you see:

```text
rejected - fetch first
non-fast-forward
```

Run:

```bash
git pull origin main --rebase
```

Then:

```bash
git push origin main
```

---

## 9️⃣ Handle merge conflicts during rebase

Keep your version:

```bash
git checkout --ours <file>
git add <file>
git rebase --continue
```

Keep remote version:

```bash
git checkout --theirs <file>
git add <file>
git rebase --continue
```

Abort rebase:

```bash
git rebase --abort
```

Editor shortcuts:

Vim:

```text
:wq
```

Nano:

```text
Ctrl+X
```

---

## 🔟 Force push (last resort)

Safer:

```bash
git push origin main --force-with-lease
```

Dangerous:

```bash
git push origin main --force
```

Only use when necessary.

---

## 1️⃣1️⃣ Everyday workflow

```bash
git add .
git commit -m "your message"
git push
```

---

## 1️⃣2️⃣ Upstream branch mismatch

If you see:

```text
fatal: The upstream branch of your current branch does not match
```

Run:

```bash
git branch --set-upstream-to=origin/main main
```

---

## 1️⃣3️⃣ Fetch without merge

Fetch latest changes:

```bash
git fetch origin
```

Fetch all remotes:

```bash
git fetch --all
```

Difference:

```bash
git fetch
```

Downloads changes only.

```bash
git pull
```

Downloads + merges/rebases.

---

## 1️⃣4️⃣ Update branch with latest main

Using rebase:

```bash
git checkout <branch_name>

git fetch origin

git rebase origin/main
```

Using merge:

```bash
git checkout <branch_name>

git fetch origin

git merge origin/main
```

---

## 1️⃣5️⃣ Pull Request workflow

```bash
git checkout -b feature-name

git add .

git commit -m "feat: description"

git push -u origin feature-name
```

Then:

1. Open GitHub
2. Click **Compare & Pull Request**
3. Create Pull Request
4. Wait for review

---

## 1️⃣6️⃣ Amend commit

Change last commit message:

```bash
git commit --amend -m "new message"
```

Add forgotten files:

```bash
git add .

git commit --amend --no-edit
```

---

## 1️⃣7️⃣ Handle merge conflicts (non-rebase)

Check conflicts:

```bash
git status
```

Keep local version:

```bash
git checkout --ours <file>
```

Keep remote version:

```bash
git checkout --theirs <file>
```

Resolve:

```bash
git add <file>

git commit -m "resolve merge conflict"

git push
```

---

## 1️⃣8️⃣ Undo last commit (keep changes)

```bash
git reset --soft HEAD~1
```

---

## 1️⃣9️⃣ Undo last commit (discard changes)

```bash
git reset --hard HEAD~1
```

---

## 2️⃣0️⃣ Restore & unstage

Discard file changes:

```bash
git restore <file>
```

Discard all unstaged changes:

```bash
git restore .
```

Unstage file:

```bash
git restore --staged <file>
```

Legacy:

```bash
git reset HEAD <file>
```

---

## 2️⃣1️⃣ Check commit history

```bash
git log --oneline
```

```bash
git log --oneline --graph --all
```

```bash
git log --pretty=format:"%h %an %ad %s" --date=short
```

---

## 2️⃣2️⃣ Stash changes

```bash
git stash
```

```bash
git stash list
```

```bash
git stash pop
```

```bash
git stash apply stash@{0}
```

```bash
git stash drop stash@{0}
```

```bash
git stash clear
```

---

## 2️⃣3️⃣ Branching

Create:

```bash
git branch <branch_name>
```

Switch:

```bash
git checkout <branch_name>
```

Modern:

```bash
git switch <branch_name>
```

Create and switch:

```bash
git checkout -b <branch_name>
```

Modern:

```bash
git switch -c <branch_name>
```

List:

```bash
git branch -a
```

Delete local:

```bash
git branch -d <branch_name>
```

Force delete:

```bash
git branch -D <branch_name>
```

Delete remote:

```bash
git push origin --delete <branch_name>
```

Rename:

```bash
git branch -m <new_name>
```

---

## 2️⃣4️⃣ Merging branches

```bash
git checkout main
```

```bash
git merge <branch_name>
```

```bash
git merge --no-ff <branch_name> -m "merge: <branch_name> into main"
```

Abort:

```bash
git merge --abort
```

---

## 2️⃣5️⃣ Tagging

```bash
git tag v1.0.0
```

```bash
git tag -a v1.0.0 -m "Release version 1.0.0"
```

```bash
git tag
```

```bash
git push origin v1.0.0
```

```bash
git push origin --tags
```

```bash
git tag -d v1.0.0
```

```bash
git push origin --delete tag v1.0.0
```

---

## 2️⃣6️⃣ Diff & inspect

```bash
git diff
```

```bash
git diff --staged
```

```bash
git diff main..<branch_name>
```

```bash
git show <commit_hash>
```

```bash
git blame <file>
```

---

## 2️⃣7️⃣ Cherry-pick

```bash
git cherry-pick <commit_hash>
```

```bash
git cherry-pick <commit_hash> --no-commit
```

Abort:

```bash
git cherry-pick --abort
```

---

## 2️⃣8️⃣ Revert

```bash
git revert <commit_hash>
```

```bash
git revert <commit_hash> --no-commit
```

---

## 2️⃣9️⃣ Clean untracked files

Preview:

```bash
git clean -n
```

Delete files:

```bash
git clean -f
```

Delete files + folders:

```bash
git clean -fd
```

Delete everything:

```bash
git clean -fdx
```

---

## 3️⃣0️⃣ Submodules

```bash
git submodule add https://github.com/<user>/<repo>.git <path>
```

```bash
git clone --recurse-submodules https://github.com/<user>/<repo>.git
```

```bash
git submodule update --remote
```

Remove:

```bash
git submodule deinit <path>

git rm <path>
```

---

## 3️⃣1️⃣ Aliases

```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.lg "log --oneline --graph --all"
```

Usage:

```bash
git st
git co main
git br
git lg
```

---

## 3️⃣2️⃣ Global config

```bash
git config --global user.name "Your Name"
```

```bash
git config --global user.email "you@example.com"
```

VSCode:

```bash
git config --global core.editor "code --wait"
```

Vim:

```bash
git config --global core.editor "vim"
```

Nano:

```bash
git config --global core.editor "nano"
```

Default branch:

```bash
git config --global init.defaultBranch main
```

View config:

```bash
git config --list
```

---

## 3️⃣3️⃣ .gitignore

Create:

```bash
touch .gitignore
```

Common entries:

```gitignore
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

Stop tracking a file:

```bash
git rm --cached <file>

git add .

git commit -m "remove file from tracking"
```

---

## 3️⃣4️⃣ Fix detached HEAD

```bash
git checkout -b <new_branch_name>
```

Then:

```bash
git checkout main

git merge <new_branch_name>
```

---

## 3️⃣5️⃣ Recover deleted branch

```bash
git reflog
```

```bash
git checkout -b <branch_name> <commit_hash>
```

---

## 3️⃣6️⃣ Interactive rebase

```bash
git rebase -i HEAD~<N>
```

Commands:

* pick
* reword
* squash
* drop

Never rewrite shared branch history.

---

## 3️⃣7️⃣ Squash commits

```bash
git reset --soft HEAD~3

git commit -m "combined commit"

git push origin main --force-with-lease
```

---

## ⚠️ Notes

* Git ignores empty folders → use `.gitkeep`
* `git fetch` does not merge
* `git pull` = fetch + merge/rebase
* `git revert` is safer than `git reset`
* `git reflog` can recover most mistakes
* Prefer `--force-with-lease` over `--force`
* Use `.gitignore` early
* Never force push to shared production branches
* Always pull or fetch before major work
* `--ours` keeps local changes
* `--theirs` keeps incoming changes
* Detached HEAD is not dangerous if you create a branch before leaving it
