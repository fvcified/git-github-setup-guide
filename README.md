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
If rebase stops with a conflict (e.g., in `.env.example`):
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

##
<br>

## ⚠️ Notes
- The old master branch usually does not exist → no need to delete
- On Windows, you might see `credential-manager-core` warning → safe to ignore
- Git ignores empty folders → add `.gitkeep` to track the folder
- `--allow-unrelated-histories` flag is needed when local and remote have separate init commits
- `--ours` keeps your local file during conflict; `--theirs` keeps the remote version
- Never force push to a shared/production branch
