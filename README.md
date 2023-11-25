<div align="center">
<img src="https://user-images.githubusercontent.com/74038190/212257468-1e9a91f1-b626-4baa-b15d-5c385dfa7ed2.gif" width="100">
</div>

# Git Commands Cheat Sheet

This is a list of common and useful Git commands that you can use in your daily development work.

## Configuration

To check your Git configuration, which includes user name and email, use the command:

```bash
git config -l
```

## Status

To check the status of the current repository, including staged, unstaged, and untracked files, use the command:

```bash
git status
```

## Commit

To commit changes, use the command:

```bash
git commit
```

To commit changes and skip the staging area, use the command:

```bash
git commit -a -m"your commit message here"
```

## Log

To see your commit history, use the command:

```bash
git log
```

To see your commit history including changes, use the command:

```bash
git log -p
```

## Diff

To see changes made before committing them, use the command:

```bash
git diff
```

## Remove

To remove tracked files from the current working tree, use the command:

```bash
git rm filename
```

## Checkout

To switch to a newly created branch, use the command:

```bash
git checkout branch_name
```

## Branch

To list branches, use the command:

```bash
git branch
```

To create a branch and switch to it immediately, use the command:

```bash
git checkout -b branch_name
```

## Remote

To add a remote repository, use the command:

```bash
git remote add <name> <url>
```

To push changes to a remote repo, use the command:

```bash
git push
```

## Pull

To pull all data from git, use the command:

```bash
git fetch –all
```

## Pull Request

To create a pull request, you typically don't use a Git command. Instead, you use the web interface of your Git hosting service (like GitHub, GitLab, or Bitbucket). However, you can use the `git request-pull` command to generate a summary of pending changes:

```bash
git request-pull <start> <URL> [<end>]
```

## Pull

To fetch from and integrate with another repository or a local branch, use the command:

```bash
git pull [<options>] [<repository> [<refspec>…​]]
```

## Merge

To merge another branch into your current branch, use the command:

```bash
git merge branch_name
```

## Rebase

To apply changes from another branch onto your current branch, use the command:

```bash
git rebase branch_name
```
