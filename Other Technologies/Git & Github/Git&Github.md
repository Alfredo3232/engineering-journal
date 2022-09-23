# What is Git?

1. Git is a Version Control System, it also known as VCs
2. What is a Version Control System
    1. A Version Control System is software that tracks and manages changes to files over time.
        1. Usually VCs generally allow users to revisit versions of files, comparing changes between versions, undo changes, sharing changes to other people, and a lot more.
        2. There is a lot more VCs than just Git the other popular ones are Subversion, CVS, and Mercurial

---
  
# History of Git

1. Linus Torvalds is a software engineer, he is the creator and main develop behind Linux and Git
    1. Linus when he was working with a team on linux they were using Bitkeeper, there were some disagreements with the developers behind Bitkeeper.
        1. So Linus decided to make a VCs himself that was free and open source. And he dedicated most oh April 2005 to develop Git
2. Git stands for Global Information Tracker

---

1. Github hosts repositories in the cloud to make it easier to collaborate with other people, its an online place to share work that is done using Git
2. Git Bash is a Command Line Interface or CLI, it is the default shell for Linux and Mac, Git was designed to run on Unix-based interface
    1. Windows comes with a different CLI called Command Prompt, it's not Unix based
    2. Fortunately Git Bash is a tool that emulates Bash on a windows machine

---

# Terminal Mini-Course Notes

1. start .  - it opens your current location on file explorer
2. pwd - this shows the location of where your are
3. touch example.js  - this creates a files in your current directory
4. mkdir exampleDir -this makes a new directory(folder)
5. rm fileName.txt - this deletes a file
6. rm -rf Folder - this deletes a directory
    1. -r - is recursive
    2. -f - is force

---

# What is a Git Repo?

1. Repository - it refers to a Git Repository or Repo, this is a workspace which tracks and manages files within a folder

---

# Git Commands

1. git status - gives information of the current status of a git repository and its content
2. git init - creates a new git repo at the current directory, you must initialize a repo first
3. How to Commit in Git?
    1. git status - this tells you what files have not been added
    2. git  add - this stages a commit this adds the files that you want to commit
        1. git add fileName1 fileName2 - this adds specified files
        2. git add . - adds all files changed
    3. git status - again to double check what files you have added
    4. git commit -m “description here” - this commits your changes with a description about the changes
4. git log - gives you all the commits that were made in a given repository
5. git commit --amend - this allows to “redo” the previous commit, you can files or fix a type in the commit message

---

# Git Branching

1. Git Branches - are separate contexts of the main project, so if one branch makes changes others will not be affected until it is merged or added to the main branch
2. When you start a project with git the default name is master, this branch is considered
3. HEAD is a pointer to a branch that you are currently in
4. git branch - lists all branches of the current project
5. git branch nameHere - after branch provide a name and that makes a new branch, but does not automatically switch to that branch
    1. git checkout -b branchName - this creates a new branch, using git checkout
6. git switch branchName - this switches the current branch to the one that you want to switch to.
7. git commit -a -m “description” - this adds all unstaged changes and commits them
8. git checkout branchName -  this also switches branches, but has tons of functionality
9. git switch -c branchName - this creates a new branch provided by the name and switches for you upon creation
10. When creating a new file on a separate branch and you dont save & commit, that file will follow you on every branch, until you commit it to your branch
    1. However, for files that are changed and in conflict with other branches, and you try to switch branches. Git will warn you that the changes that you made will be lost if you don't save & commit
11. git branch -D branchName - this deletes a branch regardless of its merge status
12. How to change a branch's name ?
    1. Switch to the branch you want to rename
    2. git branch -m newName - this renames your branch to the desired name you give it
    3. Git status to confirm that your name has been changed

---

# Merging Branches

1. Merging, we merge branches not specific commits. We always merge to the current HEAD branch
2. How to Merge Branches ?
    1. Switch to the branch you want to merge the changes into (the receiving branch)
    2. Use git merge - to merge changes from a specific branch into the current one
        1. git merge branchName
3. Resolving Conflicts
    1. Open up the files with merge conflicts
    2. Edit files to remove conflicts decide which branch’s content you want to keep in each conflict
    3. Remove the conflict marker in the documents
    4. Add your changes then commit

---

# Git Diff

1. git diff - you can use this command to view changes between commit, branches, files our working directory and more
    1. git diff - without additional options lists all the changes in our working directory that are NOT staged for the next commit

