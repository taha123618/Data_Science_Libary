 ### Short introduction
Git is a distributed Version Control System VCS tool used to versioning, collaboration of a project

### Some usefull git commands
- git init ~ This command initialize folder as a git repository
- git status ~ check current status including in which branch currently the HEAD pointing to and the information of changes to be staged
- git add . ~ start tracking changes in all the files (add to staging area)
- git add [filename] ~ only add specific file to staging area
- git reset ~ only reset from staged to unstage all files
- git reset [filename] ~ only reset specific file but not remove modifications of file
- git reset --hard ~ reset from staged to unstaged also remove modifications from all files
- git checkout HEAD [filename] ~ remove modifications of specific file before commit in stage/unstage
- git commit -m "[message]" ~ commit to local repository
- git push ~ push changes to the upstream remote repository (best practice is to use local repo name and branch name e.g git push origin main)
- git fetch ~ fetch the changes from remote repository but not merge with local repository.
- git merge ~ merge the fetched changes (from command git fetch) to local repository.
- git pull ~ fetch and merge the changes from the upstream remote to local repository (best practice is to use local repo name and branch name e.g git pull origin main)
To pull another branch present in remote but not in local then use one of these methods:

- git pull origin (remote-branch-name) and checkout into it ~ it will merge ahead commits to active branch (if any)
- git fetch origin (remote-branch-name) and checkout into it
 - git switch -c (branch-name) origin/(branch-name) ~ it will create and switched to new branch available at remote(BUT before running this command you need to run git pull command first at any other active branch)
 - git branch -M [branch-name] ~ change active/working branch name e.g git branch -M main
- git remote add [set-repo-name] [url] ` connect local repo to remote repo e.g git remote add origin (link)
 - git remote -v ~ show the remotely connected repo url to local repo
- git push -u [repo-name] [branch-name] ~ push all local commits to specific branch of remote repo (here -u flag create upstream so that to use only git push command without mentioning repo/branch name worth noting that here (repo-name) is not the actual name of remote repo and if branch doesn't exist on remote then it will create another branch of this name on remote repo)
- git remote show ~ display the local name of connected repo
- git remote show [repo-name] ~ show the status of remote repo e.g git remote show origin



### To undo/revert commits
git reset --hard [commit-hash] // to roll back upto specified commit hash to local repo(commit includes changes accross multiple files will be roll backed from commit history/log)
git revert [commit-hash] // it will only remove the applied changes/affect by a specific commit (it actually add another commit to revert changes and that commit is a part of history/log)
git push -f origin main // rolled back commits from remote repo ( affect of rolled back only available to local repo, you need to run this command to roll back commits from remote repo too)



### Branches in git
To work in a same repository but in different context/module/features in a team or even individually then creating branches are helpful. Each git repository contains at least the one branch master/main.

git branch OR git branch --list // display a list of branches
git branch -v // display a list of branches with additional detail
git branch -a // display all local and remote branches.
git branch -r // display all remote branches
git branch [branch-name] //create new branch
git checkout [branch-name] //switch branch
git checkout -b [branch-name] // create and switch to the newly created branch
git branch --delete [branch-name] //delete local branch (--delete OR -d)
git branch -dr [repo-name]/[branch-name] //delete locally available remote branch (e.g git branch -dr origin/test)
git push origin --delete [branch-name] //delete remote branch (remember origin is a local repo-name)
git merge [branch-name] //merge changes of (branch-name) into the working/active branch


### Fast-Forward Merge
A type of merge of two branches where one branch commits history ahead of second branch and second branch don't have its own commits. In this case NO additional commit is generated.

For Example we created 'dev' branch from 'main', at this point 'dev' branch contains all the 'main' branch commits, now let we add additional commits in 'dev' branch only, by this 'dev' branch is ahead of 'main' and let say 'main' don't have its own additional commit. NOW if we merge 'dev' commits to 'main' it is consider as Fast-Forwarded Merge.

### Merge-Commit
In this case both branches have it's own addtional commits. Here difference of additional commit is created in the active branch of type merge and can be seen in the history/log.

### Rebase
Rebase is a branch merge case in which we don't want to see the splitting of commit that merge from another branch. What it does it actually streamline commits (single straight line) in a way that the difference commits merging from other branch to the active branch are the commits of an active branch. While merge (through merge command) give split history to show at which branch is splitted and merged at which point.

git rebase [branch-name]
Rebase works in a steps given below

First rebase save the active branch commits saved away at a side.
Secondly add the commits (difference commits) of second branch to the active branch first in a single line.
Finally after that applying the active branch commits (that are saved away at a side) in a line with new commit (but change affect are the same). and this commit hash is different from previous ones.
This will give the affect even after merging that all the commits done on active branch

### Short live / Long live Branches
In short live branches where we need to work on a small task of specific feature where we complete task merge into other branch and remove that branch. In Long live branches e.g production, development, testing etc these branches use in long run.

### Git Workflows
It is a feature of Github not git.
It set the standards (rules/regulation) for development, communication, code review/management when working in a team.
Each branch serve it's own purpose. (Branch examples below)
master
development
feature/rss-feed
hotfix/missing-link
For example one of the team member working in a specific feature branch; after finishing his/her work, team member create pull request to review code by team lead/manager to merge in development branch. Once the team lead satisfy with the code then he/she can merge in development branch. This is git-flow

### Additional Commands
git config --global user.name "[username]" // setup username
git config --global user.name // display the setuped username
git config --global user.email "[email]" // setup email
git config --global user.email // display the setuped username
git log // check the history of commits
git log [branch-name-1..branch-name-2] // display difference of commits (commits that are in "branch-name-2" but not in "branch-name-1")
git log [repo-name]/[branch-name] // display commit history of specific branch of remote repo



### Conflict in git
conflict happens when you try to merge two branches and changes occur at same file on the same line. To resolve conflict you must review it to keep both changes or changes of any specific branch, the easy way to the change through UI tool.

### Stash in git
To save changes temporarily if you don't want to commit.

git stash OR git stash save [provide-name] // save changes temporarily to clipboard
git stash list // show list of available stash
git stash apply [stash-name] // apply the stash and keep that in the stash list e.g git stash apply stash@{0} (here stash-name is not the name that you suggest to save)
git stash clear // clear all the stashes
git stash pop // pop the last stash from list (also remove from stash list)
git stash drop [stash-name] // drop and remove the stash (e.g git stash drop stash@{0})


### Forking in github
Remember forking is a feature of Github. It clone/copy the repository into your online github account, from there you can clone into your local repostiory; do changes and can push the changes into the copy of your git hub repository and from there you can create pull request for the owner to merge the changes into the origional repository (now it is upto the owner of the repository to merge the changes or not into the original)

Your github forked copy could be behind from owners copy for that you can connect with owner copy as well to pull the changes from CLI. (one way is that you can sync fork from github and then pull that changes into your local repo)

git remote add upstream [owners-copy-link] // ('upstream' is a conventional name working with forked remote repos and 'origin' of your remote repos)
git pull upstream [branch-name]



### .gitignore
Those files and folder that you might want git don't see; create file with extension .gitignore and write it in that file. Example below is an specifying of ignoring some files and folder

/folder-name/
*.txt
*.mp4
*.node_modules