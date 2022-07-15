# GIT aliases

## What's this repository for?

This repository contains one **.gitaliases** file that you can use for your daily GIT usage.
Most of them are convenient shortcuts for basic commands.
Other aliases are powerful commands that performs many operations at once.

## Are these aliases suitable for me?

These aliases are more suitable for those who understand GIT basics.

However, there are many aliases you can use even if you are still learning the fundamentals.
If you are not confident with using aliases, do not use aliases that have "▲" in the description below. All other have no risks at all.

I recommand using your favourite IDE's GIT tools for handling all of GIT's operations.
But like many other tools, it's often preferable to know how it is working at core, because whenever you encounter a problem, you know better how to get through it.
Before using aliases, writing full basic GIT commands will help you understand its mechanisms.


## How to use this file?

Download `.gitaliases` and put it in your home folder (`~/.gitaliases`) or any other location.

Open the `.git/config` file in your project's folder if you want to use `.gitaliases` only for this project:
```
cd path/to/your/project
git config -e
```

Open the `~/.gitconfig` file if you want to use `.gitaliases` for all your projects:
```
git config -e --global 
```

Add this inside your gitconfig file to include `.gitaliases`:
```
[include]
    path = ~/.gitaliases
```

## Philosophy

This list will be perfect for me once I would have removed all aliases that I never use. There are not that much though.

Aliases naming method is not consistent, but it should be!
You can name aliases based on command **effect** or command **abbreviation**. For instance, for naming your alias for "git log --grep word":
* Effect : `git find word`, `git f word` 
* Abbreviation : `git lep word`

I recommand you to rename your aliases so that they are easier for you to remember.

### Git log aliases

The purpose of these aliases is to make your console history compact, so that after you wrote a bunch of commands, you have more information on a single window.
You will need to scroll less to compare logs for instance.
It is also compact horizontally to keep commit logs on one line in case your console is on a half screen.

## Aliases

Words in _italic_ are parameters.

Words _\[in between brackets\]_ are facultative parameters.

"▲" Indicates that command is risky.

### Commit history (git log)

Show one or more commits.

| Alias        | Effect           |
| ------------- |---|
| git l      | Last commit      |
| git ll | 3 last commits      |
| git lll | 5 last commits with graph     |
| git llll | 10 last commits with graph     |
| git ls | Last commmit with modified files. Adds A/M/D before each file to distinct Added/Modified/Removed     |
| git lep _word_ | Commits that contains _word_ in message     |
| git since _commithash_ | All commits from _commithash_ to HEAD. commithash can also be replaced by a branch or tag name.     |
| git ld | Last commit + compare creation date / modification date. Use it to see if there was a commit amend.     |


### Commited files history

| Alias        | Effect           |
| ------------- |---|
| git see _commithash_     | Files modified in _commithash_. Adds A/M/D before each file to distinct Added/Modified/Removed     |
| git diffsince _commithash_ | Files modified from _commithash_ to HEAD      |
| git newsince _commithash_ | Files added from _commithash_ to HEAD      |
| git deletedsince _commithash_ | Files deleted from _commithash_ to HEAD      |
| git renamedsince _commithash_ | Files renamed from _commithash_ to HEAD      |

### Checkout

| Alias        | Effect           |
| ------------- |---|
| git c _branchname_     | Checkout _branchname_     |
| git cd | Checkout develop      |
| git cm  | Checkout master      |

### Commit

| Alias        | Effect           |
| ------------- |---|
| git s     | Short status: show status of working directory and stage     |
| git aa | Add ALL files, including new ones, then show files added      |
| git a  | Add modified and deleted files. NEW FILES MUST BE ADDED MANUALLY      |
| git com _message_  | Commit with _message_      |
| git acom _message_  | Add all to stage and commit with _message_      |
| git chm _message_  | Change last commit _message_      |
| git coam  | ▲ Commit amend: commit all files added to stage into last commit, without changing message      |
| git fix  | ▲▲ Add all files to stage and amend them into last commit      |
| git unstage _\[filename\]_  | Remove _filename_ from stage, or remove all files from stage if no _filename_  |
| git undo _\[filename\]_  | ▲ Undo changes on _filename_ (remove changes from stage AND working directory. Undo all if no _filename_  |
| git resod  | Undo last commit and put file changes back in stage.      |
| git dc _\[filename\]_ | Show diff for _filename_ or for all files.  |

### Branches CRUD

| Alias        | Effect           |
| ------------- |---|
| git b | Show branches |
| git cb _branchname_ | Create branch with name _branchname_ and check it out |
| git cdb _branchname_ | Create branch with name _branchname_ from develop and check it out |
| git br | Update remote branches list on local and show list |
| git bd _branchname_ | Delete branch with check if merged, and confirm prompt  |
| git bdd _branchname_ | ▲ Delete branch with no confirm |
| git delete _branchname_ | ▲ Delete branch locally and on remote |
| git deletemergedcheck | Show branches that have been merged into develop and can be deleted |
| git deletemerged | ▲ Delete all branches on origin that have been merged into develop. Will show a confirm prompt y/n for each branch to delete. |
| git deletemergedmaster | ▲ Same as deletemerged but for master |


### Fetch, pull, merge, rebase

**IMPORTANT**: only rebase branches that have no descendants (no child branch have been created from this branch).

| Alias        | Effect           |
| ------------- |---|
| rbd | ▲ Fetch develop and rebase current branch onto it if necessary. If last common commit between current branch and develop is the last commit on develop, there is no need to rebase your branch.  |
| rbm | ▲ Fetch master and rebase current branch onto it if necessary.  |
| mid | ▲ Merge current branch into develop |
| mim | ▲ Merge current branch into master |

#### Details on `git mid` operations

Command: `git fd && curb=$(git branch-name) && git canmergeintodevelop && git cd && git merge $curb && git checkout $curb || git rebase develop`

1. Fetch develop
2. If current branch can be merged into develop with fast forward, checkout develop, merge branch then checkout branch
3. If current branch can NOT be merged with fast forward, rebase current branch onto develop
4. If you had to rebase develop, use git mid again to merge it into develop with fast forward (now possible).

### Publish : actions on remote repository

| Alias        | Effect           |
| ------------- |---|
| git publish | Push the current branch to the remote "origin", and set it to track the upstream branch. |
| git unpublish | ▲ Delete the remote version of the current branch |
| git please | ▲ Push force current branch to remote but with a magical check that I still need to understand |


### Misc

| Alias        | Effect           |
| ------------- |---|
| git alias | Show all aliases |
| git speed | ▲ Accelerate GIT by cleaning useless temp files |
| git stm _message_ |  Stash files and name stash with _message_ |
| git sl | Show stash list  |
| git tags | Show tag list |
