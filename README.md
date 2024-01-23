<div align="center">
<img src="https://user-images.githubusercontent.com/74038190/212257468-1e9a91f1-b626-4baa-b15d-5c385dfa7ed2.gif" width="100">
</div>

# Git Commands Cheat Sheet

This is a list of common and useful Git commands that you can use in your daily development work.

## Setting Upstream in Git

This guide explains how to set up an upstream branch in Git. Setting an upstream branch means to link a local branch to a remote branch. This is useful for tracking the relationship between the two, and Git can provide helpful information about the status of the branches.

### Steps

1. **Create a new branch**

   Create a new branch in your local repository.

   ```bash
   git checkout -b new-branch
   ```

2. **Push the new branch to the remote repository**
   
   Push the new branch to the remote repository. The `-u` option sets the upstream branch for the new branch.

   ```bash
   git push -u origin new-branch
   ```

   The `-u` option stands for --set-upstream. Afters setting the upstream branch with this command, Git will know that `git push` and `git pull` for your local branch should go to that same branch on the remote repository.

3. **Set the upstream branch for an existing branch**
   
   If you have an existing branch and you want to set its upstream branch with this command, Git will know that `git push` and `git pull` for your local branch should go to that same branch on the remote repository.

   ```bash
    git branch --set-upstream-to=origin/remote-branch
    ```

    Replace `remote-branch` with the name of the branch on the remote repository that you want to track.

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

This is a versatile command that can be used for both switching to a different branch and for checking out files from a different branch. This can sometimes lead to confusion, especially for beginners, because the command's behavior changes based on the context.


To switch to a newly created branch, use the command:

```bash
git checkout branch_name
```

## Switch

This is a newer command, introduced in Git 2.23.0, that is specifically designed for switching between branches. It separates the "switching branches" and "checking out files" functionalities of `git checkout` into two distinct commands (`git switch` and `git restore` respectively). This makes it more intuitive and less error-prone to use, especially for beginners.

```bash
git switch branch_name
```

Note:<br>

If you're using a version of Git that's older than 2.23.0, `git switch` won't be available. In that case, you'll need to use `git checkout` to switch branches.

`git checkout` and `git switch` are both Git commands used to switch between different branches in a Git repository. However, they have some differences in their usage and functionality.

## Branch

To list branches, use the command:

```bash
git branch
```

To create a branch and switch to it immediately, use the command:

```bash
git checkout -b branch_name
```

## Branch -vv

If you want to check tracking branches for pull and push requests. This command will list all local branches along with their corresponding remote branches if they have one.

Here is the command:

```bash
git branch -vv
```

The output will look something like this:

```bash
main  a3f66fd [origin/main] Add README file
feature 687704c [origin/feature: ahead 1, behind 1] Add new feature
```

In this example, the `main` branch is tracking `origin/main`, and the `feature` branch is tracking `origin/feature`. The `ahead 1` and `behind 1` indicate that the `feature` branch is one commit ahead of and one commit behind its remote tracking branch.

## Remote

To add a remote repository, use the command:

```bash
git remote add <name> <url>
```

To push changes to a remote repo, use the command:

```bash
git push
```

## Remote set-url

If you've already added a remote repository with the wrong URL, you can change it using the `git remote set-url` command. Here's how:

1. First, check the current remote repository for your project. You can do this with the `git remote -v` command. This will list all remote repositories and their URLs.

    ```bash
    git remote -v
    ```

2. If the URL for `origin` is incorrect, you can change it with the `git remote set-url` command. Replace `new_url` with the correct URL for your remote repository.

    ```bash
    git remote set-url origin new_url
    ```

3. Verify that the remote URL has been changed with the `git remote -v` command again.

    ```bash
    git remote -v
    ```

Now, the `origin` should point to the correct remote repository URL.


## Renaming a Git Branch

This guide explains how to rename a local Git branch and update the remote repository to reflect the change.

### Steps

1. **Rename the local branch**

   If you are currently on the branch you want to rename:

   ```bash
   git branch -m new-branch-name
   ```
   if you are on a different branch:

   ```bash
    git branch -m old-branch-name new-branch-name
    ```
    Replace `old-branch-name` with the current name of the branch, and `new-branch-name` with the name you want to give to the branch.

2. **Push the branch to the remote repository**

    ```bash
    git push origin -u new-branch-name
    ```
    Replace `new-branch-name` with the name of the branch you set in the previous step.

3. **Delete the old branch from remote repository**

    ```bash
    git push origin --delete old-branch-name
    ```
    Replace `old-branch-name` with the name of the branch you want to delete.

    Please be careful when deleting branches from a remote repository, as you might lose comits if you delete the wrong branch.


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

## Pull + rebase

To fetch a branch from remote + rebasing it

```sh
git pull --rebase
```

## Alias

In Git, an alias is a shorter name or abbreviation for a command or a set of commands. It's a way to create custom commands or shorten existing ones to make them quicker and easier to type.
Aliases are defined in the Git configuration file, which can be at the system, user, or repository level. The --global option sets the alias for all repositories for the current user.

- Shorten the status command

```bash
git config --global alias.st status
```

- Shorten the checkout command

```bash
git config --global alias.co checkout
```

- Shorten the branch command

```bash
git config --global alias.br branch
```

- Shorten the commit command

```bash
git config --global alias.ci commit
```

- Shorten the diff command

```bash
git config --global alias.df diff
```

- Shorten the add command

```bash
git config --global alias.ad add
```

- Show logs in one line format

```bash
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```
- Show the status in short format

```bash
git config --global alias.s "status -s"
```

- Show the list of aliases

```bash
git config --global --get-regexp alias
```
This command will list all the aliases that are set in your global Git configuration file.
Each alias will be displayed in the format `alias.<alias-name> <command>`, where `<alias-name>` is the name of the alias and `<command>` is the Git command that the alias stands for.

## .gitignore

 The `.gitignore` is a plain text file that tells Git to intentionally ignore changes in certain files. A `.gitignore` file is placed in the root directory of a Git repository and contains a list of files and directories that Git should ignore.

 Common types of files to ignore include:
 
 1. Compiled source code:
    Files that are the output of a build process, such as:
    - `.o`
    - `.pyc`
    - `.class`
    - `.dll`
    - `.exe`
    - `.so`


 2. Packages:
    Dependancy folders, such as:
    - `.node_modules`
    - `.bower_components`
    - `.pnp`
    - `.vendor`

 3. Logs and databases
    Log, data, and other files generated at runtime, such as:

    - `.log`
    - `.sql`
    - `.sqlite`

 4. Operating system generated files
    Temporary files created by the operating system, such as:

    - `.DS_Store`
    - `.Thumbs.db`
    - `.Spotlight-V100`
    - `.Trashes`

 5. User-generated settings
    Files that are personal user settings, like:

    - `.vscode`
    - `.idea`

 6. Secrets
    Files containing sensitive data, like:

    - `.env`
    - `.config.json`
