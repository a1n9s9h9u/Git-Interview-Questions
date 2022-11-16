## Git Interview Questions

#### Git

Git is a version control system. Git helps you keep track of code changes. Git is used to collaborate on code.

#### What does Git do?

Manage projects with Repositories.

Clone a project to work on a local copy.

Control and track changes with Staging and Committing.

Branch and Merge to allow for work on different parts and versions of a project.

Pull the latest version of the project to a local copy.

Push local updates to the main project.

#### Configure Git
```git
git config --global user.name "w3schools-test"
git config --global user.email "test@w3schools.com"
```
Note: Use global to set the username and e-mail for every repository on your computer. If you want to set the username/email for just the current repo, you can remove global

#### Files in your Git repository folder can be in one of 2 states:

Tracked - files that Git knows about and are added to the repository

Untracked - files that are in your working directory, but not added to the repository

When you first add files to an empty repository, they are all untracked. To get Git to track them, you need to stage them, or add them to the staging environment.

#### One of the core functions of Git is the concepts of the Staging Environment, and the Commit.

As you are working, you may be adding, editing and removing files. But whenever you hit a milestone or finish a part of the work, you should add the files to a Staging Environment. Staged files are files that are ready to be committed to the repository you are working on. You can also stage more than one file at a time. Let's add 2 more files to our working folder. Use the text editor again.
```git
git add --all
```
Using --all instead of individual filenames will stage all changes (new, modified, and deleted) files.

Note: The shorthand command for git add --all is git add -A

By adding clear messages to each commit, it is easy for yourself (and others) to see what has changed and when.
```git
git commit -m "First release of Hello World!"
```
The Staging Environment has been committed to our repo, with the message:
"First release of Hello World!"

Sometimes, when you make small changes, using the staging environment seems like a waste of time. It is possible to commit changes directly, skipping the staging environment. The -a option will automatically stage every changed, already tracked file.

#### git status
```git
git status --short
```
 M index.html

Note: Short status flags are:

?? - Untracked files
A - Files added to stage
M - Modified files
D - Deleted files

#### To view the history of commits for a repository, you can use the log command:
```git
git log
```
#### There are a couple of different ways you can use the help command in command line:
```git
git command -help -  See all the available options for the specific command

git help --all -  See all possible commands
```
Anytime you need some help remembering the specific option for a command, you can use git command -help:
```git
git commit -help
```
Note: You can also use --help instead of -help to open the relevant Git manual page

#### Branches

Branches allow you to work on different parts of a project without impacting the main branch. When the work is complete, a branch can be merged with the main project. You can even switch between branches and work on different projects without them interfering with each other. Branching in Git is very lightweight and fast!

We create a new branch:
```git
git branch hello-world-images
```
Let's confirm that we have created a new branch:
```git
git branch
```
  hello-world-images
* master

We can see the new branch with the name "hello-world-images", but the * beside master specifies that we are currently on that branch.

#### checkout

checkout is the command used to check out a branch. Moving us from the current branch, to the one specified at the end of the command:
```git
git checkout hello-world-images
```
Switched to branch 'hello-world-images'

Now we have moved our current workspace from the master branch, to the new branch Now we merge the current branch (master) with emergency-fix:
```git
git merge emergency-fix
```
Since the emergency-fix branch came directly from master, and no other changes had been made to master while we were working, Git sees this as a continuation of master. So it can "Fast-forward", just pointing both master and emergency-fix to the same commit. As master and emergency-fix are essentially the same now, we can delete emergency-fix, as it is no longer needed:
```git
git branch -d emergency-fix
```
Deleted branch emergency-fix (was dfa79db).

#### pull is a combination of 2 different commands:

fetch
merge

fetch gets all the change history of a tracked branch/repo.

So, on your local Git, fetch updates to see what has changed on GitHub:
```git
git fetch origin
```
We can also verify by showing the differences between our local master and origin/master:
```git
git diff origin/master
```
merge combines the current branch, with a specified branch.

We have confirmed that the updates are as expected, and we can merge our current branch (master) with origin/master:
```git
git merge origin/master
```
pull is a combination of fetch and merge. It is used to pull all changes from a remote repository into the branch you are working on.
```git
git pull origin
```
That is how you keep your local Git up to date from a remote repository.

Now push our changes to our remote origin:
```git
git push origin
```
#### Pull request

A pull request is how you propose changes. You can ask some to review your changes or pull your contribution and merge it into their branch. The pull request will record the changes, which means you can go through them later to figure out the changes made.

#### fork

A fork is a copy of a repository. This is useful when you want to contribute to someone else's project or start your own project based on theirs. fork is not a command.

