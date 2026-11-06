# Team GitHub Progress Submission Guide

This guide explains how team members should submit their individual progress to a shared GitHub repository.

**Goal:** Each person works on their own branch, commits and pushes progress, and submits it through a Pull Request (PR). This keeps everyone's work isolated while still allowing the team to review and merge progress safely.

---

## 1. Prerequisites (One-Time Setup)

1. Install Git and configure your name and email:

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

2. Clone the repository:

```bash
git clone <repository-url>
cd <repository-directory>
```

3. Check the remote repository:

```bash
git remote -v
```

---

## 2. Before You Start Work: Sync the Latest Code

Do not start editing immediately. Always pull the latest changes from the main branch first.

```bash
git checkout main
git pull origin main
```

> If your main branch is named `master`, replace `main` with `master` in the commands below.

---

## 3. Create Your Own Progress Branch

Each person and each task should use a separate branch. Do not work directly on `main`.

```bash
git checkout -b progress/your-name-task-name
```

Example:

```bash
git checkout -b progress/zhangsan-login-page
```

Recommended branch naming patterns:

- `progress/zhangsan-login-page`
- `feature/lisi-data-api`
- `fix/wangwu-upload-bug`

---

## 4. Make Changes and Commit

### 4.1 Check what you changed

```bash
git status
```

### 4.2 Stage your changes

Stage all changes:

```bash
git add .
```

Stage specific files:

```bash
git add path/to/file
```

### 4.3 Commit your changes

```bash
git commit -m "Complete login page form validation"
```

Write clear commit messages, for example:

- `Complete login page form validation`
- `Add pagination API for user list`
- `Fix image upload failure`

Avoid unclear messages such as `update`, `fix`, or `111`.

---

## 5. Push to GitHub

First push for a new branch:

```bash
git push -u origin progress/your-name-task-name
```

Example:

```bash
git push -u origin progress/zhangsan-login-page
```

For later commits on the same branch:

```bash
git add .
git commit -m "Add login failure message"
git push
```

---

## 6. Open a Pull Request on GitHub

1. Open the repository page on GitHub.
2. After pushing, GitHub usually shows a **Compare & pull request** button. Click it.
3. Confirm:
   - **base**: `main`
   - **compare**: your progress branch, for example `progress/zhangsan-login-page`
4. Fill in the PR title and description.

Recommended PR description template:

```markdown
## Completed
- Completed login page layout
- Added form validation
- Added login failure message

## Not Yet Completed
- Forgot-password feature is not connected to the backend yet

## Reviewers
@team-lead
```

5. If the work is not finished but you want the team to see the progress, create a **Draft Pull Request**.
6. Click **Create pull request**.

---

## 7. Review and Merge

- Team members or the team lead will review the PR and leave comments.
- If changes are requested, continue working on the same local branch:

```bash
git add .
git commit -m "Adjust login validation based on review feedback"
git push
```

The PR will update automatically. You do not need to create a new PR.

- After approval, someone with write access can click **Merge pull request**.
- After merging, you can delete the remote branch:

```bash
git push origin --delete progress/your-name-task-name
```

Then switch back to the main branch and delete the local branch:

```bash
git checkout main
git pull origin main
git branch -d progress/your-name-task-name
```

---

## 8. If Your Branch Is Behind `main`

If someone else's PR was merged before yours, your branch may be behind. Before continuing work, merge the latest `main` into your branch:

```bash
git checkout main
git pull origin main
git checkout progress/your-name-task-name
git merge main
```

If there are conflicts:

1. Open the conflicted file and look for conflict markers:

```text
<<<<<<< HEAD
Your code
=======
Other people's code
>>>>>>> main
```

2. Keep the correct content and remove the conflict markers.
3. Then run:

```bash
git add .
git commit -m "Resolve conflicts with main"
git push
```

---

## 9. Fork Workflow (If You Do Not Have Write Access)

If you cannot push directly to the main repository, use the Fork workflow.

1. Click **Fork** on GitHub to copy the repository to your own account.
2. Clone your fork:

```bash
git clone <your-fork-url>
cd <repository-directory>
```

3. Add the upstream repository:

```bash
git remote add upstream <original-repository-url>
```

4. Before starting work, sync with the upstream repository:

```bash
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
```

5. Create a branch, make changes, commit, and push to your fork:

```bash
git checkout -b progress/your-name-task-name
git add .
git commit -m "Complete a specific task"
git push -u origin progress/your-name-task-name
```

6. Open a Pull Request from your fork to the original repository on GitHub.

---

## 10. Submission Checklist

Before submitting, confirm:

- [ ] I did not edit code directly on `main`
- [ ] My branch name clearly shows who I am and what I am working on
- [ ] My commit messages clearly describe what changed
- [ ] I did not commit passwords, keys, large files, or temporary files
- [ ] I synced the latest `main` before pushing
- [ ] My PR description explains what is completed and what is not
- [ ] The required reviewers have been mentioned with `@`

---

## 11. Quick Reference

```bash
# 1. Sync the main branch
git checkout main
git pull origin main

# 2. Create your own branch
git checkout -b progress/name-task

# 3. Make changes and commit
git add .
git commit -m "Complete a specific task"

# 4. Push your branch
git push -u origin progress/name-task

# 5. Open a Pull Request on GitHub
```

**Core principle:** Keep the main branch stable. Each person submits progress on their own branch and uses a Pull Request to bring that progress back to the main line.
