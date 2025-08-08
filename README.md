# HW2 - Git Troubleshooting Lab

Welcome to your Git Troubleshooting Lab. This document provides guidance on how to investigate and fix common issues in this intentionally broken Git repository.

## General Workflow

Before doing anything, always:

```zsh
git status
git log --oneline --graph --all
git reflog
```

These commands help you understand:
- Your current state (e.g., merge conflict, detached HEAD)
- Commit history and branches
- Detached commits and previous states

## Task 1: Recover a Deleted File

### Problem
`important_data.txt` has been deleted.

### What to Try
```bash
# Find the commit where the file existed
git log -- important_data.txt

# Restore it from an earlier commit
git checkout <commit-hash> -- important_data.txt

# OR, if you know the relative history
git restore --source=HEAD~3 important_data.txt
```

## Task 2: Resolve Merge Conflict

### Problem
You are mid-merge and `student_code.py` has conflicts.

### What to Try
```bash
# See the problem
git status

# Open the conflicted file and resolve the conflict
# Then stage the resolved file
git add student_code.py

# Commit the merge
git commit
```

## Task 3: Fix Detached HEAD

### Problem
Some commits were made in a detached HEAD state and are not on any branch.

### What to Try
```bash
# Inspect your reflog
git reflog

# Look for commits not on any branch
git branch dangling-commits <detached-commit-hash>

# Checkout or cherry-pick to rescue
git checkout main
git cherry-pick <detached-commit-hash>
```

## Task 4: Rewrite Bad Commit Messages

### Problem
Some commits say things like "WIP", "asdf", "temp".

### What to Try
```bash
# Reword the last few commits (if safe)
git rebase -i HEAD~5

# Change 'pick' to 'reword' for relevant commits
# Write better messages
```

## Task 5: Clean Up the Repo

### Problem
There are leftover branches and messy state.

### What to Try
```bash
# See all branches
git branch -a

# Delete unneeded branches
git branch -d feature-branch

# Final check
git status
git log --oneline --graph --all
```

## Pro Tips

- Commit often with clear messages
- Don’t panic. Git lets you recover most things
- Ask for help if you're stuck!

---

## Deliverables

You’ll need to write a report explaining:
- What you found
- What you fixed
- What you learned

Take screenshots or copy terminal output to show your process.
