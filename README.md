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
