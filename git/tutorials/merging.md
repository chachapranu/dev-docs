# Choosing a Git Merge Strategy

## Merge Commit

**When to use:**  
- You want to preserve the full branch history.
- Useful for feature branches and team collaboration.
- Good for tracking when and how branches were integrated.

**Example:**
```bash
git merge feature-branch
```
This creates a merge commit, keeping all individual commits from the feature branch.

---

## Squash Merge

**When to use:**  
- You want a clean, linear history.
- Combine many small or "work in progress" commits into one.
- Ideal for merging finished features or bugfixes.

**Example:**
```bash
git merge --squash feature-branch
git commit -m "Add feature"
```
This squashes all changes into a single commit.

---

## Rebase

**When to use:**  
- You want to replay your changes on top of the latest main branch.
- Useful for keeping a linear history and avoiding merge commits.
- Great for updating a feature branch before merging.

**Example:**
```bash
git checkout feature-branch
git rebase main
```
This moves your feature branch commits on top of the latest main branch.

---

**Summary Table**

| Strategy       | Preserves History | Linear History | Use Case                        |
|----------------|------------------|---------------|---------------------------------|
| Merge Commit   | Yes              | No            | Team work, full history         |
| Squash Merge   | No               | Yes           | Clean up, single feature commit |
| Rebase         | No (rewrites)    | Yes           | Update branch, avoid merges     |

Choose the strategy that fits your workflow and project needs.