#### clone

A clone is a full copy of a repository, including all logging and versions of files.

#### What is SSH

SSH is a secure shell network protocol that is used for network management, remote file transfer, and remote system access. SSH uses a pair of SSH keys to establish an authenticated and encrypted secure network protocol. It allows for secure remote communication on unsecured open networks. SSH keys are used to initiate a secure "handshake". When generating a set of keys, you will generate a "public" and "private" key.

The "public" key is the one you share with the remote party. Think of this more as the lock.

The "private" key is the one you keep for yourself in a secure place. Think of this as the key to the lock.

SSH keys are generated through a security algorithm. It is all very complicated, but it uses prime numbers, and large random numbers to make the public and private key. It is created so that the public key can be derived from the private key, but not the other way around.
```git
ssh-keygen -t rsa -b 4096 -C "test@w3schools.com"
```
#### Git Revert Find Commit in Log

First thing, we need to find the point we want to return to. To do that, we need to go through the log. To avoid the very long log list, we are going to use the --oneline option, which gives just one line per commit showing:

The first seven characters of the commit hash
the commit message

So let's find the point we want to revert:
```git
git log --oneline
```
We want to revert to the previous commit: 52418f7 (HEAD -> master) Just a regular update, definitely no accidents here..., and we see that it is the latest commit.
```git
Git Revert HEAD
```
We revert the latest commit using git revert HEAD (revert the latest change,  and then commit), adding the option --no-edit to skip the commit message editor (getting the default revert message):
```git
git revert HEAD --no-edit
```
#### reset

reset is the command we use when we want to move the repository back to a previous commit, discarding any changes made after that commit.

Step 1: Find the previous commit
Step 2: Move the repository back to that step

We reset our repository back to the specific commit using git reset commithash (commithash being the first 7 characters of the commit hash we found in the log):
```git
git reset 9a9add8
```
#### commit --amend
```git
Git commit --amend
```
commit --amend is used to modify the most recent commit. It combines changes in the staging environment with the latest commit, and creates a new commit. This new commit replaces the latest commit entirely.

#### Apache Subversion vs Git

Apache Subversion or SVN is one of the most popular centralized version control systems

Git is a popular distributed version control system, which means that you can clone your repository.

#### Types of Version Control System

#### Localized Version Control Systems

The localized version control method is a common approach because of its simplicity. But this approach leads to a higher chance of error. In this approach, you may forget which directory you're in and accidentally write to the wrong file or copy over files you don't want to.

To deal with this issue, programmers developed local VCSs that had a simple database. Such databases kept all the changes to files under revision control. A local version control system keeps local copies of the files.

The major drawback of Local VCS is that it has a single point of failure.

#### Centralized Version Control System

The developers needed to collaborate with other developers on other systems. The localized version control system failed in this case. To deal with this problem, Centralized Version Control Systems were developed.

These systems have a single server that contains the versioned files, and some clients to check out files from a central place.

Centralized version control systems have many benefits, especially over local VCSs. Everyone on the system has information about the work that others are doing on the project. Administrators have control over other developers. It is easier to deal with a centralized version control system than a localized version control system.

It also has the same drawback as in the local version control system that it also has a single point of failure.

#### Distributed Version Control System

Centralized Version Control System uses a central server to store all the database and team collaboration. But due to single point failure, which means the failure of the central server, developers do not prefer it. Next, the Distributed Version Control System is developed.

In a Distributed Version Control System (such as Git), the user has a local copy of a repository. So, the clients don't just check out the latest snapshot of the files even if they can fully mirror the repository. The local repository contains all the files and metadata present in the main repository.

DVCS allows automatic management branching and merging. It speeds up most operations except pushing and pulling. DVCS enhances the ability to work offline and does not rely on a single location for backups. If any server stops and other systems are collaborating via it, then any of the client repositories could be restored by that server. Every checkout is a full backup of all the data.

These systems do not necessarily depend on a central server to store all the versions of a project file.

#### GitBash

Git Bash is an application for the Windows environment. It is used as the Git command line for windows.

#### Git GUI

Git GUI is a powerful alternative to Git BASH. It offers a graphical version of the Git command line function, as well as comprehensive visual diff tools. We can access it through the command line by typing the command below.
```git
git gui  
```
A pop-up window will open as a Git gui tool.

#### Git Stash

Sometimes you want to switch the branches, but you are working on an incomplete part of your current project. You don't want to make a commit of half-done work. Git stashing allows you to do so. The git stash command enables you to switch branches without committing the current branch.