![image](./images/1.png "image_tooltip")

1. A and B are the same file they are just being compared, A being previous commit and B being the changes now

![image](./images/2.png "image_tooltip")

![image](./images/3.png "image_tooltip")

1. git diff HEAD - lists all changes in the working tree since your last commit

![image](./images/4.png "image_tooltip")

1. git diff branchName1 branchName2 - this will list all changes between the two provided files
2. git diff hashNum..hashNum - this compares all changes between commits, all you have to do is provide the hashes of the commit, you can see the hash numbers of commits in git log

---

# Git Stashing

1. git stash -  provides and easy way of “stashing” uncommitted changes so that you can return to them later
    1. git stash pop - this removes your recently stashed changes and re-apply them to your working copy
    2. git stash apply - you can use to apply whatever is stashed away without removing it from the stash
2. You can add multiple stashes, they will all be stashed in the order you added them
    1. git stash list - gives you a list of all your stashed saves
    2. git stash apply stashID - you can apply a specific stash
3. git stash drop stashID - this removes a specific stash in your stack of stashes
4. git stash clear - this removes all your stashes
5. Checkout -  can create branches, switch to new branches, restore files and undo history
6. git checkout commit commitHash - you can use this to view a previous commit
7. DETACHED HEAD??
    1. detached HEAD - you can look around, make experimental changes and commit them. You can discard any commits in this state without impacting any branches by switching back to a branch
    2. To enter detached head mode, git checkout commitHash ?

---

![image](./images/5.png "image_tooltip")

![image](./images/6.png "image_tooltip")

1. git checkout HEAD fileName - this reverts changes done to a specific file to how it looked like in a previous commit

![image](./images/7.png "image_tooltip")

![image](./images/8.png "image_tooltip")

1. git restore --staged fileName - this command removes the file from being staged

![image](./images/9.png "image_tooltip")

1. git reset --hard commitHash -if you want to undo both the commits and the ACTUAL changes in your files, use --hard

![image](./images/10.png "image_tooltip")

1. If you want to reverse some commits that other people already have on their machines, you should use REVERT
    1. If you want to reverse commits that you haven't shared with other use RESET

---

# Github Basics

1. Github is a service that hosts git repositories in the cloud, making it easier to collaborate with other people
2. git clone is a git command its not tied in any way to github
3. git push &lt;remote> &lt;branch> - this command pushes up your work to github specify remote and the local branch you want to push up
4. git push -u origin master - -u option allows us to set the upstream of the branch we are pushing link connecting our local branch to a branch on github
5. git fetch &lt;remote> -fetches branches and history from a specific repo, it only updates remote tracking branches
6. git pull &lt;remote> &lt;branch> -will update your HEAD branch and will integrate all latest changes, basically it's git fetch + git merge.
7. README files - what the project does, how to run the project, and among other things
8. CENTRALIZED WORKFLOW -  means everyone work on Master, this is the simplest collaborative workflow possible, but has huge glaring issues
9. FEATURE BRANCHES -  rather than working directly on Master, all new development should be done on separate branches
    1. Treat Master branch as the official project history, also people can collaborate without breaking Master

---

# Pull Requests

* Pull Requests are a feature built in to products like github, and are not native to git itself
  * They allow devs to alert other team members that new work needs to be reviewed. In simple terms is that this allows team members to review work before adding those changes to the branch they are working on
* In the settings page
  * You can set branch protections, like who can merge two branches? Who can delete branches? If  pull requests require reviews?
* Fork & Clone workflow instead of just one centralized github repo, every developer has their own github repo in addition to a master repo, devs can make changes, push to their own forks before making pull requests, very common on large open source projects
  * The workflow generally looks like this
    * Fork the project
    * Clone the fork
    * Add upstream remote
    * Do some work
    * Push to origin
    * Open a Pull Request
* Forking is a feature not of git, but of github instead. Forking allows us to create personal copies of other people’s repos

---

# Rebasing

* Rebasing is used in two main ways
  * As an alternative to merging
    * When merging with merge it will appear another commit that you merged to master
    * But with rebase it will be cleaner, in summary
      * Put your changes above all new remote changes, and rewrite commit history, so your commit history will be much cleaner than git merge. Rebase is a destructive operation. That means, if you do not apply it correctly, you could lose committed work and/or break the consistency of other developer's repositories.
  * Clean up tool

