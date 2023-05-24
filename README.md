# git & GitHub - HowTo
[codecademy-course](https://www.codecademy.com/learn/learn-git/modules/learn-git-git-backtracking-u/cheatsheet)

[cheatsheet](https://www.codecademy.com/resources/docs/git/pull)

| Command                               | Description   |
|---------------------------------------|-------------|
| `git -h` | general help |
| `git help -a` | detailed help |
| `git branch -h` | help on branches |

## Generalizations
| Command                               | Description   |
|---------------------------------------|-------------|
| `git init` | creates a new Git repository. |
| `git add` | adds files from the working directory to the staging area. |
| `git add filename_1 filename_2` | add more files to stage. |
| `git add .` | add all files from WorkingDir to stage. |
| `git status` | inspects the contents of the working directory and staging area. |
| `git commit` | permanently stores file changes from the staging area in the repository. |
| `git log` | shows a list of all previous commits. |

# Contents
+ [Create a new git repository](#create-a-new-git-repository)
+ [Add existing code to empty GitHub repo](#add-existing-code-to-empty-github-repo)
+ [GitHub Flow](#github-flow)
+ [Create and merge pull requests](#github-steps-to-create-and-merge-pull-requests)
+ [Branches](#branches)
+ [HEAD commit](#head-commit)
+ [git diff, log](#git-diff-log)
+ [git reset](#git-reset-i-un-stage)
+ [git stash](#git-stash)
+ [Clone from remote](#clone-from-remote)
+ [git rebase](#rebase)
+ [gitignore](#gitignore)

## Create a new git repository
```
$ git init
Initialized empty Git repository in /home/user/new-project/.git/
$ echo "Hello World!" >> hello.txt
$ git add hello.txt 
$ git commit -m 'initial commit'
[main (root-commit) bb0e565] initial commit
 1 file changed, 1 insertion(+)
 create mode 100644 hello.txt
$ git branch
* main
```

## Add existing code to empty GitHub repo
| Command                               | Description   |
|---------------------------------------|-------------|
| `git remote add origin https://github.com/YOURREPO` | link to your empty repo on GitHub. |
| `git push -u origin main` | push changes to GitHub (`-u`, `--set-upstream` is optional). |

## GitHub Flow
1.	Work on a specific branch
2.	Commit changes and push code to remote repo
3.	Create pull request
4.	Discuss pull request with reviewers
5.	Merge branch once pull request accepted (and delete branch)

## GitHub steps to create and merge pull requests
1.	Submit pull request with description
2.	Make changes from feedback
3.	Merge code

## Branches
| Command                               | Description   |
|---------------------------------------|---------------|
| `git branch` | show all branches |
| `git branch new-branch` | Create a new branch "new-branch" |
| `git checkout new-branch` | switch to branch "new-branch" |
| --- | --- |
| `git checkout main` | switch to branch "main" |
| `git merge new-branch` | this will add the changes from "new-branch" into the current ("main") branch |
| `git branch -d new-branch` | deleting branch "new-branch" - good practice to delete after merge into main |

## HEAD commit
| Command                               | Description   |
|---------------------------------------|---------------|
| `git show HEAD` | display everything the git log command displays for the HEAD commit, plus all the file changes that were committed. |
| `git checkout HEAD filename` | restore the file in your working directory to look exactly as it did when you last made a commit. |
| `git checkout -- filename` | shortcut - for above. |

## git diff, log

| Command                               | Description   |
|---------------------------------------|---------------|
| `git diff fileName` | check for differences between your file and the last commit. |
| `git log -S "keyword"` | filter log for "keyword" |
| `git log --oneline` | log as 'one liner' |
| `git log --oneline --graph` | log as 'one liner' with branches graph |
| `git log --graph --decorate --oneline --all` | log extra options |

## git reset I (un-stage)
| Command                               | Description   |
|---------------------------------------|---------------|
| `git reset HEAD filename` | resets the file in the staging area to be the same as the HEAD commit. It does not discard file changes from the working directory, it just removes them from the staging area. |

## git reset II
| Command                               | Description   |
|---------------------------------------|---------------|
| `git reset commit_SHA` | This command works by using the first 7 characters of the SHA of a previous commit (git reset 5d69206). |

## git stash
| Command                               | Description   |
|---------------------------------------|---------------|
| `git stash -h` |  |
| `git stash` | save working dir to shash (locally) |
| `git branch xyz_123` | create new branch "xyz_123" |
| `git checkout xyz_123` | switch to other branch "xyz_123" |
| --- | --- |
| `git checkout main` | switch to main branch again |
| `git stash list` | show your stashes |
| `git stash pop` | bring back stash |

## Clone from remote

| Command                               | Description   |
|---------------------------------------|---------------|
| `git clone remote_location clone_name` | get your replica / clone_name is the name you give to the directory in which Git will clone the repository. |
| `git remote -v` | list remotes. |
| `git fetch` | fetch changes from origin. |
| `git merge origin/main` | merge fetched changes from origin to your "main" branch. |
| `git add filename` | add edited file "filename" to the stage. |
| `git commit -m "commit msg"` | commit changes to your local copy. |
| `git commit --amend --no-edit` | allows for editing previous commit, instead of creating a new one, while keeping the same commit message (--no=edit). |
| `git push origin your_branch` | push changes to origin into branch "your_branch. |

## rebase
Git rebase is an important feature for collaborating effectively in a development team. Using git rebase, you can keep your branches up to date with the most recent changes while keeping your in-progress changes isolated!

| Command                               | Description   |
|---------------------------------------|---------------|
| `git rebase main` | rebase your current branch to main. |

## gitignore
[GitHub’s gitignore repository](https://github.com/github/gitignore)

| Command                               | Description   |
|---------------------------------------|---------------|
| `find . -name .DS_Store -print0 \| xargs -0 git rm --ignore-unmatch` | find and remove all .DS_Store files including subfolders (`-f` at end might be required). |
| `git rm --cached .DS_Store` | manually remove .DS_Store files. |
| --- | --- |
| `echo .DS_Store >> .gitignore_global` | create a local `.gitignore`. (watch for correct directory) |
| `git config --global core.excludesfile **.gitignore_global**` | create a global `.gitignore`. (p.e. in GitHub directory on your pc) |
| `git config --global core.excludesfile` | shows the name of your global `.gitignore`. |
| --- | --- |
| `node_modules/` | ignore the node_modules directory, and all subdirectories and files inside. |
| `*.html` | ignore all `.html` files. |
| `example*` | ignore all any files starting with `example`. |
| `!` | ignore all any files starting with `example`. |
| Negation | --- |
| `index*` | will ignore all files starting with `index` except for `src/index.css`. |
| `!public/index.css` | but, we cannot negate a file inside an ignored directory. |
| Range | - [] - |
| `[a-z], [A-Z], [0-9]` | match a single character from a set of characters or a range of characters. |
| `**` | match 0 or more directories. |
| `**/temp/*.log` | match all `.log` files in all `temp` directories and sub-dirs in root-dir. |
| `v[1-3]/**/*.log` | match all `.log` files in `v1, v2, v3` directories and sub-dirs. |