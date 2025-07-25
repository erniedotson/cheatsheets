# Git Cheatsheet

## Git Setup and Configuration

| Action | Command |
| ------ | ------- |
| Configure username for all repos | `git config --global user.name "<firstname> <lastname>"` |
| Configure email for all repos | `git config --global user.email "<email-address>"` |
| Turn on command line coloring | `git config --global color.ui auto` |
| EOL Conversions: checkout CRLF, commit LF (recommended for Windows) | `git config --global core.autocrlf true` |
| EOL Conversions: checkout as-is, commit LF (recommended for Linux/Mac) | `git config --global core.autocrlf input` |
| EOL Conversions: checkout as-is, commit as-is (i.e. no conversions) | `git config --global core.autocrlf false` |
| Display all settings | `git config --list --show-origin` |
| Display aliases | `git config --list \| grep alias` |
| Configure kdff3 as diff and merge tool | `git config --global merge.tool kdiff3`<br/>`git config --global mergetool.kdiff3.path "C:/Program Files/KDiff3/kdiff3.exe"`<br/>`git config --global mergetool.kdiff3.trustExitCode false`<br/><br/>`git config --global diff.guitool kdiff3`<br/>`git config --global difftool.kdiff3.path "C:/Program Files/KDiff3/kdiff3.exe"`<br/>`git config --global difftool.kdiff3.trustExitCode false` |

## Repo setup and configuration

### Misc. repo commands

| Action | Command |
| ------ | ------- |
| Initialize current directory as a new Git repo | `git init` |
| Retrieve a remote repo | `git clone <url-to-repo>` |
| Configure username for current repo *(overrides global setting)* | `git config --local user.name "<firstname> <lastname>"` |
| Configure email for  for current repo *(overrides global setting)* | `git config --local user.email "<email-address>"` |
| List remotes | `git remote -v` |
| Add additional remote | `git remote add <alias> <url-to-repo>` |
| Update remote URL | `git remote set-url <alias> <url-to-repo>` |
| Remove a remote | `git remote remove <alias>` |

### Switching remote URIs from HTTPS (username & password) to SSH (public/private key) authentication

```bash
# List remotes, note the alias (usually origin)
git remote -v

# Change the URI
git remote set-url <alias> git@<hostname>:<path-to-context>/<repo-name>.git

# Verify the remote URI
git remote -v
```

### Switching remote URIs from SSH (public/private key) to HTTPS (username & password) authentication

```bash
# List remotes, note the alias (usually origin)
git remote -v

# Change the URI
git remote set-url <alias> https://@<hostname>:<path-to-context>/<repo-name>.git

# Verify the remote URI
git remote -v
```

## Dealing with Certificate errors

These can be helpful if your server has a self-signed certificate, a certificate issued by an unknown Certificate Authority, or most other certificate errors.

| Action | Command |
| ------ | ------- |
| Turn off **ALL** certificate validation *(not recommended for security reasons)* | `git config --global http.sslVerify false` |
| Clone a repo, ignoring certificate errors | `GIT_SSL_NO_VERIFY=true git clone <url-to-repo>` |
| Turn off certificate validation for current repo | `git config http.sslVerify false` |

## Branches

### Misc. branch commands

| Action | Command |
| ------ | ------- |
| List branches | `git branch` |
| Create new branch at current commit | `git branch <branch-name>` |
| Switch to existing branch | `git checkout <branch-name>` |
| Switch to existing branch if it exists, else create it | `git checkout -B <branch-name>` |
| Merge `branch-name` into current branch | `git merge <branch-name>` |
| Merge `branch-name` into current branch, creating merge commit | `git merge --no-ff <branch-name>` |
| Squash and merge `branch-name` into local branch | `git merge --squash <branch-name>` |
| Delete local branch | `git branch -D <branch-name>` |
| Delete remote branch | `git push <remote> --delete <branch-name>` |
| Prune unreachable branches | `git fetch --all --prune` |
| Delete local branches which have remote status *gone* | `git branch --v \| grep "\[gone\]" \| awk '{print $1}' \| xargs git branch -D` |
| Cleanup unnecessary files and optimize the local repository | `git gc` |

### Rename a branch

```bash
# Checkout branch to be renamed
git checkout <branch-to-rename>

# Rename local branch
git branch -m <new-branch-name>

# Local branch is renamed. If old branch name was previously pushed to remote
# do the following to rename remote branch

# Push new branch, resetting tracking branch to it
git push origin -u <new-branch-name>

# Delete the old branch from remote
git push origin --delete <branch-to-rename>
```

## Local Workspace commands

| Action | Command |
| ------ | ------- |
| Show current current branch and modified/staged files | `git status` |
| Stage file to be committed | `git add <file>` |
| Unstage file, retaining file changes | `git reset <file>` |
| Diff current branch with other branch | `git diff <other-branch>` |
| Diff current branch with other branch, showing only filenames | `git diff --name-only <other-branch>` |
| Diff file on two different branches | `git diff <branch1>..<branch2> -- <path/to/file>` |
| Diff modified file(s) | `git diff [file]` |
| Diff staged files| `git diff --staged` |
| Commit staged files | `git commit -m "Some message"` |
| Commit staged files, edit and use file for message | `git commit -eF ~/gitmsg.txt` |
| List untracked files | `git ls-files --others --exclude-standard` or `git status -u` |
| List ignored files | `git status --ignored` or `git check-ignore *` |
| Cherry pick source-commit onto dest-branch | `git checkout <dest-branch> && git cherry-pick <source-commit>` |

