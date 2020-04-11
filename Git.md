# Git
[TOC]

**This is a simplified usage of git**

1. git commit --amend -m "amended comment"
2. git checkout -d deprachted_branch
3. git checkout -b new_branch
4. git log --graph: view the merge graph from different branches
5. git stash / git stash pop / git stash list



## Undo / Amend commit

```
git commit --amend
```

### Unstage file

``` 
git reset HEAD <file>
```

### Unmodify file

```
git checkout -- <file>
```



## Git Commit



## remove local untracked files from the current Git branch
## Issue: The following untracked working tree files would be overwritten by merge
common command:

```
git clean -fdx
```

```
git clean
-f: force to remove
-d: remove directories
-x: remove all untracked files(ignored files and files unknown to Git)
-X: remove only files ignored by Git
```



# Git Branch

***Branch can be seen as a pointer to one of those commits.***

**HEAD:** points to the current working branch.

**Creating a new branch and switching to it at the same time**

```
git checkout -b <newbranchname>
```

The branch and the HEAD branch point to the same series of commits.

### show remote branches

``` 
git remote show <remote>, i.e. git remote show origin
```

## Merge branches

```
git merge <branche-to-be-merged>
```

## Delete branch

```
git branch -d <branch>
```



## Git get remote branch to local

Common command:

```
git checkout --track <remote>/<branch>
```

which is equivalently to ```git checkout -b <branch> <remote>/<branch>```

if the branch doesn’t exist and exactly matches a name on only one remote,

```
git checkout <branch>
```

If want to rename the branch from remote:

```
git checkout -b <rename> <remote>/<branch>
```

git checkout -- file

```
git branch -vv
git fetch --all: fetch all the changes on the server that local doesn't have yet. 
```

force switch branch

```
git checkout -f <branch>
```



## Remove files

1. remove files from projects

```
git rm <filename>
```

2. remove it from stages area and not tracking anymore

```
git rm --cached <filename>
```

Git: fatal: Pathspec is in submodule
https://stackoverflow.com/questions/24472596/git-fatal-pathspec-is-in-submodule

git rm --cached directory
git add directory



## Squash commits

### Squash commits in one branch

```
git rebase -i HEAD~<n>
```

### Squash commits with merge operation

```
git reset --soft <commit>
git commit
```



https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History#_squashing



## Git Reset

`git reset` moves the branch that HEAD is pointing to.

`git checkout` moves the HEAD to another branch. 

<img src="C:\Users\qingl\ws\Drafts\checkout_and_reset.png" alt="image-20200222214333289" style="zoom:50%;" />

```
--soft: undo the last several commit without changing the index or working directory
--mixed (the default option): undo the last several commit and change the index
--hard: undo the last several commit, change the index and working directory
```

**--hard** option make `git reset ` operation dangerous. 



## Git Recover

```
git reflog: recover the commited files. 
```







## Update Local Branch

```
Force update: git reset --hard <remote>/<branch>
Keep commit: git push <remote>
Keep changes: git merge --abort, git reset --merge, git pull
git stash && git pull && git stash pop

```



## ~ and ^

```
~: navigate between parent commits
^: navigate between merge commits
```

Reference: [Caret and Tilde](https://stackoverflow.com/questions/2221658/whats-the-difference-between-head-and-head-in-git)

## [Git log](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History)

example:

```
git log --color --format=format:'%C(bold yellow)%h%C(reset): %C(bold green)(%an)%C(reset) %C(bold white)<%ad>%C(reset)%n''  %C(bold cyan)%s%C(reset)' --abbrev-commit --graph
```

Reference page:



## Git clone

```
git clone <.git>
```

clone one of the branches：

```
git clone -b <branch> <.git>
```

