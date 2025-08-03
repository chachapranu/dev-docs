# Git Common Commands

## Configuration

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
git config --list
```

## Repository Setup

```bash
git init                # Initialize a new repo
git clone <url>         # Clone a repo
```

## Basic Workflow

```bash
git status              # Show status
git add <file>          # Stage file(s)
git add .               # Stage all changes
git commit -m "Message" # Commit staged changes
git push                # Push to remote
git pull                # Pull latest changes
```

## Branching

```bash
git branch              # List branches
git branch <name>       # Create branch
git checkout <name>     # Switch branch
git checkout -b <name>  # Create and switch
git merge <branch>      # Merge branch
```

## Viewing History

```bash
git log                 # Commit history
git log --oneline       # Compact log
git diff                # Show unstaged changes
git diff --staged       # Show staged changes
```

## Undoing Changes

```bash
git restore <file>      # Discard changes in file
git reset HEAD <file>   # Unstage file
git checkout <commit>   # Checkout old commit
```

---

Add more commands as needed for your workflow!