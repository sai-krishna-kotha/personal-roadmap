# Git — Infosys SP L1 Pre-Test

[← Back to Pre-Test Roadmap](./README.md)

## Table of Contents

- [How to use this file](#how-to-use-this-file)
- [1. Git model and terminology](#1-git-model-and-terminology)
- [2. Setup and configuration](#2-setup-and-configuration)
- [3. Repository creation and cloning](#3-repository-creation-and-cloning)
- [4. Working tree, staging and commits](#4-working-tree-staging-and-commits)
- [5. Inspecting history and differences](#5-inspecting-history-and-differences)
- [6. Branches and HEAD](#6-branches-and-head)
- [7. Merge and conflicts](#7-merge-and-conflicts)
- [8. Remotes, fetch, pull and push](#8-remotes-fetch-pull-and-push)
- [9. Reset, revert, restore and reflog](#9-reset-revert-restore-and-reflog)
- [10. Ignore rules, tags and stashing](#10-ignore-rules-tags-and-stashing)
- [11. Typical workflows](#11-typical-workflows)
- [12. High-yield Git traps](#12-high-yield-git-traps)
- [13. Practice MCQs](#13-practice-mcqs)
- [14. Study schedule and checklist](#14-study-schedule-and-checklist)
- [References](#references)

## How to use this file

Use a throwaway local repository to practise commands. Always inspect `git status` before a potentially destructive operation. These notes are technical preparation, not a claim about the exact Infosys assessment questions.

## 1. Git model and terminology

Git is a distributed version-control system. A repository stores commit history and related objects. Understand these areas:

- **Working tree:** files you currently see and edit.
- **Index/staging area:** proposed content for the next commit.
- **Local repository:** committed history in your clone.
- **Remote:** a named reference to another repository, often called `origin`.
- **Commit:** a snapshot with metadata and parent commit(s).
- **Branch:** a movable reference to a commit.
- **HEAD:** usually identifies the currently checked-out branch/commit.

A useful mental model is: edit files → stage selected changes → commit staged content → push commits when ready to share.

[↑ Back to TOC](#table-of-contents)

## 2. Setup and configuration

Common configuration:
```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --list
```

Configuration can be scoped to a repository, a user, or the system. A commit records an author and committer identity; setting an email does not authenticate you to a hosting provider.

Useful checks:
- `git --version`
- `git status`
- `git config --show-origin --get user.name`

[↑ Back to TOC](#table-of-contents)

## 3. Repository creation and cloning

- `git init`: initialize a repository in the current directory.
- `git clone URL`: create a local copy of a remote repository and usually set up a remote named `origin`.
- `git remote -v`: list remote URLs.
- `git remote add origin URL`: add a remote called origin.

Cloning normally downloads commit history and checks out a working tree. Initializing a repository does not automatically connect it to GitHub or another remote host.

[↑ Back to TOC](#table-of-contents)

## 4. Working tree, staging and commits

Core commands:
- `git status`: summarize working-tree and staging state.
- `git add file`: stage the current content of a path.
- `git add -p`: interactively stage parts of changes.
- `git diff`: compare working-tree changes against the index.
- `git diff --staged`: compare staged changes against the current commit.
- `git commit -m "message"`: record the staged snapshot.
- `git commit -am "message"`: stage modifications/deletions of already tracked files and commit; it does not add untracked files.

A commit captures staged content, not every change in the working directory. If a file is edited again after `git add`, the later edit is not automatically staged.

[↑ Back to TOC](#table-of-contents)

## 5. Inspecting history and differences

- `git log --oneline --graph --decorate --all`: compact, visual history.
- `git show COMMIT`: inspect a commit and its changes.
- `git diff A B`: compare two trees/revisions.
- `git blame file`: show the commit/author associated with lines in a file.
- `git status --short`: compact working-tree status.

A commit hash identifies a Git object. Parent links form history; ordinary commits generally have one parent, while merge commits have multiple parents. The exact display depends on command options and repository state.

[↑ Back to TOC](#table-of-contents)

## 6. Branches and HEAD

A branch is a movable name pointing to a commit, not a separate copy of all files.

- `git branch`: list local branches.
- `git switch -c feature`: create and switch to a branch.
- `git switch main`: switch branches.
- `git branch -d feature`: delete a merged branch when Git permits.
- `git log --oneline --all --decorate --graph`: inspect branches and history.

Detached HEAD means HEAD points directly to a commit rather than to a local branch. Commits made in detached HEAD are possible, but may become hard to find unless you create a branch or another reference.

[↑ Back to TOC](#table-of-contents)

## 7. Merge and conflicts

`git merge feature` integrates the named branch into the current branch. It may fast-forward, create a merge commit, or stop for conflicts, depending on history and options.

When a merge conflict occurs:

1. Run `git status` to identify conflicted paths.
2. Open and resolve conflict markers in each file.
3. Test the result.
4. Stage resolved paths with `git add`.
5. Complete the merge with `git commit` if Git has not already done so.

Conflict markers such as `<<<<<<<`, `=======`, and `>>>>>>>` are placeholders for competing changes. Do not leave them in final code.

[↑ Back to TOC](#table-of-contents)

## 8. Remotes, fetch, pull and push

- `git fetch origin`: retrieve remote refs/objects and update remote-tracking references; it does not by itself integrate them into your current branch.
- `git pull`: fetch and then integrate updates, commonly by merge or rebase depending on configuration/options.
- `git push origin branch`: publish local commits to a remote branch, subject to permissions and server rules.
- `git branch -vv`: show local branches and upstream information.
- `git remote show origin`: inspect remote-tracking details.

Remote-tracking names such as `origin/main` describe the last known remote state locally. They can become stale until you fetch again. A push can be rejected if it is not a fast-forward or is blocked by remote policy.

[↑ Back to TOC](#table-of-contents)

## 9. Reset, revert, restore and reflog

These commands differ in what they change:

- `git restore file`: restore working-tree content from a source (defaulting to the index for an unstaged path); can discard local edits.
- `git restore --staged file`: unstage a path while generally keeping its working-tree edits.
- `git reset --soft HEAD~1`: move current branch/HEAD back one commit while keeping changes staged.
- `git reset --mixed HEAD~1`: move branch/HEAD and reset the index; working-tree changes remain (mixed is the default mode).
- `git reset --hard HEAD~1`: reset branch, index and working tree; potentially destroys uncommitted changes.
- `git revert COMMIT`: create a new commit that reverses the selected commit's changes.
- `git reflog`: inspect recent movements of local references, useful for recovering commits that are no longer visible in current branch history.

Rule of thumb: `revert` records an inverse change and is often safer for shared history. `reset` moves a reference and can rewrite local history. Understand the precise target before running either.

[↑ Back to TOC](#table-of-contents)

## 10. Ignore rules, tags and stashing

- `.gitignore`: lists untracked paths Git should normally ignore; it does not automatically untrack files already committed.
- `git rm --cached file`: remove a path from the index while leaving the local file.
- `git stash`: save certain working-tree and index changes for later; include untracked files with appropriate options such as `-u`.
- `git stash list`, `git stash apply`, `git stash pop`: inspect and reapply saved changes.
- `git tag v1.0.0`: create a lightweight tag; annotated tags can record tag metadata.
- `git tag`: list tags.

A stash is not a replacement for a meaningful commit. A `.gitignore` rule does not remove a secret that was already committed; if credentials leaked, revoke/rotate them and follow repository cleanup guidance.

[↑ Back to TOC](#table-of-contents)

## 11. Typical workflows

### Start a feature
```bash
git switch main
git pull
git switch -c feature/search
# edit files
git status
git add .
git diff --staged
git commit -m "Add search feature"
```

### Inspect before sharing
```bash
git status
git log --oneline --decorate -5
git diff
git diff --staged
```

### Practise recovery safely
Create a disposable repo, commit a file, make a change, stage it, and try `restore --staged`, `restore`, `reset --soft`, `revert`, and `reflog` with a fresh commit after each experiment. Do not begin with a valuable repository.

[↑ Back to TOC](#table-of-contents)

## 12. High-yield Git traps

1. `git add` stages a snapshot of content at that moment.
2. `git commit` records staged content.
3. `git commit -am` does not add untracked files.
4. `git fetch` does not automatically merge into the current branch.
5. `git pull` combines fetching with integration.
6. `git revert` creates a new commit; `reset` moves a reference.
7. `reset --hard` can discard work.
8. `restore --staged` unstages; it usually does not delete the corresponding working-tree edit.
9. Branches are refs, not separate folders.
10. Detached HEAD does not prevent committing, but makes those commits easier to lose track of.
11. `.gitignore` does not untrack already tracked files.
12. `uniq` is not relevant to Git; avoid confusing shell utilities with Git subcommands when reading mixed questions.
13. Merge conflicts require resolving, staging and completing the merge.
14. `origin/main` is a remote-tracking reference, not necessarily the current server state.
15. Avoid force-pushing shared branches unless you understand the impact and have permission.

[↑ Back to TOC](#table-of-contents)

## 13. Practice MCQs

### Q1. Staging

Which command shows changes that are staged but not committed?

A. `git diff`  
B. `git diff --staged`  
C. `git status --delete`  
D. `git reset --hard`

**Answer: B.**

### Q2. Fetch vs pull

Which statement is accurate?

A. Fetch always merges changes into the current branch  
B. Pull is fetch plus integration of updates  
C. Pull only creates tags  
D. Fetch deletes local commits

**Answer: B.**

### Q3. Tracked files

What does `git commit -am "update"` generally omit?

A. Modifications to tracked files  
B. Deletions of tracked files  
C. Untracked new files  
D. Existing staged changes

**Answer: C.**

### Q4. Undoing a shared commit

Which is often a safer way to reverse a commit in shared history?

A. `git revert COMMIT`  
B. `git reset --hard COMMIT`  
C. Delete the `.git` directory  
D. Edit the commit hash

**Answer: A.**

### Q5. Ignore files

What happens when a file already tracked by Git is added to `.gitignore`?

A. It is automatically untracked  
B. It is deleted from every clone  
C. It remains tracked unless removed from the index/history appropriately  
D. The repository stops working

**Answer: C.**

### Q6. Branches

What is a branch most accurately described as?

A. A full duplicate repository  
B. A movable reference to a commit  
C. A text file that stores every project file  
D. A remote server only

**Answer: B.**

### Q7. Staging reset

Which command unstages `notes.md` while keeping its working-tree edit in the usual case?

A. `git restore --staged notes.md`  
B. `git rm notes.md`  
C. `git clean -fd`  
D. `git reset --hard`

**Answer: A.**

### Q8. Detached HEAD

Which statement is true?

A. Commits are impossible in detached HEAD  
B. Detached HEAD means the repository is corrupted  
C. You can commit, but should create a branch if you need to retain the work easily  
D. It means no commit exists

**Answer: C.**

### Q9. Conflict handling

After resolving conflict markers in a file during a merge, what is normally needed?

A. Stage the resolved file and complete the merge  
B. Delete all Git branches  
C. Run `git init` again  
D. Only rename the file

**Answer: A.**

### Q10. Recovery clues

Which command can show recent movements of local references?

A. `git reflog`  
B. `git chmod`  
C. `git wc`  
D. `git grep --reflog`

**Answer: A.**

[↑ Back to TOC](#table-of-contents)

## 14. Study schedule and checklist

### Recommended one-week first pass

- **Days 1–2:** model, setup, init/clone, status, add, diff and commit.
- **Day 3:** log/show, branches, HEAD and switching.
- **Day 4:** merge and conflict resolution.
- **Day 5:** remotes, fetch, pull, push and tracking branches.
- **Day 6:** reset, restore, revert, reflog, ignore and stash.
- **Day 7:** scenario questions and safe recovery drills.

Return for spaced review after 1, 3, 7 and 14 days.

### Checklist

- [ ] I can explain the working tree, index, local repo and remote.
- [ ] I know what each common command changes.
- [ ] I can distinguish diff from diff --staged.
- [ ] I understand fetch, pull and push.
- [ ] I can resolve a simple merge conflict.
- [ ] I can compare reset, restore and revert.
- [ ] I can use reflog to reason about recovery.
- [ ] I practise destructive commands only in disposable repositories.
- [ ] I score at least 85% on two fresh quizzes.

[↑ Back to TOC](#table-of-contents)

## References

- [Pro Git book](https://git-scm.com/book/en/v2)
- [Official Git documentation](https://git-scm.com/docs)
- [Git reference](https://git-scm.com/docs)

[← Back to Pre-Test Roadmap](./README.md)
