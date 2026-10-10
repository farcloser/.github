# Git for contributors

The rules a pull request must meet are in [CONTRIBUTING.md](./CONTRIBUTING.md). This is
the companion: the git moves that get you there, for anyone whose day job did not involve
rewriting history. None of it is advanced; all of it comes up.

1. [Sign-off and signature](#sign-off-and-signature)
1. [Amend instead of piling up](#amend-instead-of-piling-up)
1. [Rebase, do not merge](#rebase-do-not-merge)
1. [Force-push with a lease](#force-push-with-a-lease)
1. [One commit per concern](#one-commit-per-concern)
1. [Edit a commit in the middle](#edit-a-commit-in-the-middle)
1. [Name your branches](#name-your-branches)
1. [Name your stashes](#name-your-stashes)
1. [Remotes](#remotes)
1. [FAQ](#faq)

## Sign-off and signature

Two different things, both required, both one flag:

```bash
git commit -s -S -m "Subject"
```

- `-s` adds `Signed-off-by: Name <email>`, the [DCO](https://developercertificate.org/)
  trailer: a statement, taken from your git identity, that you may contribute this code.
- `-S` signs the commit with your key: proof the commit came from you. With
  `commit.gpgsign` set as CONTRIBUTING shows, you can leave `-S` out; git signs every
  commit.

Forgot either on a whole branch? Rewrite it in one go:

```bash
git rebase --signoff --exec 'git commit --amend --no-edit -S' origin/main
```

## Amend instead of piling up

Iterating on one change does not need one commit per iteration. Fold the fix into the
commit it belongs to:

```bash
git add path/to/file
git commit --amend --no-edit
```

`--amend` opens the message for editing unless you pass `--no-edit`. The amended commit
is a new commit: with `commit.gpgsign` set, git signs it again on its own; without it,
pass `-S` again or the signature is gone.

## Rebase, do not merge

`main` moves while your pull request is open. Put your work back on top of it, so the
diff the reviewer sees is yours and nothing else:

```bash
git fetch origin
git rebase origin/main
# On a conflict: fix the file, then
git add path/to/file
git rebase --continue
```

Never `git merge main` into your branch: it adds a merge commit that says nothing and
makes your diff include other people's changes.

## Force-push with a lease

A rebase or an amend rewrites your branch, so a plain push is refused. Do not reach for
`git push -f`: it overwrites whatever is on the remote, including a commit a reviewer or
a bot pushed to your branch while you were working. The lease refuses the push when the
remote moved under you:

```bash
git push --force-with-lease
```

If it is refused, fetch, look at what arrived, rebase on top of it, push again.

## One commit per concern

A pull request is read commit by commit. Keep each commit to one thing with its own
reason: a fix is one commit, the test for it is in the same commit, an unrelated cleanup
you did on the way is another commit, or another pull request. A commit's subject says
what it does; its body says why.

If you were asked to squash, it means your commits are iterations of one change, not
several changes; fold them into the one that carries the reason:

```bash
git rebase --interactive origin/main
```

Mark every line but the first `fixup` (keep its changes, drop its message) or `squash`
(keep its changes, merge its message), save, and git does the rest. Then push with a lease.

## Edit a commit in the middle

Review asked for a change to the second of your five commits, not the last. Make the
change, then put it where it belongs:

```bash
git add -p path/to/file          # stage only the hunks for that commit
git commit --fixup <sha-of-commit-2>
git rebase --interactive --autosquash origin/main
```

`--fixup` writes a commit git knows how to fold, `--autosquash` places it behind its
target in the rebase list, and the editor opens with everything already in order: save
and exit. Repeat per target commit when several need a change.

To drop a commit, delete its line in the interactive list. To change a commit's message,
mark it `reword`.

## Name your branches

A busy contributor keeps dozens of branches, some for months. A name that says nothing
(`fix`, `wip2`, `try-again`) is a branch you will not dare delete. One scheme that holds
up:

```
<type>/<issue>-<short-description>
fix/123-checksum-drift
feature/88-sbom-output
```

The issue number ties the branch to the ticket and the pull request; the description
tells you what it is without checking out.

## Name your stashes

```bash
git stash push -m "half-done retry logic, before the rebase"
git stash list
```

A bare `git stash` gives you `WIP on main: 1a2b3c4 ...` five times over. The stash you
cannot identify is the stash you lose. Apply by name, not by position (`stash@{0}` moves
every time you stash again):

```bash
git stash apply stash^{/retry}
```

## Remotes

```bash
git remote -v
git remote add upstream git@github.com:owner/repo.git
git fetch --all
git branch -a
git switch -c fix/123-thing upstream/main    # a new branch off a remote branch
git push -u origin fix/123-thing             # first push, sets the tracking branch
```

`git switch` is the modern form of `git checkout` for branches; `git restore` is the one
for files.

## FAQ

**I committed without the DCO sign-off.** `git commit --amend -s --no-edit` for the last
commit; `git rebase --signoff origin/main` for the branch.

**What does the sign-off do, exactly?** It appends `Signed-off-by: Name <email>` to the
message, from `user.name` and `user.email` in your git configuration. Set them once
(`git config --global user.name ...`), or per repository without `--global` when you
contribute under more than one identity.

**My commit shows "Unverified" on GitHub.** The key that signed it is not on your GitHub
account as a *signing* key (a key can be registered for authentication, signing, or
both), or the commit's author email is not one of the account's verified emails.

**The pull request says my branch has conflicts.** Rebase on `main` as above; resolve;
push with a lease. The pull request updates itself.

**I rebased and now the pull request shows commits that are not mine.** You rebased onto
a stale `main`, or merged instead of rebasing. `git fetch origin && git rebase origin/main`
again; if a merge commit crept in, `git rebase --interactive origin/main` and drop it.