Generally, the stash's meaning is "store something safely in a hidden place." The sense in Git is also the same for stash; Git temporarily saves your data safely without committing.
```git
git stash 
```
The work is saved with the git stash command. We can check the status of the repository.

Now, the directory is cleaned. At this point, you can switch between branches and work on them.

#### Git Index

The Git index is a staging area between the working directory and repository. It is used to build up a set of changes that you want to commit together. To better understand the Git index, then first understand the working directory and repository.

There are three places in Git where file changes can reside, and these are the working directory, staging area, and the repository. To better understand the Git index first, let's take a quick view of these places.

#### Working directory:

When you worked on your project and made some changes, you are dealing with your project's working directory. This project directory is available on your computer's filesystem. All the changes you make will remain in the working directory until you add them to the staging area.

#### Staging area:

The staging area can be described as a preview of your next commit. When you create a git commit, Git takes changes that are in the staging area and makes them as a new commit. You are allowed to add and remove changes from the staging area. The staging area can be considered as a real area where git stores the changes.

Although, Git doesn't have a dedicated staging directory where it can store some objects representing file changes (blobs). Instead of this, it uses a file called index.

#### Repository:

In Git, Repository is like a data structure used by GIt to store metadata for a set of files and directories. It contains the collection of the files as well as the history of changes made to those files. Repositories in Git are considered as your project folder. A repository has all the project-related data. Distinct projects have distinct repositories.

You can check what is in the index by the git status command. The git status command allows you to see which files are staged, modified but not yet staged, and completely untracked. Staged files mean, it is currently in the index.

#### Git Head

The HEAD points out the last commit in the current checkout branch. It is like a pointer to any reference. The HEAD can be understood as the "current branch." When you switch branches with 'checkout,' the HEAD is transferred to the new branch.

#### Git Show Head

The git show head is used to check the status of the Head. This command will show the location of the Head.
```git
git show HEAD  
```
#### Git Origin Master

The term "git origin master" is used in the context of a remote repository. It is used to deal with the remote repository. The term origin comes from where the repository originally situated and master stands for the main branch.

#### Git Remote

In Git, the term remote is concerned with the remote repository. It is a shared repository that all team members use to exchange their changes. A remote repository is stored on a code hosting service like an internal server, GitHub, Subversion, and more. In the case of a local repository, a remote typically does not provide a file tree of the project's current state; as an alternative, it only consists of the .git versioning data.

The developers can perform many operations with the remote server. These operations can be a clone, fetch, push, pull, and more.

#### Git Tags

Tags make a point as a specific point in Git history. Tags are used to mark a commit stage as relevant. We can tag a commit for future reference. Primarily, it is used to mark a project's initial point like v1.1.

Tags are much like branches, and they do not change once initiated. We can have any number of tags on a branch or different branches.

#### Upstream and Downstream

The term upstream and downstream refers to the repository. Generally, upstream is from where you clone the repository, and downstream is any project that integrates your work with other works.

#### Git Rm

In Git, the term rm stands for remove. It is used to remove individual files or a collection of files. The key function of git rm is to remove tracked files from the Git index. Additionally, it can be used to remove files from both the working directory and staging index.

The files being removed must be ideal for the branch to remove. No updates to their contents can be staged in the index. Otherwise, the removal process can be complex, and sometimes it will not happen. But it can be done forcefully by -f option.
```git
git rm <file Name>  
```
#### Git Cherry-pick

Cherry-picking in Git stands for applying some commits from one branch into another branch. In case you made a mistake and committed a change into the wrong branch, but do not want to merge the whole branch. You can revert the commit and apply it on another branch.

The main motive of a cherry-pick is to apply the changes introduced by some existing commit. A cherry-pick looks at a previous commit in the repository history and updates the changes that were part of that last commit to the current working tree. The definition is straight forward, yet it is more complicated when someone tries to cherry-pick a commit, or even cherry-pick from another branch.

Cherry-pick is a useful tool, but it is not a good option. It can cause duplicate commits and some other scenarios where other merges are preferred instead of cherry-picking. It is a useful tool for a few situations. It is in contrast with different ways such as merge and rebase commands. Merge and rebase can usually apply many commits in another branch.

#### Git Rebase

Rebasing is a process to reapply commits on top of another base trip. It is used to apply a sequence of commits from distinct branches into a final commit. It is an alternative to the git merge command. It is a linear process of merging.

In Git, the term rebase is referred to as the process of moving or combining a sequence of commits to a new base commit. Rebasing is very beneficial and it visualizes the process in the environment of a feature branching workflow.

