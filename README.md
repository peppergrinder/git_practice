# git & GitHub - HowTo

[codecademy-course](https://www.codecademy.com/learn/learn-git/modules/learn-git-git-backtracking-u/cheatsheet)

[cheatsheet-edu](/resources/pdf/git-cheat-sheet-education.pdf)

[cheatsheet](https://www.codecademy.com/resources/docs/git/pull)

| Command                               | Description   |
|---------------------------------------|-------------|
| `git -h` | general help |
| `git help -a` | detailed help |
| `git branch -h` | help on branches |
| `git config --edit` | edit your config file |
| `git config -l --show-origin` | list of config options and their locations |
| `git config --edit --global` | edit your global config file |

## Generalizations

| Command                               | Description   |
|---------------------------------------|-------------|
| `git init` | creates a new Git repository. |
| `git add` | adds files from the working directory to the staging area. |
| `git add filename_1 filename_2` | add more files to stage. |
| `git add .` | add all files from WorkingDir to stage. |
| `git status` | inspects the contents of the working directory and staging area. |
| `git commit -m "commit msg"` | permanently stores file changes from the staging area in the repository. |
| `git log` | shows a list of all previous commits. |

## Contents

+ [Visual Studio Code integration](#git-integration-visual-studio-code-and-first-time-setup)
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
+ [Forking](#forking)
  + [Forking steps](#forking-steps)
+ [git rebase](#rebase)
+ [gitignore](#gitignore)
+ [GitHub Features](#github-features)
  + [GitHub Issues](#github-issues)
  + [GitHub CLI](#github-cli-gh)
  + [GitHub Actions](#github-actions)
  + [GitHub Codespaces](#github-codespaces)
  + [GitHub.dev](#githubdev)
  + [GitHub Project Management](#github-project-management)
  + [Conclusion](#conclusion)
+ [Privacy, Security, and Administration](#privacy-security-and-administration)
  + [Managing GitHub Personal Access Tokens](#managing-github-personal-access-tokens)
  + [Different Types of GitHub Personal Access Tokens](#different-types-of-github-personal-access-tokens)
  + [How to Create Personal Access Tokens in GitHub](#how-to-create-personal-access-tokens-in-github)
  + [GitHub Enterprise Managed Users](#github-enterprise-managed-users)
    + [Features of GitHub EMU](#features-of-github-emu)
    + [Major Differences Between GitHub.com and GitHub EMU Accounts](#major-differences-between-githubcom-and-github-emu-accounts)
  + [GitHub Copilot](#github-copilot)

## Git integration Visual Studio Code and first-time setup

```zsh
git --version
git config --global --list
git config --global user.name "UserName"
git config --global user.email "your@email.com"
git config --global merge.tool vscode # needed for VSC to sync
git config --global mergetool.vscode.cmd 'code --wait $MERGED' # needed for VSC to sync
```

## Create a new git repository

```zsh
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
| ------------------------------------- | ------------- |
| `git remote add origin https://github.com/YOURREPO` | link to your empty repo on GitHub. |
| `git push -u origin main` | push changes to GitHub (`-u`, `--set-upstream` is optional). |
| From here you can: |  |
| `git pull origin main`    | Pull changes from origin |
| `git push`        | Since origin is set, we can simply push |

## GitHub Flow

1. Work on a specific branch
2. Commit changes and push code to remote repo
3. Create pull request
4. Discuss pull request with reviewers
5. Merge branch once pull request accepted (and delete branch)

## GitHub steps to create and merge pull requests

1. Submit pull request with description
2. Make changes from feedback
3. Merge code

## Branches

| Command                               | Description   |
| ------------------------------------- | ------------- |
| `git branch` | show all branches |
| `git branch new-branch`     | Create a new branch "new-branch" |
| `git checkout new-branch`   | switch to branch "new-branch" |
| --- | --- |
| `git checkout main`         | switch to branch "main" |
| `git merge new-branch`      | this will add the changes from "new-branch" into the current ("main") branch |
| `git branch -d new-branch`  | deleting branch "new-branch" - good practice to delete after merge into main |

## HEAD commit

| Command                       | Description   |
|-------------------------------|---------------|
| `git show HEAD`               | display everything the git log command displays for the HEAD commit, plus all the file changes that were committed. |
| `git checkout HEAD filename`  | restore the file in your working directory to look exactly as it did when you last made a commit. |
| `git checkout -- filename`    | shortcut - for above. |

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

## git reset II (and force-push to GitHub after)

| Command                               | Description   |
|---------------------------------------|---------------|
| `git reset commit_SHA`                | This command works by using the first 7 characters of the SHA of a previous commit (git reset 5d69206). |
| `git reset 5d69206 --hard`            | hard reset might be needed.  |
| `git push -f origin main`             | force push your reset to GitHub (Your branch is behind 'origin/main' by 1 commit,...) |

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
| `git push origin your_branch` | push changes to origin into branch `your_branch`. |

## [Forking](https://www.codecademy.com/courses/learn-git/articles/forking-a-repository-tutorial)

A fork is a duplicate of an existing repository. This "fork” is an independent entity that allows a contributor to interact with the original repository. Collaboration, experimentation, and contributions to open-source code are made possible by forking. It enables developers worldwide to collaborate, make changes, and contribute to projects while retaining the integrity of the source code. It is a secure approach to modify and test code without making changes directly to the original.

### Forking steps

1. In your browser, go to the repo you wish to fork.
2. Hit 'Fork' top right, and add a clone to your GitHub space.
3. Now you can download this repo to your computer like any other using `git clone`.
    + (Fork to directory `/forks` on your machine to keep things organised)
4. Set upstream in order to receive updates from parent
    + shell: cd into your clone
    + get parent's `https` key -> `git remote add upstream https://github.com/parentRepo.git`
5. Fetch upstream: `git fetch upstream'
    + Compare number of commits on parent with your clone.

| Command                               | Description   |
|---------------------------------------|---------------|
| `git clone https://github.com/...` | Clone your fork locally. |
| `git remote -v` | See that the original repo forked from does not exist yet. |
| `git remote add upstream https://github.com/...` | accepts updates from original repo. |
| `git fetch upstream` | fetches updates from original branches. |
| `git merge upstream/main main` | Merge changes from upstream branch 'main' to your local 'main' branch. |

To add your origin permanently you can add it to `git config --edit` under `[core]` in **`[checkout]`**:

```json
[core]
        repositoryformatversion = 0
        filemode = true
        bare = false
        logallrefupdates = true
        ignorecase = true
        precomposeunicode = true
[checkout]
        defaultRemote = origin
[remote "origin"]
        url = ...
```

## rebase

Git rebase is an important feature for collaborating effectively in a development team. Using git rebase, you can keep your branches up to date with the most recent changes while keeping your in-progress changes isolated!

| Command                               | Description   |
|---------------------------------------|---------------|
| `git rebase main` | rebase your current branch to main. |

## gitignore

[GitHub's gitignore repository](https://github.com/github/gitignore)

| Command                               | Description   |
|---------------------------------------|---------------|
| `find . -name .DS_Store -print0 \| xargs -0 git rm --ignore-unmatch` | find and remove all .DS_Store files including subfolders (`-f` at end might be required). |
| `git rm --cached .DS_Store` | manually remove .DS_Store files. |
| --- | --- |
| `echo .DS_Store >> .gitignore` | create a local `.gitignore`. (watch for correct directory) |
| `git config --global core.excludesfile .gitignore_global` | link a global `.gitignore_global`. (p.e. in GitHub directory on your pc / needs to exist prior) |
| `git config --global core.excludesfile` | shows the name of your global `.gitignore`. |
| --- | --- |
| `node_modules/` | ignore the node_modules directory, and all subdirectories and files inside. |
| `*.html` | ignore all `.html` files. |
| `example*` | ignore all any files starting with `example`. |
| `!` | Negation |
| Negation | --- |
| `index*` | will ignore all files starting with `index` except for `src/index.css`. |
| `!public/index.css` | but, we cannot negate a file inside an ignored directory. |
| Range | - [] - |
| `[a-z], [A-Z], [0-9]` | match a single character from a set of characters or a range of characters. |
| `**` | match 0 or more directories. |
| `**/temp/*.log` | match all `.log` files in all `temp` directories and sub-dirs in root-dir. |
| `v[1-3]/**/*.log` | match all `.log` files in `v1, v2, v3` directories and sub-dirs. |

---

## GitHub Features

### GitHub Issues

GitHub Issues adds project management right to your repository. You can list tasks and organize them into which are open and in progress. These issues can also be referenced in pull requests and even other issues.
![Issues Board](resources/issues-board-docs.webp)

The issue board acts as a forum for all the collaborators of the repository. In some instances, issue boards are public and users of a project can submit and discuss bugs they've encountered.

#### Labels

To help organize issues when more and more pop up in a project, we can use labels. bug and feature are common labels used to differentiate between errors and new features. In the Codecademy Docs repo Issue board earlier, we could see labels such as Good first issue, if a suggested entry to Docs is new or an edit, and what language the entry should be in, like C# or Java. Labels help us toggle between different types of issues at a glance and have short names.

#### Creating an Issue

To create an Issue, we can click the New Issue button on top of the Issues board. This will take us to a new page where to set the title and content of the issue.

Issues are a bit like pull requests in that we want to keep the title specific but to the point. For descriptions, repositories often have their own guidelines (just like pull requests do) for including details. For example, if the issue is related to a bug, we should include the error message in the description. Check out a complete issue from the Facebook Folly repository:
![Completed Issue](resources/completed-issue.webp)
Once the issue is posted and now open, collaborators and other GitHub users can add to the discussion and reference this issue by the # in other issues and pull requests.

---

### GitHub CLI (gh)

The GitHub Command Line Interface (CLI) is a tool that allows you to directly access and. modify issues and pull requests right from your terminal!

`brew install gh`

#### [Installation](https://github.com/cli/cli#installation)

Download and execute the installer for your operating system from the GitHub CLI public webpage. Once the installation is complete, open a new terminal and verify the default configuration:
`gh --version`

Review the list of the supported APIs and functionalities:

| Command                               | Description   |
|---------------------------------------|---------------|
| `gh --help`      | General help     |
| `gh auth --help` | Learn about auth |
| `gh auth status` | Check auth status |
| `gh auth login` | Login to GitHub from your terminal |

#### GitHub CLI in action

[Fork the try-GitHub-cli-off-platform-project](https://github.com/Codecademy/try-github-CLI-off-platform-project) repository to your GitHub account and clone it onto your local computer. Next, open a terminal and change the current directory to the directory of the cloned repository.

The repository contains a simple Python application for a Magic Eight Ball. The application, however, has a defect. The code tries to use the Python random library without importing it.

Login to GitHub from your terminal using GitHub CLI and follow the instructions to complete the authentication.
`> gh auth login`

```zsh
taaroth4@TRoMBProM2Pro Off-platform-proj % gh auth login
? Where do you use GitHub? GitHub.com
? What is your preferred protocol for Git operations on this host? HTTPS
? Authenticate Git with your GitHub credentials? Yes
? How would you like to authenticate GitHub CLI? Login with a web browser

! First copy your one-time code: B41C-26C4
Press Enter to open https://github.com/login/device in your browser...
✓ Authentication complete.
- gh config set -h github.com git_protocol https
✓ Configured git protocol
✓ Logged in as peppergrinder
```

View issues: `gh issue status`

If running into this: `X No default remote repository has been set for this directory.`

run this: `gh repo set-default`

```zsh
% gh repo set-default
This command sets the default remote repository to use when querying the
GitHub API for the locally cloned repository.

gh uses the default repository for things like:

 - viewing and creating pull requests
 - viewing and creating issues
 - viewing and creating releases
 - working with GitHub Actions
 - adding repository and environment secrets

? Which repository should be the default? Codecademy/try-github-CLI-off-platform-project
✓ Set Codecademy/try-github-CLI-off-platform-project as the default repository for the current directory
```

Check on issues again

```zsh
% gh issue status

Relevant issues in Codecademy/try-github-CLI-off-platform-project

Issues assigned to you
  There are no issues assigned to you

Issues mentioning you
  There are no issues mentioning you

Issues opened by you
  There are no issues opened by you
```

Use the command line to create a GitHub Issue documenting the problem:

```zsh
> gh issue create --title "Fix magic8.py error" --body "The code for magic8.py uses the Python random library without importing it. This causes issues during runtime."
```

Follow the instructions in the terminal and select the forked repository to create the issue.
![Create issue](resources/github-CLI-create-issue.webp)
Once the issue is created, you can view it on GitHub web interface under the Issues tab.
![Resulting issue](resources/GitHub_Off-platform-issue-1583.png)
You can also use GitHub CLI to list all opened issues so far:

```zsh
Off-platform-proj % gh issue status

Relevant issues in Codecademy/try-github-CLI-off-platform-project

Issues assigned to you
  There are no issues assigned to you

Issues mentioning you
  There are no issues mentioning you

Issues opened by you
ID       TITLE                LABELS  UPDATED            
  #1583  Fix magic8.py error          about 4 minutes ago
```

Let's now create a new branch to actually fix the issue.

```zsh
% git checkout -b "fix-magic8" 
Switched to a new branch 'fix-magic8'
```

Open the magic8.py file using an editor of your choice and add the following line at the beginning of the file to fix the defect:

```Python
import random
```

Commit and push your change to the remote.

```shell
git commit -a -m "Fixed magic8.py file by importing the proper required library"
git push --set-upstream origin fix-magic8
```

Now that there's a full solution to the problem in your branch, it's time to create a pull request! You can use the command line to directly make a pull request:

`gh pr create`

Follow the prompts and add the proper title and description for the pull request. Mention the id of the issue in the description following #[id] format so that GitHub automatically links the pull request to the issue.
To check if this actually worked, you can check that the new pull request appears under the Pull Requests tab. Also, observe the state of the issue and see that the issue is now linked to the pull request.
![Fix magic8.py error #1581](resources/FixMagic8.py_error.png)

Assuming that your pull request is good to go, you can merge your pull request using the following GitHub CLI command:

```zsh
gh pr merge
Merging pull request Codecademy/try-github-CLI-off-platform-project#1584 (Fix magic8.py error #1583)
? What merge method would you like to use?  [Use arrows to move, type to filter]
> Create a merge commit
  Rebase and merge
  Squash and merge
```

> Error: GraphQL: peppergrinder does not have the correct permissions to execute `MergePullRequest` (mergePullRequest)
> Check the next excercise, where you fork a repo and update your GitHub fork version. Here merging is not a problem.

Once the pull request is merged, check back the status of the issues and notice that the issue is now closed and no longer listed under the open issues:
`gh issue status`

---

### GitHub Actions

Want to add automated tests after a pull request is created? Want to trigger something after a branch is merged into main? We can use GitHub Actions!

GitHub Actions is a powerful, advanced GitHub feature that enables users to define custom and automated workflows triggered on various types of events such as pushing code or creating a pull request. The workflows execute inside a temporary container running in GitHub infrastructure.
[Use cases](https://docs.github.com/en/actions/use-cases-and-examples)
[Writing workflows](https://docs.github.com/en/actions/writing-workflows)
[Actions Marketplace](https://github.com/marketplace?type=actions)

#### Simple Workflow Example

```YAML
# This is a basic workflow to help you get started with Actions
name: sample_worflow
# Controls when the workflow will run
on:
  # Triggers the workflow on push or pull request events but only for the "main" branch
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]
  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:
# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
  # This workflow contains a single job called " sample_job "
  sample_job:
    # The type of runner that the job will run on
    runs-on: ubuntu-latest
    # Steps represent a sequence of tasks that will be executed as part of the job
    steps:
      # Checks-out your repository under $GITHUB_WORKSPACE, so your job can access it
      - uses: actions/checkout@v4
      # Runs a single command using the runner's shell
      - name: first_step
        run: echo  You are at Codecademy.
      # Runs a set of commands using the runner's shell
      - name: second_step
        run: |
          echo You are learning GitHub Actions.
          echo It is fun to learn programming at Codecademy!
```

---

### [GitHub Codespaces](https://www.codecademy.com/courses/learn-git/articles/getting-started-with-github-codespaces)

GitHub Codespaces offers a cloud-based, on-demand development environment within GitHub.

GitHub Codespaces is a platform that allows us to create and manage development environments within GitHub. It helps us create a virtual environment, code in the cloud, and commit the code back to the GitHub repository without worrying about setting up or managing the environment for the project.

With GitHub Codespaces, we can create a fully configured, containerized development environment with all the tools and dependencies needed for our project with only a few clicks.

[Codespaces Homepage](https://github.com/codespaces)

#### GitHub Codespaces lifecycle

+ Creation
+ Active Development
+ Timeout
+ Rebuilding
+ Stopping
+ Deleting

#### Customizing GitHub Codespaces

##### Renaming Codespaces

To rename go to: [GitHub codespaces Homepage](https://github.com/codespaces)
![Rename Codespace](resources/GitHub_Codespace_rename.png)

#### Change machine type for Codespaces

Within same contextual menu as above.

#### Customizing the Command Line Terminal in GitHub Codespaces

To customize the appearance of the terminal, click on the bash icon above the terminal. This gives us different options, such as changing the color and icon to customize the terminal.

We can also change the shell for the terminal. By default, GitHub Codespaces come with the bash, zsh, and fish shells installed.

To change the shell in a terminal, click on the dropdown arrow beside the + button above the terminal. This gives us a menu from which to select a shell.

![Change shell](resources/GitHub_Codespace_shell.png)

#### Configuring Default Timeout and Codespaces Retention Time

By default, a GitHub Codespace is timed out after 30 minutes and stopped. The retention period of a stopped Codespace is 30 days, after which it is permanently deleted.

Visit: [GitHub-Settings](https://github.com/settings/). From there go to the section: "Code, planning, and automation". From here go to [Codespaces](https://github.com/settings/codespaces).
Here we get sections on Default idle timeout, Region settings and Default retention period.

---

### GitHub.dev

GitHub.dev is a lightweight, web-based code editor provided by GitHub. It allows us to make quick edits to files in GitHub repositories directly in the browser, without the need to clone the repository to a local development environment.

First, sign in to your GitHub account. After signing in, open GitHub.dev for any repository you have. To do this, go to the repository homepage.

We can open the GitHub.dev editor for the repository by one of the following ways:

+ Replace .com with .dev in the repository URL.
+ Press the period key `.` on the repository page.
+ Press `Shift` and `.` keys on the repository page. (opens in new tab)

#### GitHub.dev limitations

+ No terminal
+ Limited support for extensions

#### GitHub Codespaces vs GitHub.dev

| Aspect      | GitHub Codespaces   | GitHub.dev |
|-------------|---------------------|------------|
| Availability | Available to everyone on GitHub.com with free monthly quota for personal accounts.| Available to everyone on GitHub.com for free.|
| Compute     | A dedicated virtual machine is assigned to each Codespace on which we can run our code. | The editor runs in the local browser and there is no compute facility available. |
| Start up    | When we create a Codespace, a virtual machine is assigned and configured. This can take up to a few minutes. | GitHub.dev editor opens instantly in the browser, and we can start using it without having to wait for any configuration. |
| Terminal access | We get terminals with shell options like bash, zsh, and fish to execute commands on the assigned virtual machine. | There is no terminal support. |
| Extensions  | We can install and use most extensions in Codespaces that we use in a VS Code IDE installed on a local computer. | We can install extensions. However, their functionalities are restricted. |

---

### GitHub Project Management

GitHub projects is a beta feature (as of late 2021) for project management. While other project management tools exist, like JIRA or even handwritten post-its, GitHub projects allow direct integration within the repository, letting developers stay within the same ecosystem. We can also create automated project boards that trigger the status of issues and pull requests. And… it's completely free!

To try out projects, we can select the New Project option after clicking the + button on the upper right side of the GitHub dashboard. In most cases, projects are linked to repositories, which already have existing issues and pull requests, but in other cases, projects can be standalone.
![New Project](resources/new-project.webp)
After filling out the name and description of the new project, a drop-down will appear asking what Project template we want to use.
![Project types](resources/project-types.webp)
The options range from different types of Kanban boards that can host issues and pull requests to a Bug Triage, which gives details into which bugs are high priority, low priority, or need further investigation. Once the board is created, we will [add issues and pull requests](https://docs.github.com/en/issues/organizing-your-work-with-project-boards/tracking-work-with-project-boards/adding-issues-and-pull-requests-to-a-project-board) to it.

An example of a laid-out GitHub project board is [Github's own public roadmap project](https://github.com/orgs/github/projects/4247/views/1), shown next. This is an example of a Project with no repository, as a roadmap can be used for organizational purposes.
![GitHub Project Board](resources/github-project-board.webp)

### Conclusion

We learned about two GitHub features that can come in handy for teams: issues and projects. We can use GitHub issues to keep track of tasks that need to be worked on. Those issues can then be referenced in pull requests, comments, or projects. GitHub projects are an even newer feature for project management purposes and can be linked to repositories. We can choose from a variety of different board types to organize tasks.

## Privacy, Security, and Administration

### Managing GitHub Personal Access Tokens

Personal access tokens are a great utility for secured and controlled access to GitHub repositories.
GitHub personal access tokens are authentication tokens that allow us to access GitHub's API and manage repositories through command-line applications without using a password.

Personal access tokens provide a more secure and flexible way to integrate with GitHub. We can create specific tokens for dedicated tasks and revoke them individually if needed. These are particularly useful for automating workflows, accessing protected resources, and managing repository access programmatically.

### [Different Types of GitHub Personal Access Tokens](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens)

+ Classic personal access tokens are an alternative to using passwords for authentication, offering more security and flexibility.
+ Fine-grained personal access tokens in GitHub are an enhanced version of classic personal access tokens, offering more precise control over permissions and access.

### How to Create Personal Access Tokens in GitHub

To create personal access tokens in GitHub, go to your GitHub dashboard and click on the profile image in the top-right corner of the page. Click on `Settings` and go to `Developer settings` at the bottom left.
![Developer Settings](resources/GitHub_DevSettings.png)

### GitHub Enterprise Managed Users

GitHub for Enterprises is a version of GitHub designed specifically for companies and large organizations. It offers enhanced security, compliance, and administrative controls tailored to meet the needs of enterprise environments.

GitHub for enterprises is ideal for organizations that require more stringent data governance, collaboration across large, distributed teams, and customized workflows.

#### Features of GitHub EMU

+ Centralized user management: EMUs directly integrate with enterprise identity providers like Google and Azure Active Directory. This allows us to manage user identities, access permissions, and authentication through our existing systems in the company. EMUs also eliminate the need for personal GitHub accounts.
+ Automated provisioning and de-provisioning of user accounts: As the user accounts in GitHub EMU are tied to company accounts, they are automatically created or revoked through the company's identity management system. This helps us ensure that only authorized users have access to the codebase and reduces the risk of orphaned accounts.
+ Role-based access control: EMUs allow us to have granular control over user roles and permissions. This makes it easier for us to control who can view, edit, and manage repositories and other resources within the organization, resulting in strict adherence to security and compliance policies.
+ Enhanced security and compliance: EMUs provide detailed auditing and monitoring capabilities. They allow us to track user activities, access logs, and changes across the company's GitHub environment, aiding in security and compliance efforts.

#### Major Differences Between GitHub.com and GitHub EMU Accounts

| Aspect      | GitHub.com          | GitHub EMU |
|-------------|---------------------|------------|
| Account Management | We can create and manage our own personal GitHub accounts. We can join multiple organizations and contribute to both public and private repositories using the same account. | The company manages user accounts through a centralized identity provider. We cannot contribute to any other organization or public repository through a GitHub EMU account. |
| Access Control | We control our access settings and manage our repositories. Organizations can set permissions for members in their repositories, but we retain control over our accounts. | The company has complete control over access permissions. All user permissions, including account access, can be managed centrally by the administrator. |
| Security & Compliance | Security and compliance are managed at the user level. Companies can set policies for their specific repositories and teams. However, we are responsible for managing the security of our accounts. | Security and compliance are enforced at the organizational level. Our activities are tied to the company account. This ensures that all actions are compliant with the company's security policies. |
|Audit and Monitoring | Companies have access to audit logs for activities within their repositories, but they cannot track our actions outside their repository. | The organization has comprehensive audit and monitoring capabilities across all user activities as all actions are tied to the enterprise-managed account. |
| Repository ownership and control | We can create personal repositories that we fully control. Organizations have control over repositories created by them but not over personal repositories of the members. | All repositories are owned and controlled by the company. There are no personal repositories, ensuring that all intellectual property remains within the organization's control. |

Apart from the above differences, there are other abilities and restrictions on GitHub EMUs compared to GitHub.com accounts that you can check out [here](https://docs.github.com/en/enterprise-cloud@latest/admin/managing-iam/understanding-iam-for-enterprises/abilities-and-restrictions-of-managed-user-accounts).

---

## [GitHub Copilot](https://www.codecademy.com/learn/learn-git/modules/github-copilot-learn-git/cheatsheet)

### Key Features of GitHub Copilot

+ Autocompletion: Predictive Coding Based on Context
+ Code Generation: Turning Comments into Code
+ Multi-Language Support: Understanding and Aiding in Multiple Programming Languages
+ Inline Documentation: Offering Suggestions and Explanations for Code Snippets

### Benefits of Using GitHub Copilot

+ Enhancing Developer Productivity and Efficiency
+ Reducing the Likelihood of Errors
+ Assisting in Learning and Understanding New Code Patterns and Languages
+ Reducing Onboarding Time for New Team Members

### Potential Concerns & Limitations

+ Concerns About Code Originality and Licensing
+ Copilot's Limitations in Creative Problem-Solving and Unconventional Tasks
+ Understanding Copilot's Occasional Inaccuracies

### [Setting Up GitHub Copilot](https://www.codecademy.com/courses/learn-git/articles/setting-up-git-hub-copilot)

### Keyboard Shortcuts

GitHub Copilot offers a set of keyboard shortcuts to further enhance your productivity. These shortcuts are specific to Copilot within Visual Studio Code. Some essential shortcuts include:

+ Toggle Copilot Suggestions: Use `Ctrl+Space` (Windows/Linux) or `Cmd+Space` (macOS) to toggle Copilot suggestions on and off.
+ Accept Suggestion: Press `Tab` or `Enter` to accept the currently highlighted suggestion.
+ Show Documentation: Press `Ctrl+ Shift+ H` (Windows/Linux) or `Cmd+ Shift+ H` (macOS) to display documentation for the current code.

### Integration with Testing

To make up for some of Copilot's shortcomings, consider using it conjunction with testing frameworks to maintain code quality and security:

+ Use Copilot to write unit tests for your code. This ensures that the code functions as intended and helps catch regressions.
+ Copilot can assist in generating test cases for various scenarios, aiding in comprehensive testing.
+ Monitor code coverage to ensure that all critical code paths are tested thoroughly.

---

## Review

These are all the skills we've practiced:

+ Create a Git project and setup a remote copy on GitHub. Label code changes and move between different versions of your project.
+ Write text on the GitHub interface using Markdown to describe your project and code changes.
+ Create branches in your Git project so you can collaborate with others.
+ Use Git commands to make sure your local copy of code matches the remote copy on GitHub.
+ Use GitHub pull requests to discuss code changes with others.
+ Be familiar with Git rebase, GitHub repository settings, and how to keep a remote repository organized.
+ Create a GitHub profile and explore code written by others
+ Be familiar with intermediate to advanced GitHub features that allow you manage tasks within GitHub itself and automate actions.
+ Use GitHub Copilot to simplify complex coding tasks.
+ Use GitHub Copilot to enhance productivity.
+ Use GitHub Copilot to streamline your workflow.
