<div align="center">
<img src="https://user-images.githubusercontent.com/74038190/212257468-1e9a91f1-b626-4baa-b15d-5c385dfa7ed2.gif" width="100">
</div>

# Git Commands Cheat Sheet

This is a list of common and useful Git commands that you can use in your daily development work.

> Note: I list an extra customizing git like alias, .gitignore, and .gitattributes

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
git commit -m "your commit message here"
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

- To list branches, use the command:

  ```bash
  git branch
  ```

  The `git branch` command without any options lists only the local branches in the repository. 

  Example:

  ```bash
  $ git branch
  * main
  ```

  The `*` before a branch name indicates that it's the currently checked out branch.

- To list all branches, including remote branches, use the command:

  ```bash
  git branch -a
  ```

   This `git branch -a` command lists all branches in the local repository, both local and remote. The branches are listed in a hierarchical structure, showing the remote repository (origin/upstream) followed by the branch name.

   Example:

   ```bash
   $ git branch -a
   * main
    remotes/origin/HEAD -> origin/main
    remotes/origin/main
    remotes/upstream/agraves.test-branch
    remotes/upstream/dotnet
    remotes/upstream/main
    remotes/upstream/strong-induction-edits
   ```

   The remote branches are listed under their respective remotes (origin and upstream in this case).

- To list only remote branches, use the command:

  ```bash
  git branch -r
  ```

  This `git branch -r` command lists only the remote branches in the repository. **These** are **branches** that **exist in the remote repositories** and have been fetched into your local repository, but they are not local branches that you can directly check out and work on. **To work on these branches**, you would **first** need to **check them out**, which **creates a local branch that tracks the remote one**. This command is useful when you want to see what branches exist on the remote repositories, without the clutter of your local branches.

  Example:

  ```bash
  $ git branch -r
    origin/HEAD -> origin/main
    origin/main
    upstream/agraves.test-branch
    upstream/dotnet
    upstream/main
    upstream/strong-induction-edits
  ```

  The remote branches are listed under their respective remotes (origin and upstream in this case).

- To create a branch and switch to it immediately, use the command:

  ```bash
  git checkout -b branch_name
  ```

   This `git checkout -b` command creates a new branch and switches to it immediately. It's a shortcut for the following two commands:
   
   ```bash
   git branch branch_name
   git checkout branch_name
   ```

   Example:

   ```bash
   $ git checkout -b new-branch
   Switched to a new branch 'new-branch'
   ```

- To fetch all branches from a remote repository and create corresponding local tracking branches , you can use the following commands:

   ```bash
   # Fetch all branches from the upstream repository
   git fetch upstream

   # Check out each branch you want to have locally, creating a local tracking branch
   git checkout -b branch-name upstream/branch-name
   ```
   Replace `branch-name` with the name of each branch you want to create locally. This will create a new local branch that tracks the corresponding branch from the `upstream` repository.

   If you want to fetch all branches and automatically create tracking branches for all of them, you can use a loop in bash:

   ```bash
   # Fetch all branches from the upstream repository
   git fetch upstream
   # Loop over each branch from the upstream repository
   for branch in $(git branch -r | grep 'upstream/' | sed 's/upstream\///'); do
       # Check out each branch, creating a local tracking branch
       git checkout -b $branch upstream/$branch;
   done
   ```
   Example:

   ```bash
   $ for branch in $(git branch -r | grep 'upstream/' | sed 's/upstream\///'); do
   > git checkout -b $branch upstream/$branch;
   > done
   Switched to a new branch 'agraves.test-branch'
   Switched to a new branch 'dotnet'
   Switched to a new branch 'main'
   Switched to a new branch 'strong-induction-edits'
   ``` 

   This will create a local branch for each branch in the `upstream` repository, each tracking its corresponding `upstream` branch.
   
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
git pull
```

`git pull` is a Git command used to update the local version of a repository from a remote. It is actually a combination of `git fetch` followed by `git merge`. When you use `git pull`, Git will do the following:

1. Fetch the branch of the same name from the remote repository that you're currently working on.
2. Merge the changes from that branch into your current local branch.

Here's a detailed breakdown:

- `git pull`: This command fetches the branch from the remote repository that corresponds to the current local branch and then merges the changes into the current local branch. If there are any conflicts between the local and remote versions, Git will prompt you to resolve them.

- `git pull origin master`: This command fetches the 'master' branch from the 'origin' remote repository and then merges the changes into the current local branch. Again, if there are any conflicts, Git will prompt you to resolve them.

Use Case:

Suppose you're working on a project with a team, and you're all pushing changes to the same remote repository. You've been working on the 'feature' branch locally, and you want to get the latest changes that your teammates have pushed to the 'feature' branch on the remote repository. You would navigate to your local 'feature' branch and then run `git pull`. This would fetch the latest version of the 'feature' branch from the remote repository and merge it into your local 'feature' branch. If there are any conflicts between your local version and the remote version, you would need to resolve them before the merge can complete.

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

Best practices for writing a `.gitignore` file:

1. **Don't ignore everything:**
   Only ignore files that are generated automatically, such as compiled source code, dependancy folders, and temporary files. Don't ignore files that are part of the project, such as source code, documentation, and configuration files.

2. **Use glob patterns:**
   You can use glob patterns to ignore files with a certain extension or in a certain directory. For example, to ignore all `.log` files, you can use the pattern `*.log`. To ignore all files in a directory named `logs`, you can use the pattern `logs/`.

3. **Ignore files locally if needed:**
   If you want to ignore files only in your local repository, you can create a `.git/info/exclude` file. This file works the same way as a `.gitignore` file, but it's not committed to the repository. This is useful if you want to ignore files that are specific to your local environment, such as editor configuration files.

4. **Check what you're ignoring:**
   Before you commit your `.gitignore` file, make sure that you're not ignoring any important files. You can do this by running the `git status --ignored` command. If you see any files that you want to track, you can remove them from the `.gitignore` file.

5. **Use templates:**
   There are many `.gitignore` templates available online for different types of projects. You can use these templates as a starting point for your own `.gitignore` file. You can find a list of templates on the [GitHub gitignore repository](https://github.com/toptal/gitignore)


Example of a .gitignore file for a Python project:

```bash
# Byte-compiled / optimized / DLL files
__pycache__/
*.py[cod]
*$py.class

