# Version Management & Git

[TOC]

## Introduction

> *Git is a free and open source distributed version control system designed to handle everything from small to very large projects with speed and efficiency.*
>
> [Git (git-scm.com)](https://git-scm.com/)

Git is a distribute version control system designed to efficiently manage and track changes to files and directories.

## Architecture

<img src="assets/Git Diagram.svg" alt="Git Diagram" style="zoom: 33%;" />

* **Remote Repository**: A remote repository is a separate copy of the repository that exists on a remote server. It allows multiple developers to collaborate on the same project by sharing changes with each other. Developers can push their local commits to the remote repository and fetch or pull updates from it.
* **Local Repository**: The repository is the central component of Git and contains the complete history and metadata of the project. It is usually divided into two main parts:
  * Object Database: The object database stores all the data and content of the project's files. It uses a content-addressable storage model, where each file and version is identified by a unique SHA-1 hash. Git objects include blobs (file contents), trees (directory structures), commits (snapshots of the project at a specific point in time), and tags (named references to specific commits).
  * Reference Database: The reference database holds references to specific commits within the object database. It includes branch references, which are pointers to specific commits on a branch, and tags, which are human-readable names assigned to specific commits.

* **Staging Area**: is an intermediate area where changes to the project's files are prepared to be committed.
* **Working Directory**: is the directory on a developer's local machine where they make modifications to the project's files. It represents the current state of the codebase and includes all the files and directories.

### Command & Operations
- ***config***: Used to configure Git user information, text editor, etc.
  - ***--list***: list all Git configuration items.
  - ***--global*** user.name "Your Name": Set the global username.
  - ***--global*** user.email "your_email@example.com": Set up a global user mailbox.
- ***init***:  Creates & initializes a new Git repository in the current directory, generating a hidden .git directory for tracking version information.
- ***clone***: Create a copy of a remote repository on your local machine.
- ***status***: View the status of the workspace and staging area, and display information such as file modifications and untracked files.
- ***add***: Adds changes or new files to the staging area for the next commit.
- ***commit***: Records the changes mode to the repository and creates a new commit.
  - ***-m*** "commit message": Describing the content of this submission.
  - ***--amend***: Modify the most recent commit message or content, if some files are missing or the commit message is incorrect after committing.
- ***push***: Upload local commits to a remote repository.
- ***pull***: Fetches changes from a remote repository and merges them into the current branch.
- ***rm***: Removes files from the working directory and stages the removal.
- ***diff***: shows the differences between the working directory and the staging area or previous commit.
- ***fetch***: Download new commit records, branch information, etc. from the remote repository, but do not automatically merge these changes into the local branch. It just updates the latest status of the remote repository to the local remote tracking branch (such as origin/main), allowing you to view the new commits in the remote repository without affecting the local work progress.
- ***branch***: List all local branches. The current branch will be marked with an asterisk *.
  - <branch_name>: Create a new branch <branch_name>, but do not switch to the new branch.
  - ***-d*** <branch_name>: Delete the specified local branch.
- ***checkout***: Switch to the specified branch <branch_name>.
- ***merge***: Merge the specified branch into the current branch <branch_name>.
- ***rebase*** The purpose of organizing and linearizing the commit history is to apply a series of commits to another branch in order. It will "copy" the commits in the current branch and then apply these commits in sequence on the target branch to make the commit history look more linear.
- ***remote add***: Add a remote repository, <remote_name> is usually origin, and <remote_url> is the URL address of the remote repository.
- ***push***: Push the local specified branch to the remote repository.
- ***pull***: Pull the code of the specified branch from the remote repository and merge it with the local current branch.
- ***log***: View commit history, including commit hash, author, date, commit message, and more.
  - ***--pretty***=oneline: Displays the commit history in a concise one-line format.

### Merge branches: Rebase & Merge

<img src="./assets/rebase.svg" alt="rebase" style="zoom: 80%;" />

#### Rebase

***Rebase***: Apply the commits of the current branch to the top of the latest commit of the target branch in sequence to form a linear commit history.

- **Workflow**:
  - Locate common ancestor: find the most recent common ancestor commit of the current branch and the target branch
  - Extract modifications: convert all commits of the current branch after the common ancestor into patch files
  - Reset branch: point the current branch pointer directly to the latest commit of the target branch
  - Apply patch: reapply the extracted patch file in sequence
- **Conflict handling**:
  - Git suspends rebase and prompts conflicting files
  - Manually resolve conflicts (IDE visualization tools are recommended)
  - Execute git add <file> to mark the conflict resolved
  - Continue rebase: git rebase `--continue`
  - To terminate: git rebase `--abort`
- **Key features**:
  - Maintains the linear structure of the commit history
  - Often used to maintain the cleanliness of feature branches
  - Can be interactively edited via git rebase -i
  - Will change the SHA value of the commit

#### Merge

***Merge***: Create a new merge commit to integrate the history of two branches and keep the complete branch development track.

- **Workflow**:
  - Automatic merge: Git tries to intelligently merge the changes of two branches
  - Generate a merge commit: If the merge is successful, automatically create a commit with two parent nodes
  - Conflict handling: If there is a conflict, you need to manually resolve it before submitting it
- Conflict handling:
  - Git prompts conflicting files (marked with symbols such as <<<<<<<).
  - Manually edit conflicting files (it is recommended to use the merge tool of IDE)
  - Execute git add <file> after saving the changes
  - Complete the merge commit: git commit -m "Merge branch..."
- Key features:
  - Keep the complete branch history
  - Merge commit contains two parent nodes
  - Support three-way merge algorithm
  - Submit SHA value remains unchanged

### Undo: Revert & Reset

#### Reset

***reset***: Restore the status of the files in the staging area to the status of the last commit, that is, cancel the staging. If the <file> parameter is not added, git reset will restore all files in the staging area by default.

- ***--soft***: Only move HEAD to the specified commit, and the contents of the staging area and the work area will not be changed. That is, all changes are still kept in the staging area, and you can resubmit these changes.
- ***--mixed*** (Default mode): Move HEAD to the specified commit, and reset the staging area to make it consistent with the contents of the specified commit, but the contents of the work area will not be changed. That is, the previous git add operation is undone, and the changes are still kept in the work area.
- ***--hard***: Move HEAD to the specified commit, and reset the staging area and the work area to make them consistent with the contents of the specified commit. This means that all uncommitted changes will be completely discarded and cannot be recovered.
- ***--hard HEAD^***: The number of ^ after HEAD represents the number of versions to roll back. For example, if you want to roll back 100 versions, you can write HEAD~100 .
- ***--patch***: Allows you to interactively select changes to be undone. It will show the differences between the work area and the staging area block by block, and you can choose to accept or reject each block of changes.

<img src="./assets/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fcx7c746kwfaa97quvnch.png" alt="img" style="zoom: 50%;" />

<img src="./assets/1_lirDsZh5ZZP3l9EtulZEjw.png" alt="1_lirDsZh5ZZP3l9EtulZEjw" style="zoom:50%;" />

## Branch

Branches are independent lines of development within the repository. They allow developers to work on different features or bug fixes simultaneously. Each branch has its own commit history and can be merged with other branches to incorporate changes.

### Gitflow Workflow

* Long-term branch
  * `Main/Master`: The core branch of the project represents the stable version of the software and usually contains code that can be directly deployed to the production environment.
  * `Develop`: The main development branch of the project, where new features and improvements are integrated.
* Temporal branch
  * `Release`: A branch derived from the Develop branch in preparation for the official release of the software.
  * `Feature`: A branch created for new requirements or new feature development, usually derived from the Develop branch.
  * `bugfix/hotfix`: A branch used to urgently fix serious bugs in the production environment, usually derived from the Main/Master branch.

<img src="./assets/04 Hotfix branches.svg" width="60%">

#### Main/Master & Develop branches

Instead of a single `main` (`master`) branch, this workflow uses two branches to record the history of the project. The `main` branch stores the official release history, and the `develop` branch serves as an integration branch for features. It's also convenient to tag all commits in the `main` branch with a version number.

#### Feature branches

Each new feature should reside in its own branch, which can be pushed to the central repository for backup/collaboration. But, instead of branching off of main, feature branches use develop as their parent branch. When a feature is complete, it gets merged back into develop. Features should never interact directly with main.

#### Release branches

Once develop has acquired enough features for a release (or a predetermined release date is approaching), you fork a release branch off of develop. Creating this branch starts the next release cycle, so no new features can be added after this point—only bug fixes, documentation generation, and other release-oriented tasks should go in this branch. Once it's ready to ship, the release branch gets merged into main and tagged with a version number. In addition, it should be merged back into develop, which may have progressed since the release was initiated.

#### Hotfix branches

Maintenance or hotfix branches are used to quickly patch production releases. `Hotfix` branches are a lot like `release` branches and `feature` branches except they're based on `main` instead of `develop`. This is the only branch that should fork directly off of `main`. As soon as the fix is complete, it should be merged into both `main` and `develop` (or the current `release` branch), and `main` should be tagged with an updated version number.

### Conflict Resolution

- **Identify the conflict & Open the conflicting file(s)**: When you attempt to merge or rebase branches and encounter a conflict, Git will notify you of the conflicting files. Use a text editor or an integrated development environment (IDE) to open the files with conflicts. In the file, Git will mark the conflicting sections with special markers, such as `<<<<<<<`, `=======`, and `>>>>>>>`.

  ```
  <<<<<<< HEAD
  // Code from current branch
  =======
  // Code from merged branch
  >>>>>>> feature_branch
  ```

- **Understand & Resolve the conflict**: Analyze the conflicting sections and understand the changes made in each branch. Edit the conflicting file(s) to manually choose the desired changes. You can modify the code to include the changes from both branches or discard some changes altogether.

  - **Remove conflict markers**: Remove the conflict markers (`<<<<<<<`, `=======`, and `>>>>>>>`) and any unnecessary code added by Git during the conflict resolution process.
  - **Choose desired changes**: Modify the code to select the changes you want to keep. This may involve merging or modifying the conflicting sections to combine the changes or discarding one set of changes entirely.

- **Add the resolved file(s) & Commit the changes**: Once you've finished resolving conflicts, use the `git add` to stage the resolved file(s) for the next commit. Use `git commit` to create a new commit that includes the conflict resolution changes. It's helpful to provide a meaningful commit message that describes the conflict resolution.

  ```shell
  git add <冲突文件1> <冲突文件2> ...
  git commit
  ```

- **Repeat if necessary**: If there are additional conflicts in other files, go back to step 2 and resolve them until all conflicts are resolved.
- **Complete the merge or rebase & Push or continue with your workflow**: Once all conflicts are resolved, continue the merge or rebase operation using `git merge --continue` or `git rebase --continue`. After resolving the conflicts and completing the merge or rebase, you can ```git push``` the changes to the remote repository or continue with your workflow as desired. 

## Special Operations

### Merge commits into one commit

`git rebase --soft` Method: 

<img src="./assets/reset.svg" alt="reset" style="zoom:80%;" />