## Sync'ing up with remote/server repo

| Action | Command |
| ------ | ------- |
| Fetch remote changes | `git fetch <remote-alias>` |
| Fetch all remote changes from all remotes  | `git fetch --all` |
| Merge remote branch into current branch | `git merge <remote-alias>/<branch-name>` |
| Push local commits to remote branch | `git push <remote-alias> <branch>` |
| Fetch *and* merge remote changes | `git pull` |

## Viewing History

| Action | Command |
| ------ | ------- |
| Show detailed commit history for current branch | `git log` |
| Show information for last commit on current branch | `git log -1` |
| Show minimal commit history for current branch | `git log --oneline` |
| Show entire commit tree for curent branch | `git log --oneline --graph --decorate` |
| Show entire commit tree for all branches | `git log --all --oneline --graph --decorate` |
| Show commits containing file moves | `git log --stat -M` |
| Show commit history for a single file |  `git log --follow --pretty=format:"%h %ad \| %an \| %s" --date=short -- <path_to_file>` |

## Moving or Removing files

| Action | Command |
| ------ | ------- |
| Delete file from git and workspace | `git rm <file>` |
| Delete file from git, keep in workspace | `git rm <file> --cache` |
| Delete directory from git and workspace | `git rm -r <dir>` |
| Move file in git and workspace | `git mv <existing-filename> <new-filename>` |

## Dealing with merge conflicts

| Action | Command |
| ------ | ------- |
| Launch mergetool (configured in gitconfig) | `git mergetool` |
| Abort merge | `git merge --abort` |

## Undoing things

| Action | Command |
| ------ | ------- |
| Un-stage a file *(file will remain modified)* | `git reset HEAD <file>` |
| Un-do changes to a modified file | `git checkout -- <file>` |
| Un-do changes to all modified files *(untracked files are unaffected)* | `git reset --hard` |
| Clean untracked files and directories | `git clean -f -d` |
| Clean ignored files | `git clean -x` |
| Revert the last commit (create another commit that does the opposite of last commit) | `git revert HEAD` |
| Delete the last commit (and changes) like it never happened | `git reset --hard HEAD^` |
| Delete the last commit but keep the changes in my workspace | `git reset HEAD^` |
| Fix the last commit message | `git commit --amend` |
| Change author/email on last commit message | `git commit --amend --author="Firstname Lastname <email@address.com>"` |

## Tagging

| Action | Command |
| ------ | ------- |
| Create Lightweight tag | `git tag <label>` |
| Create Annotated tag | `git tag -a <label> -m "Some message"` |
| List tags | `git tag` |
| List tags, displaying annotations (1st line only) | `git tag -l -n` |
| List tags, displaying annotations (3 lines) | `git tag -l -n3` |
| Filter list tags (beginning with 'v1.1.') | `git tag -l 'v1.1.*'` |
| Display tag details | `git show <label>` |
| Delete local tag | `git tag -d <label>` |
| Delete remote tag | `git push <remote-alias> :<label>` (note the : in front of the label) |
| Publishing single tag | `git push <remote-alias> <label>` |
| Publishing all tags | `git push <remote-alias> --tags` |
| Editing local tag | `git tag -a -f <label> <commid-id>` |
| Editing remote tag | Edit local tag, then `git push <remote-alias> -f --tags` |

## Temporary Commits

| Action | Command |
| ------ | ------- |
| Save modified and staged changes | `git stash` |
| List stack of stashed changes | `git stash list` |
| Show files in (latest or named) stash | `git stash show` or `git stash show stash@{0}` |
| Show changes in (latest or named) stash | `git stash show -p` or `git stash show -p stash@{0}]  # named` |
| Retrieve most recent stashed changes | `git stash pop` |
| Delete most recent stashed changes | `git stash drop` |

## Submodules

| Action | Command |
| ------ | ------- |
| Clone a repo that contains submodules | `git clone --recursive <url-to-repo>` |
| Get submodules for a repo already cloned | `git submodule update --init` |
| Get nested submodules for a repo already cloned | `git submodule update --init --recursive` |

## Additional Resources

- [Git cherry pick | Atlassian](https://www.atlassian.com/git/tutorials/cherry-pick) - A tutorial on using git cherry pick
- [Git User Manual](https://git-scm.com/docs/user-manual)
- [Git pretty - so you have a mess on your hands](https://east.fm/refcards/git/git-pretty.pdf)
- [Oh Shit, Git!?!](https://ohshitgit.com/)
- [Git Flow: A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model/) - No longer recommended.
- [Github Forks](https://help.github.com/en/github/getting-started-with-github/fork-a-repo)
- [releaseflow](http://releaseflow.org/) - The trendy name for the Release Branching strategy