![image](./images/11.png "image_tooltip")

---

* Rewriting History, sometimes we want to rewrite, delete, rename or even reorder commits before sharing them, we can do this with git rebase
* git rebase -i HEAD~# - you will enter interactive mode which allows you to edit commits, add files, drop commits, NOTE that you need to specify how far back you want to rewrite commits
  * Next page  

![image](./images/12.png "image_tooltip")

---

# Git Tags

* Tags are pointers that refer to particular points in git history, you can mark a particular moment in time with a tag. Think of tags as branch references that do not change
* There are two kinds of tags
  * Lightweight tags are lightweight, they are just a name/label that points to a particular commit
  * Annotated tags store extra metadata including the authors name and email, the date, and a tagging message
* Semantic Versioning
  * It's a specification on how to version software there rules to follow
  * 2.4.1
    * 2 - Major release - Major changes that is no longer backwards compatible
    * 4 - minor release - new features or functionality have been added, it's still backwards compatible
    * 1 - patch release - only bug fixes or other changes that do not impact code

![image](./images/13.png "image_tooltip")

* git tag - lists all tags in the branch you are on  
* git tag &lt;tagName> - this creates a lightweight tag, by default git will reference to the commit that the HEAD is referencing
* git tag -a &lt;tagName> - this creates a new annotated tag, then git will open your default editor and prompt you for additional info.
  * Additionally you use -m option instead to pass a message directly
* git tag -f &lt;tagName> - if you try to reuse a tag that is already referring to a commit, you can use -f option to FORCE the tag through
* git tag -d &lt;tagName> - deletes the given tag
* git push --tags - this will push up any tags that you have, normally git push does not push tags, but with this flag it will

---

# Git Behind The Scenes

* Config file of git is for configuration, you can configure global settings like name and email across all git repos, but you can also configure things per-repo
* IN EVERY GIT REPO FOLDER THERE IS A .git FOLDER CD INTO IT AND YOU CAN FIND THE CONFIG FILE INSIDE
* Refs Folder - refs/head contains one file per branch, each file is named after a branch and contains the hash of the commit at the tip of the branch
  * refs/tags folder which contains one file for each tag in the repo
* HEAD file, keeps track of where HEAD points
  * If it contains refs/head/master, means that the HEAD is pointing to the master branch
* In detached HEAD, the HEAD file contains a commit hash instead of a branch reference
* Objects Folder, objects directory contains all the repo files, this is where git stores the backups of the repo, the files are all compressed and encrypted
  * There are 4 types of git objects; commit, tree, blob, and annotated tag
* Git uses a hashing function called SHA-1, SHA-1 always generates 40 digit hexadecimal numbers
* Git Database, git is a key-value data store, we can insert any kind of content into a git repo and git will hand us back a unique key we later can use to retrieve that content

![image](./images/14.png "image_tooltip")

![image](./images/15.png "image_tooltip")

* Git Blobs (binary large object)  are the object type git uses to store the contents of files, blobs don't event include the file names of eachfile or any other data, just the content inside the file
* Trees are a git objects used to store the contents of a directory, each tree contains pointers that can refer to blobs and to other trees

![image](./images/16.png "image_tooltip")

![image](./images/17.png "image_tooltip")

* Commit objects combine a tree object along with information, commits store a reference to parent commits, the author, the committer, and commit message

---

# Git Reflogs

* Git keeps a record of when the tips of branches and other references were updated in the repo, you can view and update those reference logs using git reflog
  * Git only keeps reflogs on your local activity, they are not shared with others, reflogs expire, git cleans old entries after around 90 days (it can be configured tho)

![image](./images/18.png "image_tooltip")

* name@{qualifer} - you can use that syntax to access specific ref pointers

![image](./images/19.png "image_tooltip")

* Steps to go back from a rebase
  * git reflog show &lt;HEAD>
  * Copy the hash or name of commit
  * git reset  --hard &lt;hashOrName>

---

# Custom Git Aliases

![image](./images/20.png "image_tooltip")

* git aliases is like a shortcut for other commands for example
  * You can define an alias git ci instead of git commit
* EXAMPLE OF ALIAS

![image](./images/21.png "image_tooltip")

# Q&A

* What is the difference between git checkout & git switch?
* What is really the difference between “git fetch” and “git merge” vs “git pull” vs “git rebase”?