# C extensions
*.so

# Distribution / packaging
.Python
build/
develop-eggs/
dist/
downloads/
eggs/
.eggs/
lib/
lib64/
parts/
sdist/
var/
wheels/
pip-wheel-metadata/
share/python-wheels/
*.egg-info/
.installed.cfg
*.egg
MANIFEST

# PyInstaller
#  Usually these files are written by a python script from a template
#  before PyInstaller builds the exe, so as to inject date/other infos into it.
*.manifest
*.spec

# Installer logs
pip-log.txt
pip-delete-this-directory.txt

# Unit test / coverage reports
htmlcov/
.tox/
.nox/
.coverage
.coverage.*
.cache
nosetests.xml
coverage.xml
*.cover
.hypothesis/
.pytest_cache/

# Translations
*.mo
*.pot

# Django stuff:
*.log
local_settings.py
db.sqlite3
db.sqlite3-journal

# Flask stuff:
instance/
.webassets-cache

# Scrapy stuff:
.scrapy

# Sphinx documentation
docs/_build/

# PyBuilder
target/

# Jupyter Notebook
.ipynb_checkpoints

# IPython
profile_default/
ipython_config.py

# pyenv
.python-version

# pipenv
#   According to pypa/pipenv#598, it is recommended to include Pipfile.lock in version control.
#   However, in case of collaboration, if having platform-specific dependencies or dependencies
#   having no cross-platform support, pipenv may install dependencies that don’t work, or not
#   install all needed dependencies.
#Pipfile.lock

# PEP 582; used by e.g. github.com/David-OConnor/pyflow
__pypackages__/

# Celery stuff
celerybeat-schedule
celerybeat.pid

# SageMath parsed files
*.sage.py

# Environments
.env
.venv
env/
venv/
ENV/
env.bak/
venv.bak/

# Spyder project settings
.spyderproject
.spyproject

# Rope project settings
.ropeproject

# mkdocs documentation
/site

# mypy
.mypy_cache/
.dmypy.json
dmypy.json

# Pyre type checker
.pyre/
```

## .gitattributes

The `.gitattributes` file is a plain text file that controls how Git treats files. Each line in the `.gitattributes` file is a pattern followed by an attribute specification. It's placed in the root directory of a Git repository and contains a list of file patterns followed by the attributes that should be applied to them.

Here are a few use cases of .gitattributes:

1. **Specify line ending style**: You can use `.gitattributes` to normalize line endings to a standard style. This is useful in a team where developers are using different operating systems that handle line endings differently (like Windows using CRLF and Unix using LF).

    ```gitattributes
    # Ensure all .txt and .md files use LF
    *.txt text eol=lf
    *.md text eol=lf
    ```

2. **Mark files as binary**: If you have binary files in your repository, you can use `.gitattributes` to tell Git to treat them as such. This can prevent Git from trying to merge them or show diffs for them.

    ```gitattributes
    # Treat .jpg and .png files as binary
    *.jpg binary
    *.png binary
    ```

3. **Specify diff driver**: For certain types of files, you might want to use a different tool to show diffs. You can specify this in the `.gitattributes` file.

    ```gitattributes
    # Use the "diff-python" tool for .py files
    *.py diff=diff-python
    ```

4. **Export-ignore**: If you're creating an archive of your files (for example, with `git archive`), you can use the `export-ignore` attribute to exclude certain files from the archive.

    ```gitattributes
    # Ignore test files and documentation when creating an archive
    /tests export-ignore
    /docs export-ignore
    ```

Remember to commit the `.gitattributes` file into your repository so that these settings are shared with all collaborators.