Generally, it is an alternative to the git merge command. Merge is always a forward changing record. Comparatively, rebase is a compelling history rewriting tool in git. It merges the different commits one by one.

Suppose you have made three commits in your master branch and three in your other branch named test. If you merge this, then it will merge all commits in a time. But if you rebase it, then it will be merged in a linear manner.
```git
git rebase <branch name>  
```
#### Git Squash

In Git, the term squash is used to squash the previous commits into one. It is not a command; instead, it is a keyword. The squash is an excellent technique for group-specific changes before forwarding them to others. You can merge several commits into a single commit with the compelling interactive rebase command.

If you are a Git user, then you must have realized the importance of squashing a commit. Especially if you are an open-source contributor, then many times, you have to create a PR (pull request) with a squashed commit. You can also squash commits if you have already created a PR.

#### Which language is used in Git?

Git uses 'C' language. Git is quick, and 'C' language makes this possible by decreasing the overhead of run times contained with high-level languages.

#### What is a 'conflict' in git?

A 'conflict' appears when the commit that has to be combined has some change in one place, and the current act also has a change at the same place. Git will not be easy to predict which change should take precedence.

#### How to resolve a conflict in Git?

If you need to resolve a conflict in Git, edit the list for fixing the different changes, and then you can run "git add" to add the resolved directory, and after that, you can run the 'git commit' for committing the repaired merge.

#### Describing branching systems you have utilized?

#### Feature Branching:

A component branch model keeps the majority of the changes for a specific element within a branch. At the point when the item is throughout tested and approved by automated tests, the branch is then converged into master.

#### Task Branching

In this model, each assignment is actualized on its branch with the undertaking key included in the branch name. It is anything but difficult to see which code actualizes which task, search for the task key in the branch name.

#### Release Branching

Once the create branch has procured enough features for a discharge, you can clone that branch to frame a Release branch. Making this branch begins the following discharge cycle so that no new features can be included after this point, just bug fixes, documentation age, and other release oriented assignments ought to go in this branch. When it is prepared to deliver, the release gets converged into master and labeled with a form number. Likewise, it should be converged once again into creating a branch, which may have advanced since the release was started.

#### By what method will you know in Git if a branch has just been combined into master?

To know whether a branch has been merged into master or not you can utilize the below commands:

git branch - merged It records the branches that have been merged into the present branch.

git branch - no merged It records the branches that have not been merged.

#### What is Subgit? Why use it?

'Subgit' is a tool that migrates SVN to Git. It is a stable and stress-free migration. Subgit is one of the solutions for a company-wide migration from SVN to Git that is:

It is much superior to git-svn.

No need to change the infrastructure that is already placed.

It allows using all git and all sub-version features.

It provides a stress free migration experience.

#### What is the functionality of git clean command? 

The git clean command removes the untracked files from the working directory.

#### If you recover a deleted branch, what work is restored?

The files that were stashed and saved in the stashed index can be recovered. The files that were untracked will be lost. Hence, it's always a good idea to stage and commit your work or stash them. 

#### Explain the different points when a merge can enter a conflicted stage.

There are two stages when a merge can enter a conflicted stage.

1. Starting the merge process

If there are changes in the working directory of the stage area in the current project, the merge will fail to start. In this case, conflicts happen due to pending changes that need to be stabilized using different Git commands.

2. During the merge process

The failure during the merge process indicates that there’s a conflict between the local branch and the branch being merged. In this case, Git resolves as much as possible, but some things have to be fixed manually in the conflicted files.

#### What is the command used to fix a broken commit?

To fix a broken commit in Git, you may use the “git commit --amend” command, which helps you combine the staged changes with the previous commits instead of creating an entirely new commit.

#### How do you recover a deleted branch that was not merged?

To recover a deleted branch, first, you can use the git reflog command. It will list the local recorded logs for all the references. Then, you can identify the history stamp and recover it using the git checkout command.

#### What’s the difference between reverting and resetting?

The revert command in Git is used to create a new commit that undoes the changes made in the previous commit. When you use this command, a new history is added to the project; the existing history is not modified.

Git reset is a command that is used to undo the local changes that have been made to a Git repository. Git reset operates on the following: commit history, the staging index, and the working directory.

#### Git clone

Git clone allows you to create a local copy of the remote GitHub repository. Once you clone a repo, you can make edits locally in your system rather than directly in the source files of the remote repo.

#### GitLab

GitLab is a web-based Git repository that provides free open and private repositories, issue-following capabilities, and wikis. It is a complete DevOps platform that enables professionals to perform all the tasks in a project—from project planning and source code management to monitoring and security. Additionally, it allows teams to collaborate and build better software.
