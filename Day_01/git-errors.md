# Git Errors Encountered - Day 1

## Introduction

While learning Git, it's completely normal to encounter errors. Every Git error teaches an important concept about how Git works.

This document contains all the Git errors I encountered on Day 1, along with their causes, solutions, and the lessons learned.

---

# Error 1

## Error Message

```bash
fatal: not a git repository (or any of the parent directories): .git
```

## Why did this happen?

Git commands such as:

```bash
git status
git add
git commit
git push
```

only work inside a Git repository.

A Git repository is a folder that contains a hidden directory named:

```text
.git
```

If Git cannot find this hidden folder, it displays the error:

```bash
fatal: not a git repository
```

---

## Example

Current Directory

```text
Documents/
│
├── DevOps_90Days/
└── Notes/
```

If I run:

```bash
git status
```

inside **Documents**, Git cannot find a repository.

---

## Solution

Move into the project folder first.

```bash
cd DevOps_90Days
```

Then verify:

```bash
pwd
```

Initialize Git if it has never been initialized.

```bash
git init
```

---

## Lesson Learned

Always run Git commands inside your project directory.

---

# Error 2

## Error Message

```bash
git add
```

Output

```bash
Nothing specified, nothing added.
Maybe you wanted to say 'git add .'
```

---

## Why did this happen?

The command

```bash
git add
```

does not specify what should be added.

Git needs to know which file or folder should be staged.

---

## Wrong

```bash
git add
```

---

## Correct

Stage everything

```bash
git add .
```

Stage a single file

```bash
git add README.md
```

Stage one folder

```bash
git add Day_01/
```

---

## Lesson Learned

Always specify the files you want Git to stage.

---

# Error 3

## Error Message

```bash
nothing added to commit but untracked files present
```

---

## Why did this happen?

Git saw new files but they were not added to the staging area.

Workflow

```text
Working Directory

↓

git add

↓

Staging Area

↓

git commit
```

The commit was attempted before staging.

---

## Solution

```bash
git add .
git commit -m "Day 1"
```

---

## Lesson Learned

Git can only commit staged files.

---

# Error 4

## Error Message

```bash
Repository not found.
fatal: repository not found
```

---

## Why did this happen?

Possible reasons

- Wrong GitHub URL
- Repository does not exist
- Typo in repository name
- Repository belongs to another account

---

## Solution

Verify the repository exists.

Check remote URL.

```bash
git remote -v
```

Update remote.

```bash
git remote set-url origin https://github.com/username/repository.git
```

---

## Lesson Learned

Always verify the repository URL before pushing.

---

# Error 5

## Error Message

```bash
Updates were rejected because the remote contains work that you do not have locally.
```

or

```bash
! [rejected] main -> main (fetch first)
```

---

## Why did this happen?

GitHub already had a commit.

Example

- README created on GitHub
- Local repository created separately

Now both repositories have different histories.

Git refuses to overwrite history automatically.

---

## Solution

Option 1 (Recommended)

```bash
git pull origin main --allow-unrelated-histories
```

Resolve merge if necessary.

Then

```bash
git push origin main
```

Option 2 (Only for brand new repositories)

```bash
git push --force
```

Never use force push in production unless you understand the consequences.

---

## Lesson Learned

Always pull the latest changes before pushing if the remote repository already contains commits.

---

# Error 6

## Problem

Git repository initialized in the wrong location.

Example

```bash
git init
```

inside

```text
C:\Users\hp
```

instead of

```text
C:\Users\hp\Documents\DevOps_90Days
```

---

## Why is this bad?

Git starts tracking your entire Home directory.

Git status shows

- Downloads
- Documents
- Pictures
- Videos
- OneDrive

and many other files.

---

## Correct Practice

One Project = One Git Repository

Always

```bash
cd ProjectFolder
git init
```

---

## Lesson Learned

Never initialize Git in your Home directory.

---

# Error 7

## Error Message

```bash
git remote -v
```

Output

Nothing

---

## Why did this happen?

The local repository was never connected to GitHub.

No remote repository existed.

---

## Solution

Add the remote.

```bash
git remote add origin https://github.com/username/DevOps-90days.git
```

Verify

```bash
git remote -v
```

Expected Output

```text
origin https://github.com/username/DevOps-90days.git (fetch)

origin https://github.com/username/DevOps-90days.git (push)
```

---

## Lesson Learned

Git and GitHub are different.

Git is local.

GitHub is remote.

You must connect them using

```bash
git remote add origin
```

---

# Git Workflow Learned Today

```text
Create Files
      │
      ▼
git status
      │
      ▼
git add .
      │
      ▼
git commit -m "Message"
      │
      ▼
git push
      │
      ▼
GitHub
```

---

# Important Git Commands Learned

| Command | Description |
|----------|-------------|
| git init | Initialize a Git repository |
| git status | Check repository status |
| git add . | Stage all files |
| git commit -m | Save changes locally |
| git log --oneline | View commit history |
| git remote -v | Show remote repository |
| git remote add origin | Connect to GitHub |
| git push | Upload commits to GitHub |
| git pull | Download latest changes |
| git branch -M main | Rename branch to main |

---

# Key Takeaways

- Git tracks changes locally.
- GitHub stores your project online.
- Always work inside your project folder.
- Stage files before committing.
- Commit before pushing.
- Pull before pushing if the remote repository has new commits.
- One project should have one Git repository.
- Read Git error messages carefully—they usually tell you exactly what went wrong.

---

# My Day 1 Learning Summary

Today I learned:

- How Git repositories work.
- Difference between Local Repository and GitHub Repository.
- How to initialize Git.
- How to stage files.
- How to commit changes.
- How to connect GitHub.
- How to push code.
- How to troubleshoot common Git errors.

Every error I encountered helped me understand Git better and made me more confident using version control.
