# Git → GitHub Workflow

A step-by-step summary of the standard Git workflow for getting a project onto GitHub, based on **"Git & GitHub Crash Course for Beginners [2026]"** (freeCodeCamp, Dec 2025). Each step lists the relevant Git commands.

---

## The Big Picture

Git tracks changes locally across three areas, and GitHub holds the remote copy:

```
Working Directory  →  Staging Area  →  Local Repository  →  Remote (GitHub)
   (your edits)        git add          git commit            git push
```

Pulling changes back down flows the other way: `git fetch` / `git pull`.

---

## Step 1 — Start a Repository

You either turn an existing folder into a repo, or copy an existing remote one.

```bash
# Initialize a brand-new local repository
git init

# OR clone an existing repository from GitHub
git clone https://github.com/user/repo.git
```

`git init` creates the hidden `.git` folder that turns a normal folder into a tracked repository. `git clone` downloads a full copy of a remote repo, including its history.

---

## Step 2 — Configure Your Identity

Git stamps every commit with a name and email. Set these once (globally) before committing.

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"

# Check what's currently set
git config --list
```

---

## Step 3 — Check What Changed

Before staging anything, see the current state of your working directory.

```bash
git status
```

Shows which files are untracked, modified, or already staged.

---

## Step 4 — Stage Changes

Move changes from the working directory into the staging area so they're ready to commit.

```bash
git add file.txt        # stage a specific file
git add .               # stage everything in the current directory
git add -A              # stage all changes (including deletions) repo-wide
```

If you staged something by mistake, unstage it:

```bash
git reset file.txt      # unstage a file (keeps your edits)
```

---

## Step 5 — Commit

Permanently save the staged snapshot to your local repository history.

```bash
git commit -m "Describe what you changed"
```

Undo the most recent commit if needed (keeps changes in your working directory):

```bash
git reset HEAD~1
```

---

## Step 6 — Manage & Remove Files

```bash
git rm file.txt          # delete a file and stage the deletion
git rm --cached file.txt # stop tracking a file but keep it on disk
```

`git rm --cached` is the typical move for files that should have been in `.gitignore`.

---

## Step 7 — Review History

```bash
git log                  # full commit history
git log --oneline        # compact, one line per commit
git diff                 # compare changes between commits / working state
```

---

## Step 8 — Branching

Branches let you work on features in isolation without touching the main line.

```bash
git branch feature       # create a branch
git checkout feature     # switch to it
git checkout -b feature   # create AND switch in one command
```

---

## Step 9 — Merge Branches

Bring a feature branch's work back into your main branch.

```bash
git checkout main        # switch to the receiving branch first
git merge feature        # merge the feature branch in
```

If Git can't auto-combine the changes, you'll get a **merge conflict**: edit the marked files manually, then stage and commit the resolution.

```bash
git add <resolved-files>
git commit
```

---

## Step 10 — Push to GitHub

Upload your local commits to the remote repository.

```bash
git push origin main
```

`origin` is the default name for the remote; `main` is the branch you're pushing.

---

## Step 11 — Pull Remote Changes

Keep your local copy in sync with what's on GitHub (important when collaborating).

```bash
git fetch       # download remote changes WITHOUT merging them
git pull        # download AND merge remote changes (fetch + merge)
```

Use `fetch` when you want to inspect changes first; use `pull` when you're ready to integrate them immediately.

---

## Useful "Undo & Rescue" Commands

These don't belong to one step but show up constantly in a real workflow.

```bash
git restore file.txt     # discard local (unstaged) changes to a file
git stash                # shelve unfinished work to come back to later
git stash pop            # reapply the most recently stashed work
git revert <commit>      # safely undo a commit by creating a new inverse commit
git rebase main          # replay your commits on top of another branch (cleaner history)
```

`git revert` is the safe way to undo a *pushed* commit (it doesn't rewrite history), whereas `git reset` and `git rebase` rewrite history and are best used on local, unshared work.

---

## Step 12 — Collaborate with Pull Requests

The team workflow on GitHub:

1. Push your feature branch to GitHub: `git push origin feature`
2. Open a **Pull Request (PR)** on GitHub to propose merging `feature` → `main`.
3. Teammates review, comment, and approve.
4. Merge the PR on GitHub.
5. Locally sync the merged result: `git checkout main && git pull`.

---

## Quick Reference Table

| Goal | Command |
|------|---------|
| Start a repo | `git init` / `git clone <url>` |
| Check status | `git status` |
| Stage changes | `git add .` |
| Unstage | `git reset <file>` |
| Save a snapshot | `git commit -m "msg"` |
| View history | `git log --oneline` |
| Compare changes | `git diff` |
| New branch | `git checkout -b <name>` |
| Merge | `git merge <branch>` |
| Upload to GitHub | `git push origin <branch>` |
| Download (no merge) | `git fetch` |
| Download + merge | `git pull` |
| Shelve work | `git stash` |
| Safely undo a commit | `git revert <commit>` |
| Clean up history | `git rebase <branch>` |

---

*Summary based on the chapter structure of the source video. Command flags and syntax follow standard Git usage.*
