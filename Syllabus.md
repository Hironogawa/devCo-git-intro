# DevCo Git Intro

Learn about git and how to use it.

## Index

- [1. Git Short Intro](#1-explore-git-theorie)
- [2. First things first setup Git](#2-first-things-first-setup-git)
- [3. Git command practices](#3-git-command-practices)
- [4. Git Flow](#4-git-flow)

# 1. Explore Git Theorie

We look at git, what it's and how we can use it.

# 2. First things first setup Git

## 2.1 Create a git account

We'll work with Github, but you can use any git Repository if you want for this. (All examples are also based on Github and differ on different Git providers)

_Both organisation have free git reposiotories and tools for developers:_

- Github: https://github.com/
- Gitlab: https://gitlab.com/users/sign_up

## 2.2 Create a SSH Key to have access to your repository with the CLI

Setup the SSH key, so we can work with our remote git Repository.

## 2.3 Git Config

We now set our git config settings. We can set global settings to apply on every Repository and local settings, if we need to define settings on specific git repositories.

### Display the Config Settings

Display the config files on different levels.

#### Show Global Settings

Set here your default Git settings

`git config --global --list`

#### Show Local Settings

You can set different personas ex. private project and profile on the folder level.

`git config --local --list`

#### Show all settings and the file paths

`git config --list --show-origin`

### Global Settings

Set the following settings to the global git settings.

#### Set Global Username

`git config --global user.name "My Name"`

This will be displayed in the commit message etc. Use your Github username. Only use quotes if you want a name/value with spaces in it.

#### Set Global E-Mail

`git config --global user.email my@email-address.com`

#### Set Global Default Branch Name

`git config --global init.defaultBranch main`

Now we can check all our settings, with the command learned before: [Show all Settings](#show-all-settings-and-the-file-paths)
`

### Local Settings

We can write the local config if we need specifig settings on the git repository level. Ex. if we have private repository on our company machine with a different username and email.

We set the config with the --local flag ex.

`git config --local user.name MyUserName`

### Define now your global config

Define your configs like below:

`git config --global user.name Username`

`git config --global user.email my@email-address.com`

`git config --global init.defaultBranch main`

Check if everything is correct:

`git config --global --list`

# 3. Git command practices

Essential git commands to work with git. We'll use the CLI in the examples.

- [3.1 Git clone](#31-git-clone)
- [3.2 Git create branches](#32-git-create-branches)
- [3.3 Git switch branch](#34-git-switch-branch)
- [3.4 Git commit & push](#35-git-commit--push)
- [3.5 Git stash](#37-git-stash)
- [3.6 Git merge](#37-git-merge)
- [3.7 Git resolve merge conflicts](#38-git-resolve-merge-conflicts)
- [3.8 Git rebase](#39-git-rebase)
- [3.9 Git cherrypick](#310-git-cherrypick)

## 3.1 Git clone

To clone a git repository we use the following command:

`git clone repository-url`

For example we clone this git repository with the following command:
`git clone git@github.com:Hironogawa/devCo-git-into.git`

## 3.2 Git create branches

### Create a new local branch in the CLI

`git branch new-branch-name`

The "branch" command creates a new branch from the current working-branch with the name "new-branch-name".

#### Create new branch and switch to that branch

To change the current working branch we can use the checkout command. We can combine the checkout command with the branch command to create a new branch and siwtch to that branch in one command.

`git checkout -b new-branch-name`

### 3.3 From a different Branch

If we use the "branch" command, we create a new branch from the current working branch. If we want to create a new branch from a specific branch, we can use the following command:
`git checkout -b feature-branch develop`

In the example above we create a new branch with the name "feature-branch" from the branch "develop".

## 3.4 Git Switch branch

With the checkout command we can switch between branches. Use [Git stash [↓]](#37-git-stash) to save your changes before switching branches or commit your changes. If you switch branches with uncommited changes, you'll get an error message.

`git checkout branch-name`

## 3.5 Git commit & push

### 3.5.1 Add files to the staging area

If we are happy with our changes, we can commit and push them to the remote repository. First we need to add the files to the staging area with the following command:

`git add .`

This command adds all files to the staging area. If we want to add only specific files, we can use the following command:

`git add file-name`

### 3.5.2 Commit message

After adding the files to the staging area, we can commit them with the following command:

`git commit -m "commit message"`

The commit message should be short and describe the changes you made. If you want to add more information to the commit message, you can use the following command:

`git commit -m "commit message" -m "additional information"`

### 3.5.3 Push changes to the remote repository

After commiting our changes, we can push them to the remote repository with the following command:

`git push`

## 3.7 Git stash

Git stash is a very usefull command, if we want to switch branches or pull changes from the remote repository. If we have uncommited changes, we can stash them and apply them later.

### Stash your local changes

To stash your local changes use the following command:

`git stash`

### List all stashes

To list all stashes use the following command:

`git stash list`

### Apply a stash

After applying a stash, the stash is still in the stash list.

`git stash apply`

### Apply a stash and remove it from the stash list

This will apply the stash and remove it from the stash list.

`git stash pop`

### Apply a stash with a specific stash id

We can also apply a specific stash with the stash id. The stash id is the number in the stash list.

`git stash apply stash@{2}`

### Remove a stash

If we don't need a stash anymore, we can remove it from the stash list.

`git stash drop stash@{2}`

### Remove all stashes

If we are done working with the stash we also can remove all stashes with the following command:

`git stash clear`

## 3.7 git merge

The git merge command merges changes from a different branch into the current working branch. For example if we want to merge the branch "feature-branch" into the branch "develop", we need to switch to the branch "develop" and use the following command:

`git merge feature-branch`

If we have merge conflicts, we need to resolve them before we can commit and push our changes. [Resolve merge conflicts [↓]](#38-git-resolve-merge-conflicts)

To regular workflow would look like this:

1. Switch to the branch you want to merge into ex. "develop". `git checkout develop`
2. Pull the latest changes from the remote repository. `git pull`
3. Merge the branch you want to merge into the current working branch ex. "feature-branch". `git merge feature-branch`
4. Resolve merge conflicts if there are any. [Resolve merge conflicts [↓]](#38-git-resolve-merge-conflicts)
5. Add the files to the staging area. `git add .`
6. Commit the changes. `git commit -m "commit message"`
7. Push the changes to the remote repository. `git push`

## 3.8 git resolve merge conflicts

Sometimes we have merge conflicts, if we merge a branch into another branch. That means, that the same file was changed in both branches we want to merge. That could happen, if we or one of our peers changed the same file in different branches. Git can't decide which changes to keep, so we need to resolve the merge conflict manually.

### Resolve merge conflicts with the CLI

To resolve merge conflicts with the CLI we need to open the file with the merge conflict and reslove the conflict manually. The file with the merge conflict looks like this:

`git merge feature-branch`

We could use the CLI for this but VS Code has a nice UI for this. We can open the file with the merge conflict in VS Code and resolve the merge conflict with the UI. The UI will display the conflicting changes on that line more or less like this:

<sup><sub>Accept Current Change | Accept Incoming Change | Accept Both Changes | Compare Changes</sub></sup><br>
`<<<<<< HEAD`<br>
new line in the current working branch<br>
`======`<br>
new line in the branch we want to merge<br>
`>>>>>>` feature-branch

Now we need to decide wich changes we want to keep. If we want to keep the changes from the current working branch, we need to delete the changes from the branch we want to merge. We want for example to keep the changes from the current working branch, so we delete the changes from the branch we want to merge. So click on the button "Accept Current Change". After we resolved all the merge conflicts, we can add the files to the staging area `git add .` and commit the changes `git commit -m "commit message"` and push the changes to the remote repository `git push`.

## 3.9 git rebase

Git rebase is used to clean up the git history. If we have a lot of commits, we can squash them into one commit. We can also change the order of the commits. We can also use git rebase to merge a branch into another branch.

### 3.9.1 Squash commits

## 3.10 git cherrypick

# 4. Git Flow

## Additional Workflow and Pipeline

### Git Tag and Release