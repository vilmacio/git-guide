# git-guide
> This is a git guide that contain command examples with explanations, different use cases and links to further documentations.

*Read this in: [Português](/README.pt-BR.md)*

---

### [Config](https://git-scm.com/docs/git-config)
```bash
# System git config
$ git config --system --edit

# Global git config (User config)
$ git config --global --edit

# Local git config (Project config)
$ git config --edit
# or
$ git config --local --edit
```
#### How to create [alias](https://git-scm.com/docs/git-config#Documentation/git-config.txt-alias)
Run the following command:
```console
admin:~$ git config --global --edit
```
You must add the following command to the .gitconfig file opened into editor:
```js
[alias]
  c = !git command
```
Now, use `git c` instead.

### Creating [commit](https://git-scm.com/docs/git-commit) and [stash](https://git-scm.com/docs/git-stash)
```bash
# Add files to stage area
$ git add file_name # Add single file.
$ git add . # Add files from current diretory.
$ git add --all # Add all files.

# Create a commit
$ git commit -m "message" # It creates a new commit.
$ git commit --amend --no-edit # It creates a commit merged with the previous commit.

# Putting changes to stash
$ git stash # Stash all modifications.
$ git stash list # Saved stash listing.
$ git stash pop # Returns modifications from stash and clears the list.
$ git stash apply # Returns modifications
$ git stash clear # Clear the stash listinig
```

### File [status](https://git-scm.com/docs/git-status)
#### Untracked files
Unknown files by git.
```console
admin:~$ git status -s
?? index.js
```
#### Not staged (Unstaged area)
Files known to git but not added to stage area after modification. They are outside the stage area therefore they will not enter the next commit.
```console
admin:~$ git status -s
M index.js
```
#### Staged (Staging area / Index)
Files that will enter the next commit.
```console
admin:~$ git status -s
A index.js
```

### Auxiliary commands
[status](https://git-scm.com/docs/git-status), [show](https://git-scm.com/docs/git-show) and [log](https://git-scm.com/docs/git-log)
```bash
# Show status of modified files and current branch.
$ git status
# or
$ git status --s

# Show specific commit details
$ git show
# or
$ git show --oneline

# Commit listing
$ git log
# or
$ git log --oneline
```

#### How to add [custom git log](https://git-scm.com/docs/git-log#_pretty_formats) to the alias:
Add the following command to the alias:
```
l = !git log --pretty=format:'%C(green)%h %C(yellow)%d %C(white)%s - %C(cyan)%cn, %C(blue)%cr'
```
New *git log*:
<p><img src="/samples/log.png"></p>

### [Tags](https://git-scm.com/docs/git-tag)
```bash
# Create a new tag
$ git tag v1.0 hash_commit # It creates a Lightweight tag
$ git tag v1.0 -m "Release v1.0" hash_commit # It creates a Annotated tag (for sending github)

# View tags
$ git tag # Show all tags
$ git tag v1.0 # Show a single tag

# Delete tag
$ git tag --delete v1.0 # Delete from local
$ git push --delete origin v1.0 # Delete from remote
```
#### Sending Annotated tags to GitHub
Open the global git config `--global` and add the following code:
```js
  [push]
    followTags = true
```

### [Checkout](https://git-scm.com/docs/git-checkout)
```bash
$ git checkout . # Returns changes to files that are Unstaged and tracked.
$ git checkout [[commit_ref] or [tag_ref]] # Creates a virtual branch with the chosen point to analyze the code.
$ git checkout -b nome_branch # Create a truly branch.
$ git checkout nome_branch # Switch between branches.

```
### [Merge](https://git-scm.com/docs/git-merge)
```bash
$ git merge branch_name . # Merge the current branch with the branch_name.

```

### [Git reset](https://git-scm.com/docs/git-reset) 

#### Standard structure
```bash
$ git reset [hash or HEAD~n] --flag
```
*HEAD* - Last commit
####
*n* - Number of commits below HEAD.
####
*hash* - Commit hash ( The default is the last commit (HEAD) )
####
*--flag* - It can be --soft, --mixed (default), --hard

#### Examples
  ```bash
  # Handling commits
  $ git reset HEAD~1 --soft # Goes back to the previous commit by placing the files to Staging area.
  $ git reset HEAD~2 --mixed # Goes back 2 commits by placing the files back in the Unstaged area.
  $ git reset HEAD~1 --hard # Goes back to the previous commit and undo the modification of the Unstaged area files.
  
  # Handling the current commit (HEAD)
  # The default is the HEAD
  $ git reset # --mixed tag omitted. Place the files from the Staging Area to Unstaged area.
  $ git reset --hard # Undo the modification of files that are in the Unstaged area or Staging area.
  ```

### [Revert](https://git-scm.com/docs/git-revert)
#### Structure
```bash
$ git revert [hash ou HEAD~1] --flag
```
#### Examples
```bash
$ git revert HEAD~1 # Creates a new commit with the reverse modifications.
$ git revert HAAD~1 --no-edit # Creates a new commit no editing.
$ git revert HEAD~1 --no-commit # Make the reverse changes to the files and add them to Staging area.
```

### [Clean](https://git-scm.com/docs/git-clean)
#### Structure
```bash
$ git clean --flag
```
#### Examples
```bash
$ git clean -n # Show the untracked files.
$ git clean -n -d # Show all untracked files recursively.
$ git clean -f # Delete the untracked files.
$ git clean -f -d # Delete all untracked files recursively.
```

### [Rm](https://git-scm.com/docs/git-rm)
#### Structure
```bash
$ git rm file.ex --flag
```
#### Examples
```bash
$ git rm index.js # Remove the tracked file.
$ git rm folder -r # Remove the tracked files recursively.
```
#### How to ignore tracked files.
Run the following command:
```bash
$ git rm index.js --cached'
```

### [Rebase](https://git-scm.com/docs/git-rebase)
Run the following command to open the editor:
```bash
$ git rebase -i [commit_ref]'
```

#### Commands
```bash
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup <commit> = like "squash", but discard this commit's log message
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
# .       create a merge commit using the original merge commit's
# .       message (or the oneline, if no original merge commit was
# .       specified). Use -c <commit> to reword the commit message.
```

Close the editor or use the ```---abort``` flag to exit *rebasing* mode.
```bash
$ git rebase --abort'
```

