# Git workflow and learning path

This is a solo project developed as if changes need to be understandable to a
reviewer. The assistant can run routine Git commands within the agreed task and
read their output directly. For each command, explain what it does, when it is
useful, why it is needed now, and whether it changes files or history, then
interpret the actual result with the user. The user can run commands for practice
without being required to copy terminal output back to the assistant.

## The first mental model

Git is local version control. GitHub hosts a remote copy and the pull-request
discussion. A public repository can be read and forked by other people; that
does not give them permission to push to the user's repository.

| Concept | Meaning |
| --- | --- |
| Working tree | The files currently on this computer, including uncommitted edits. |
| Staging area | The exact changes selected for the next commit. |
| Commit | A recorded snapshot with a message and parent history. It is initially local. |
| Branch | A movable name pointing to a commit, used to keep a line of work separate. |
| Remote | A named connection to another repository, usually `origin` for GitHub. |
| Remote-tracking branch | This clone's last fetched view of a remote branch; it is not a live connection. |
| Pull request | A GitHub proposal to merge one branch's changes into another, including review and checks. |

Start by inspecting status and diffs. Learn the difference between an untracked
file, an unstaged edit, and a staged change before making the first setup commit.
Review what is staged, not just what is visible in the editor.

## Default development workflow

1. Start from an up-to-date local `main`. Fetch to inspect remote changes; use a
   fast-forward-only update for `main` so divergence is visible rather than
   resolved implicitly.
2. Create a short-lived branch for one focused outcome, such as workspace path
   validation. Branches are cheap and do not need a complete feature to exist.
3. Make a small change and understand it. Review the diff and perform the checks
   relevant to that change. A documentation change does not need invented tests.
4. Stage only intended changes and commit with a message describing the outcome.
   Several commits on a feature branch are normal. Avoid mixing unrelated editor
   cleanup, application behavior, and formatting in one implementation commit.
5. Push the feature branch and open a pull request into `main`. Start it as a
   draft when useful. Explain the problem, resulting behavior, checks performed,
   and known limitations.
6. Review the PR diff as if seeing it for the first time. For a solo project,
   self-review and checks are useful; a mandatory approval from another person
   would block work unless a reviewer is available. AI feedback supplements the
   user's review rather than replacing understanding.
7. Merge after the relevant checks pass. The proposed starting convention is
   squash merging one focused PR into one understandable commit on `main`.
8. Update local `main`, then remove the completed feature branch when its work
   is verified in the merged history. Do not remove branches with unmerged work.

This is a proposed teaching workflow, not a statement that branch protection,
CI, or pull requests have already been configured. Choose any repository rules
together before applying them.

## Learn the three merge strategies

| Strategy | What happens | Tradeoff |
| --- | --- | --- |
| Merge commit | Joins the histories and records a merge commit. | Preserves branch history; the graph can become busier. |
| Squash merge | Creates a new commit containing the combined change. | Gives `main` a concise history; individual feature commits are not retained as ancestors of that squash commit. |
| Rebase and merge | Replays commits onto another base. | Produces linear history but changes commit identities. |

First learn how ordinary branching and merging work. Introduce rebase after the
user can explain shared versus unpublished history. Do not rewrite a shared
branch or force-push merely to make the graph look tidy.

## Working on Windows and a Mac laptop

Both computers have independent clones connected to the same GitHub repository.
Git carries committed source and configuration between them; it does not copy
uncommitted work, running processes, or installed environments.

- Clone the repository once on the laptop. Do not copy `.git` or `.venv` from the
  Windows machine, and do not run both clones through a shared cloud-sync folder.
- Install the required Python version and create a separate `.venv` on each
  machine. Install dependencies from the project dependency files. Platform
  compatibility must be checked on the laptop; Windows import checks alone do
  not prove it.
- Open the repository root in VS Code, install the recommended extensions, and
  choose that clone's interpreter. See [the editor guide](EDITOR.md) for the
  project settings and global editor preferences, including Vim.
- Before switching computers, save and commit work on the feature branch and
  push it. A clearly marked work-in-progress commit on that branch is acceptable
  for a handoff; it does not need to be merged into `main`.
- On the receiving computer, fetch and check out or update the same feature
  branch before editing. If both machines have new local commits, inspect the
  divergence and reconcile it instead of overwriting either copy.
- Use branches and normal remote synchronization for handoffs. Cherry-picking
  is not the default way to move the same branch between computers.

`.gitattributes` gives the repository a consistent text line-ending policy.
`.gitignore` excludes environments, credentials, caches, runtime state, and the
agent's target workspace. Only the portable editor settings and extension
recommendations are shared from `.vscode`; local backups remain ignored.

## Advanced skills to introduce through real examples

| Skill | When it is useful | What to understand first |
| --- | --- | --- |
| Conflict resolution | Two lines of work change overlapping content. | Understand both intended behaviors; do not blindly pick an entire side. Re-run relevant checks after resolving. |
| Cherry-pick | Apply a particular commit to another branch, such as a focused fix. | It creates a new commit and may need earlier dependencies. It is not a substitute for merging related history. |
| Revert | Undo a published change through a new commit. | History remains visible and other clones can update normally. |
| Restore and reset | Discard selected edits or move a local branch/index. | Their scopes differ. Inspect what can be lost and explain destructive options before using them. |
| Stash | Temporarily put local unfinished work aside. | A stash is local and is not a second-machine handoff or durable remote backup. |
| Reflog | Find commits that a local branch previously pointed to. | It is local recovery information with retention limits, not a permanent backup. |
| Interactive rebase | Organize unpublished feature commits. | Reordering and squashing rewrite commit identities and can break dependencies. |
| Bisect | Narrow down which commit introduced a regression. | Requires a repeatable way to classify a commit as good or bad. |
| Worktrees | Use separate checkouts for independent branches. | Files and branch ownership must stay clear; introduce only after ordinary branch workflow is comfortable. |

Do not introduce all of these commands at once. Teach the problem, inspect the
history, predict the outcome, perform the agreed operation, and verify the result
together. The user may take the keyboard when they want hands-on command practice.

## Public repository habits

Review staged content for credentials and local-only files. An ignored file is
not protected if it was already tracked, and deleting a secret in a later commit
does not remove it from earlier history. If a credential is exposed, revoke it
and address the repository history as a separate task.

Introduce a CI workflow when meaningful tests exist. The intended future checks
should exercise supported operating systems and use deterministic test fixtures
without requiring paid model calls or production credentials. A green run that
discovers zero tests is not evidence that the harness works.

## Current next lesson

The scaffold, dependency files, documentation, and portable editor settings have
local changes. Begin by explaining and inspecting their status and diff, then
decide how to group the setup commits. Work through staging, committing, pushing,
and the first PR as explained steps; the assistant may execute routine commands
within that agreed workflow. This does not authorize unexplained history rewrites
or unrelated repository changes.
