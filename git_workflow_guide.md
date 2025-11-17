# Git Workflow Guide (Personal & Professional Use)

This guide summarizes a clean and consistent Git workflow suitable for both solo projects and team collaboration. It includes naming conventions, commit structure, and key commands.

## Table of Contents

- [1. Start a New Feature or Task](#1-start-a-new-feature-or-task-top-)
  - [Branch naming convention](#branch-naming-convention)
- [2. Make Small, Thematic Commits](#2-make-small-thematic-commits-top-)
  - [Commit message format](#commit-message-format)
- [3. Rewriting History with git rebase -i (before pushing)](#3-rewriting-history-with-git-rebase--i-before-pushing-top-)
  - [Useful actions](#useful-actions)
  - [Tip](#tip)
- [4. Check Your Commit History](#4-check-your-commit-history-top-)
  - [Stay Updated When Working in Teams](#stay-updated-when-working-in-teams)
- [5. Merge Feature Branch into Main](#5-merge-feature-branch-into-main-top-)
- [6. Clean Up](#6-clean-up-top-)
- [7. Push to GitHub](#7-push-to-github-top-)
  - [7.1 Safe force push after rebase](#71-safe-force-push-after-rebase)
- [8. Versioning with Git Tags (Optional)](#8-versioning-with-git-tags-optional-top-)
  - [How to create a tag](#how-to-create-a-tag)
  - [Tips](#tips)
- [Extras (Optional but Recommended)](#extras-optional-but-recommended-top-)
- [Summary Cheat Sheet](#summary-cheat-sheet-top-)
  - [Alternative flow with develop branch (team projects, GitFlow-like)](#alternative-flow-with-develop-branch-team-projects-gitflow-like)
  - ⭐️ [Alternative flow with Pull Requests & Protected Branches (professional workflow))](#alternative-flow-with-pull-requests--protected-branches-professional-workflow-top-)


## 1. Start a New Feature or Task [top ↑](#)

Always create a new branch from `main` for each feature or fix:

```bash
git checkout -b feat/feature-name
```

### Branch naming convention:

- `feat/...` → new features
- `fix/...` → bug fixes
- `refactor/...` → code restructuring
- `style/...` → styling changes (CSS, Bootstrap, etc.)
- `docs/...` → documentation
- `test/...` → tests
- `chore/...` → config or setup (no functional change)

Use **kebab-case** (dashes) for readability: `feat/add-navbar`, `fix/form-validation`

[Git branch naming best practices](https://www.conventionalcommits.org/en/v1.0.0/#summary)


## 2. Make Small, Thematic Commits [top ↑](#)

Use `git add -p` to stage code **by logical chunks**:

```bash
git add -p
```

Then commit with a clear, structured message:

```bash
git commit -m "<type>(<scope>): message"
```

### Commit message format:

```
feat(view): apply Bootstrap to new form
```

- `<type>` → like `feat`, `fix`, `refactor`...
- `<scope>` → what part of the app changed (`views`, `layout`, `navbar`, etc.)
- `message` → clear and concise action


## 3. Rewriting History with git rebase -i (before pushing) [top ↑](#)

If you made several small or messy commits (typos, debug logs, quick fixes), you can clean them up before pushing with:

```
git rebase -i HEAD~N
```

Replace N with the number of recent commits you want to review.

### Useful actions:
- pick → keep the commit as is
- reword → edit the commit message
- squash → combine with the previous commit
- drop → delete the commit entirely

### Tip:
Combine small commits into a single clear, meaningful one.
Final example:

```
feat(navbar): add responsive navbar with custom colors
```

## 4. Check Your Commit History [top ↑](#)

To visualize your commits:

```bash
git log --oneline --graph --decorate
```

This helps you ensure commits are clean and in order.

### Stay Updated When Working in Teams
Before merging or pushing to a shared branch (like main), always make sure your local copy is up to date:

```bash
git fetch origin
git checkout main
git pull origin main
```

This helps you avoid conflicts and keeps your work in sync with others.


## 5. Merge Feature Branch into Main [top ↑](#)

Once your task is done:

```bash
git checkout main

git merge feat/feature-name
```

This keeps your `main` branch up-to-date and your history intact.

**Avoid rebasing** public/shared branches.

[Git merge docs](https://git-scm.com/docs/git-merge)


## 6. Clean Up [top ↑](#)

After merging:

```bash
git branch -d feat/feature-name
```

Deletes the branch locally (safe after merge).


## 7. Push to GitHub [top ↑](#)

Push your updated `main` branch:

```bash
git push origin main
```

And push any new branches as needed:

```bash
git push -u origin feat/feature-name
```

### 7.1 Safe force push after rebase

If you used an interactive rebase, your commit history has changed, so the next push must update the remote forcefully:

```bash
git push --force-with-lease
```

This is safer than --force because it only overwrites the remote if nobody else has updated it since your last fetch.

Use it only on private branches or solo work, and never on shared branches without coordination.


[Git push docs](https://git-scm.com/docs/git-push)


## 8. Versioning with Git Tags (Optional) [top ↑](#)
You can use Git tags to mark important points in your project history, such as stable releases or deployment versions.

### How to create a tag
First, make sure you're on the correct branch (usually main) and that you've already committed the changes you want to tag:

```bash
git checkout main
git pull origin main
```
Then, create an annotated tag with a message:

```
git tag -a v1.0.0 -m "First stable release"
```
Push the tag to the remote repository:

```
git push origin v1.0.0
```
To push all tags:

```
git push --tags
```

### Tips
- Use Semantic Versioning: v1.0.0, v1.1.0, v2.0.0, etc.
- Tags are useful for deployments, releases, or rollback points
- Use annotated tags (-a) rather than lightweight tags for better metadata

[Git Tag Docs](https://git-scm.com/book/en/v2/Git-Basics-Tagging)


## Extras (Optional but Recommended) [top ↑](#)

- Use `.gitignore` to exclude environment files, `node_modules`, etc.
- Create a `docs/` folder for project documentation
- Use `README.md` to describe the project purpose, setup and usage
- Use `rebase -i` to squash or edit commits **before pushing**

[Git rebase interactive](https://git-scm.com/docs/git-rebase#_interactive_mode)


## Summary Cheat Sheet [top ↑](#)

```bash
# Create feature branch
git checkout -b feat/some-feature

# Make changes, stage parts
git add -p

# Commit with Conventional Commit format
git commit -m "feat(scope): message"

# (Optional) Clean up commit history
git rebase -i HEAD~N

# Merge feature into main
git checkout main
git pull origin main
git merge feat/some-feature

# Delete feature branch
git branch -d feat/some-feature

# Push to GitHub
git push origin main

# If you rebased: force push safely
git push --force-with-lease

# Tag a new version (semantic versioning)
git tag -a v1.0.0 -m "First stable release"
git push origin v1.0.0

```

### Alternative flow with `develop` branch (team projects, GitFlow-like) 
```
# Start from develop (not main)
git checkout develop
git pull origin develop

# Create feature branch from develop
git checkout -b feat/some-feature

# Make and stage changes
git add -p

# Commit with Conventional Commit format
git commit -m "feat(scope): message"

# (Optional) Rebase to clean history
git rebase -i HEAD~N

# Merge back into develop
git checkout develop
git pull origin develop
git merge feat/some-feature

# Delete feature branch
git branch -d feat/some-feature

# Push develop to GitHub
git push origin develop

# If you rebased: force push safely
git push --force-with-lease

# When ready to release, merge develop into main
git checkout main
git pull origin main
git merge develop

# Tag and push new version
git tag -a v1.1.0 -m "Release: feature X completed"
git push origin main
git push origin v1.1.0
```

---

## Alternative flow with Pull Requests & Protected Branches (professional workflow) [top ↑](#)

In collaborative or production-like environments, branches such as `main` and `develop` are often protected, meaning you cannot push to them directly.
All changes must go through Pull Requests (PRs) to ensure review, CI checks, and a clean commit history.

### Branch workflow (professional protected-branch setup)
```bash
# Always start from an up-to-date develop
git checkout develop
git pull --rebase origin develop

# Create your feature branch
git checkout -b feat/some-feature
```

> Using --rebase avoids unnecessary merge commits and keeps the history linear and easier to read during code review.

Work on your feature:
```bash
git add -p
git commit -m "feat(scope): implement X"
```

Keep your branch updated while working:
```bash
# Fetch new changes from develop
git fetch origin

# Reapply your work on top of the latest develop
git rebase origin/develop
```

(Optional) Rebase to clean history:
```bash
git rebase -i HEAD~N
```

If you rebased, update your branch safely:
```bash
git push --force-with-lease
```

> --force-with-lease is safer than --force — it only pushes if no one else has updated the branch since your last pull, protecting shared work.

### Opening the Pull Request

- Open a PR targeting `develop` (not main).
- Use clear, conventional-commit titles:
  - feat(api): add new stock endpoint
  - fix(auth): correct login cookie
  - docs(contributing): update PR workflow
- Keep PRs focused and small.
- Resolve all comments before merging.
- Use Squash & Merge to keep history clean.

### After the PR is merged
```bash
# Update local develop
git checkout develop
git pull origin develop

# Delete local branch
git branch -d feat/some-feature

# Delete remote branch
git push origin --delete feat/some-feature
```

### Release workflow (protected main branch)
```bash
# Update local develop
git checkout develop
git pull origin develop

# Create a release branch
git checkout -b release/v1.2.0
git push origin release/v1.2.0

# Open a PR → main

# After merging:
git checkout main
git pull origin main

# Tag release
git tag -a v1.2.0 -m "Release: version 1.2.0"
git push origin v1.2.0
```
