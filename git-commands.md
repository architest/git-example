# Git commands

This is a set of recipes to use Git, partly based on a very good tutorial in
'Real Python' called [Introduction to Git and GitHub for Python Developers](https://realpython.com/python-git-github-intro/)

## Basic, day-to-day commands

1. Initialize a new local repository (repo) from scratch: Create a directory, get into it, and use `git init`
```
mkdir my_new_repo
cd my_new_repo
git init
```

2. See current status. Very useful instruction, and used very often
```
git status
```

3. Create new file in repo. Now file exists, but it is _untracked_ by Git
```
echo "print('Hello World')" > hello.py
git status
```

4. Add new file to Git tracking. Now it is tracked but it is not yet part of the repo. It is in the **_staging area_**
```
git add hello.py
git status
```

5. Commit a change, adding a comment. Now `hello.py` belongs to repo
```
git commit -m "Creating hello.py"
git status
```

6. Create another file and add it to repo. Original `hello.py` was also modified, so it must be again added and commited
```
vim myname.py
vim hello.py
git add hello.py myname.py
git status
git commit -m "Added myname module. Minor modification to hello.py"
```

   - Instead of specifying each file in the `git add` line, we can do:
```
git add --all
```

7. The `.gitignore` file is special, because it contains the names of the files which should be ignored by Git, like for instance, python `.pyc` files. It is Ok to use wildcards inside it
```
vim .gitignore
git add .gitignore
git commit -m "Created .gitignore"
```

8. See a log of the changes. This can be verbose when you have commited many changes
```
git log
```

9. The command `git log` provides, besides the commit messages of the changes, the **_SHA_** ID of every commit. Then, one can use the command `git show SHA` to get a detailed description of the changes related to that commit:
```
git show fcf22e5d3cf1c
```

10. You made a change in `.gitignore`, but then changed your mind and **dropped it**. This instruction changes the file back to where it was at last commit
```
vim .gitignore
git checkout -- .gitignore
```

11. You decided to apply and commit other change
```
vim .gitignore
git status
git add .gitignore
git commit -m "Modifying .gitignore to exclude all .pyc files"
```

12. Take a look at what is different from our last commit. In this case we want the diff of our most recent commit, and we can refer to it using **_HEAD_**
```
git diff HEAD
```
If what we want to check is whether we are about to commit a file with whitespace errors, let's use:
```
git diff --check
```

13. We can unstage files by using the `git reset` command
```
git reset octofamily/octodog.txt
```

## Recover files or folders accidentaly deleted

1. Files are deleted from working tree but not commited yet:
```
git checkout -- path/to/folder
```
If deletion was already indexed, it must be reset first:
```
git reset -- path/to/folder
git checkout -- path/to/folder
```

2. Restore the full working tree, but lose all uncommitted changes:
```
git reset --hard HEAD
```

3. When files are deleted in some commit in the past:
Find the last commit that affected the given path. As the file isn't in the HEAD commit, this commit must have deleted it.
```
git rev-list -n 1 HEAD -- <file_path>
```
Then, with the output provided by the former command (a SHA1 string), checkout the version at the commit **_before_**, using the caret (**_^_**) symbol:
```
git checkout <deleting_commit>^ -- <file_path>
```

4. Restore the full working tree from a distant commit:
```
git reset --hard <revision>
```

5. It is possible to use the following command to get all the commits which have deleted files and the files deleted:
```
git log --diff-filter=D --summary
```

## Compare files between different commits

1. The `git-diff` man page states:
```
git diff [--options] <commit> <commit> [--] [<path>...]
```
For instance, to see the difference for a file `main.c` between now and two commits back, here are three equivalent commands:
```
git diff HEAD^^ HEAD main.c
git diff HEAD^^..HEAD -- main.c
git diff HEAD~2 HEAD -- main.c
```

2. You can also use `git log` or `gitk` to find the **SHA1s** to use, in case the commits are very far appart. And you can use this approach to compare whole commits, not only one file:
```
git diff (sha-id-one) (sha-id-two)
```

3. You can also compare two different files in two different revisions, like this:
```
git diff <revision_1>:<file_1> <revision_2>:<file_2>
```

## Handling branches

1. To see all branches
```
git branch
```

2. To create a new branch _AND MOVE IN THERE_
```
git checkout -b my_new_feature
```

3. To see all branches again (current branch is marked with '\*')
```
git branch
```

4. Back to the top of the main branch (**_master_**), and confirm we are indeed there
```
git checkout master
git branch
```

5. Change back to the new branch. Confirm we are where we want
```
git checkout my_new_feature
git branch
```

6. We are inside the **NEW** `my_new_feature` branch, so further changes will go in there
```
vim hello.py
git add hello.py
git commit -m "Added code for feature x"
```

7. Get back to the top of the `master` branch
```
git checkout master
```

8. Compare the state of two branches
```
git show-branch my_new_feature master
git show-branch my_new_feature
git show-branch master
```

9. `HEAD` is where the repository is currently pointing to (in this case, the last commit done in `my_new_feature`)
```
git show-branch HEAD
```

10. This is like regular 'show-branch' but using SHA codes instead of names
```
git show-branch --sha1-name my_new_feature master
```

11. Go back to `master` and **MERGE** changes **FROM** `my_new_feature` **TO** `master`
```
git checkout master
git merge my_new_feature
```

12. Removing a branch which is no longer needed
```
git branch -d my_new_feature
```

13. This is for checking out (use) the repository at an specific point in time (98011e69...). The long number is the (unique) SHA code
```
git checkout 98011e69fda0df3937e99e2d7ac11ca3a1e37959
```

## Miscellaneous instructions

1. Rename a file
```
git mv <old-file> <new-file>
git commit -m "Renaming file"
```

2. Removing files (wildcards are also valid)
```
git rm <target-file>
git commit -m "Removed target file"
```

3. Removing directories
```
git rm -r folder_of_cats
git commit -m "Removed directory 'folder_of_cats'"
```

4. Set user email and name _for every repository_ in your computer
```
git config --global user.email "user@example.com"
git config --global user.name "User Surname"
```

5. Set user email and name _for a single repository_
```
git config user.email "user@example.com"
git config user.name "User Surname"
```

6. Several aspects of Git behavior, like aliases, may be set up at file `~/.gitconfig`. An example content could be:
```
[user]
    name = architest
    email = 23104729+architest@users.noreply.github.com
[color]
    ui = true
[alias]
    co = checkout
    br = branch
```

## Handling remote repositories

1. Download (_clone_) a full repository
```
git clone https://github.com/jima80525/github-playground.git
```

2. **Download** (_pull_) to the current computer the changes in an already present repository
```
git pull https://github.com/architest/git-example
```

3. **Upload** (_push_) the local changes to GitHub:
```
git push https://github.com/architest/git-example master
```

4. '**origin**' is an alias for the remote server repository (if we started by _cloning_ a repo), so the former instruction can be abbreviated as:
```
git push origin master
```

5. The same, but the `-u` option tell Git to remember the parameters, so afterwards we only need to write `git push` (some conditions may apply)
```
git push -u origin master
```

6. _Pulling_, but in a more compact way
```
git pull origin master
```
'Pulling' can be seen as the combination of two commands: `git fetch`, which fetches down all the changes on the server that we don't have yet, but doesn't modify the working directory, and `git merge`, which combines remote and local data.

7. Add a remote repository to push our local repo to the GitHub server (i.e.: We created our repository from scratch, and we are setting `origin` in order to be able to _push it_ to a remote server)
```
git remote add origin https://github.com/try-git/try_git.git
```

8. In order to make a _tracking branch_, i.e., a local branch that automatically tracks a remote branch, we can do:
```
git checkout -b serverfix origin/serverfix
```
In this way, the local _serverfix_ branch tracks the remote _serverfix_ branch in _origin_. A shorthand for the former operation is:
```
git checkout --track origin/serverfix
```
If the local branch doesn't exist, and you know the (unique) name of the branch in the remote, we can even do:
```
git checkout serverfix
```
If one wants to use a different name for the local branch (_myfix_ in this example):
```
git checkout -b myfix origin/serverfix
```

9. In order to see which tracking branches have been setup, we use the `-vv` option with `git branch`:
```
 git branch -vv
        iss53     7e424c3 [origin/iss53: ahead 2] forgot the brackets
        master    1ae2a45 [origin/master] deploying index fix
      * serverfix f8674d9 [teamone/server-fix-good: ahead 3, behind 1] this should do it
        testing   5ea463a trying something new
```
Or, even better, to get completely up-to-date numbers from all tracked remotes:
```
git fetch -all
git branch -vv
```

## Configure Git to sync your fork with the original repository

1. First, fork the repository using GitHub facilities for that

   - Original repository is: https://github.com/jima80525/github-playground.git
   - The forked repository is: https://github.com/architest/github-playground.git

2. Then, clone the repository to the local machine
```
git clone https://github.com/architest/github-playground.git
```

3. Get into the cloned repository. It is good to check the currently configured remote repository
```
git remote -v
```

  The result should be something like:
```
origin  https://github.com/architest/github-playground.git (fetch)
origin  https://github.com/architest/github-playground.git (push)
```

4. Add the path to the original repository
```
git remote add upstream https://github.com/jima80525/github-playground.git
```

5. Verify that it worked:
```
git remote -v
```
```
origin  https://github.com/architest/github-playground.git (fetch)
origin  https://github.com/architest/github-playground.git (push)
upstream    https://github.com/jima80525/github-playground.git (fetch)
upstream    https://github.com/jima80525/github-playground.git (push)
```

6. Now, in order to fetch changes from the `upstream` repository you do:
```
git fetch upstream
```

7. Possible changes are in `upstream/master`. Make sure you're in `master`:
```
git checkout master
```

8. Merge changes from `upstream/master` into local `master` branch
```
git merge upstream/master
```

9. Updated!!!

## Interrupting your work and then resuming it: `git stash`

**NOTE**: This section is adapted from [Advanced Git Tips for Python Developers](https://realpython.com/advanced-git-for-pythonistas/).

1. Suppose that you're working in some feature, have added some files, but it is not yet ready, and then you must clean up your working directory to work in something else, presumably more urgent. That's when `git stash` comes handy:
```
git stash save
```
Or, if you want to add a comment:
```
git stash save "Stored for later"
```
With this, your working directory is _clean_ as far as `git` is concerned, and you can go on to carry out other task (Note: the default option is `save`, so you can only do `git stash`).

2. **_Untracked files_** are not included in the stash. In order to do so the `--include-untracked` option is used:
```
git stash save --include-untracked "Untracked files are now included"
```

3. Then, when you are done with the urgent task and want to come back to your previous work, you do:
```
git stash pop
```
`git` applies the changes stored in the stash, and gets rid of the stash itself.

4. By default, `git stash pop` doesn't store the status of files in the index (they go from **_"Changes to be commited"_** to **_"Changes not staged for commit"_**. In order to keep this status you can use:
```
git stash pop --index
```

5. If you havemore than one stash, then the following instruction comes handy:
```
git stash list
```
The output of this instruction is something like:
```
stash@{0}: WIP on master: 387dcfc adding some files
stash@{1}: On master: the third save
stash@{2}: On master: the second save
stash@{3}: On master: the first save
```

6. In order to know the files that have changes in a specific stash:
```
git stash show stash@{2}
```
Add the `-p/--patch` option to get the diffs in _patch_ format:
```
git stash show -p stash@{2}
```
**Note**: When no name is supplied, git assumes `stash@{0}`.

7. To get a specific stash out of the stack and into our working directory, we need to provide `pop` the corresponding ID:
```
git stash pop stash@{1}
```
To get a given stash into the working directory, but _also_ leave it in the stack as well, the `apply` subcommand is used:
```
git stash apply stash@{1}
```

8. If you need to throw away a given stash without applying it to your working directory, the subcommand `drop` should be used:
```
git stash drop stash@{1}
```

9. It is possible that you want to do a `pull` from some changes, but that doesn't work if you have pending changes in your working directory. For this case, `stash` comes handy:
```
git stash
git pull
git stash pop
```

## Comparing revisions: `git diff`

**NOTE**: This section is adapted from [Advanced Git Tips for Python Developers](https://realpython.com/advanced-git-for-pythonistas/).

1. The command `git diff` by default shows the changes (in _patch_ format) in your working directory that are **not** in your index or in HEAD:
```
$ echo "I'm editing file3 now" >> file3
$ git diff
diff --git a/file3 b/file3
index faf2282..c5dd702 100644
--- a/file3
+++ b/file3
@@ -1,3 +1,4 @@
{other contents of files3}
+I'm editing file3 now
```

2. If file `file3` is added to the staging area, it no longer appears with `git diff`:
```
$ git add file3
$ git diff
[no output here]
```

3. In order to see the changes that are in the index and staged for the next commit, use the `--staged` option:
```
$ git diff --staged
diff --git a/file3 b/file3
index faf2282..c5dd702 100644
--- a/file3
+++ b/file3
@@ -1,3 +1,4 @@
 file1
 file2
 file3
+I'm editing file3 now
```

4. `diff` can be used to compare any two commits in the repo. For instance, if you have the SHAs:
```
$ git diff b3e9b4d 387dcfc
diff --git a/file3 b/file3
deleted file mode 100644
index faf2282..0000000
--- a/file3
+++ /dev/null
@@ -1,3 +0,0 @@
-file1
-file2
-file3
```
Branch names can also be used:
```
$ git diff master tmp
diff --git a/file1 b/file1
index e212970..04dbd7b 100644
--- a/file1
+++ b/file1
@@ -1 +1,2 @@
 file1
+editing file1
```
As well as revision naming methods:
```
$ git diff master^ master
diff --git a/file3 b/file3
new file mode 100644
index 0000000..faf2282
--- /dev/null
+++ b/file3
@@ -0,0 +1,3 @@
+file1
+file2
+file3
```

5. It is possible to restrict the diffs to a single file using the `--` option:
```
$ git diff HEAD~3 HEAD
diff --git a/file1 b/file1
index e212970..04dbd7b 100644
--- a/file1
+++ b/file1
@@ -1 +1,2 @@
 file1
+editing file1
diff --git a/file2 b/file2
index 89361a0..91c5d97 100644
--- a/file2
+++ b/file2
@@ -1,2 +1,3 @@
 file1
 file2
+editing file2
diff --git a/file3 b/file3
index faf2282..c5dd702 100644
--- a/file3
+++ b/file3
@@ -1,3 +1,4 @@
 file1
 file2
 file3
+I'm editing file3 now
```
```
$ git diff HEAD~3 HEAD -- file3
diff --git a/file3 b/file3
index faf2282..c5dd702 100644
--- a/file3
+++ b/file3
@@ -1,3 +1,4 @@
 file1
 file2
 file3
+I'm editing file3 now
```

6. In order to show the files changed in the most recent commit on _master_, we can compare **HEAD** with **HEAD^**:
```
$ git diff HEAD^ HEAD
diff --git a/file1 b/file1
index e212970..04dbd7b 100644
--- a/file1
+++ b/file1
@@ -1 +1,2 @@
 file1
+editing file1
```
If the output is too long and you're only interested in the names of the changed files:
```
$ git diff HEAD^ HEAD --name-only
file1
```

7. When you want the differences to be processed by a given specialized tool, you should first configure `git` to use the right tool (`meld` in this case):
```
$ git config --global diff.tool meld
$ git config --global difftool.prompt false
```
To call the difftool you can use, for instance:
```
git difftool HEAD^ HEAD
```
By the way, all the sintax used to address stashes works with difftool:
```
git difftool stash@{1}
```

## Changing history

**NOTE #1**: This section is adapted from [Advanced Git Tips for Python Developers](https://realpython.com/advanced-git-for-pythonistas/).

**NOTE #2**: The only case when you should modify a commit is when it exists on your local repo **_but not in the remote!_**.

1. The easiest way to modify a commit is when changing it right after commiting it:
```
git commit -m "I am bad at spilling"
git commit --amend -m "I am bad at spelling"
```

2. A _rebase_ operation is similar to a merge, but it can produce a much cleaner history. When you rebase, `git` will find the common ancestor between your current branch and the specified branch. It will then take all of the changes after that common ancestor from your branch and _"replay"_ them on top of the other branch. The result will look like you did all of your changes after the other branch.
Let's suppose that you're in the `my_feature_branch` branch:
```
$ git log --oneline
143ae7f second feature commit
aef68dc first feature commit
2512d27 Common Ancestor Commit
```
And now let's see what is in `master`:
```
$ git log --oneline master
23a558c third master commit
5ec06af second master commit
190d6af first master commit
2512d27 Common Ancestor Commit
```
While still in `my_feature_branch`, let's do a `rebase` to put the two feature commits **after** the three commits on master:
```
$ git rebase master
First, rewinding head to replay your work on top of it...
Applying: first feature commit
Applying: second feature commit
```
```
$ git log --oneline
cf16517 second feature commit
69f61e9 first feature commit
23a558c third master commit
5ec06af second master commit
190d6af first master commit
2512d27 Common Ancestor Commit
```
If you had done a `merge` instead of a `rebase`, there would have been a new commit with the message **Merge branch 'master' into my\_feature\_branch**, and the SHAs of the two feature commits would be unchanged. Doing a rebase avoids the extra merge commit and makes your revision history cleaner.

3. Using a `rebase` can be handy when you’re working on a branch with a different developer. If there are changes on the remote, and you have local commits to the same branch, you can use the `-r` option on the `git pull` command. Where a normal `git pull` does a `merge` to the remote branch, `git pull -r` will `rebase` your commits on top of the changes that were on the remote.
```
git pull -r
```

4. In order to revert a commit that has been done but you don't want, you have the subcommand `reset` with the options `--soft` and `--hard`. The `git reset --soft <SHA>` moves _HEAD_ back to the specified SHA. It doesn’t change the **local file system**, and it doesn't change the **index**.
```
git reset --soft HEAD^
```
After this, whatever file which was added will still be in the index in **_Changes to be commited:_**. The commit message is removed from the history, though. On the other hand, we now call the ``--hard`` option:
```
git reset --hard HEAD^
```
Here is not only the last commit gone, but the affected files have been deleted from the working directory, also. The ``--hard`` option resets you completely back to the SHA you specified.

5. The `git revert` command allows you to easily remove the changes from a given commit **_but does not change the history_**, it only adds a new entry in the log.
```
git revert HEAD
```
This will allow you to change provide a commit message for the revert commit, and will delete the files added by the commit (or will modify them to a previous state). It effectively _undoes_ the changes introduced by the commit, without altering the previous history of changes.

6. To remove files and directories which are **not** under version control, the `git clean` command is used. Given that the changes can't be recovered, you must explicitly pass the `-f` option to make it really work:
```
git clean -f
```
To remove untracked and **ignored** files, the `-x` option is needed:
```
git clean -fx
```
Finally, to remove untracked **directories**, you must pass the `-d` option:
```
git clean -fxd
```


# Simple git workflow:

1. `git status` – Make sure your current area is clean.
2. `git pull` – Get the latest version from the remote. This saves merging issues later.
3. Edit your files and make your changes. Remember to run your linter and do unit tests!
4. `git status` – Find all files that are changed. Make sure to watch untracked files too!
5. `git add [files]` – Add the changed files to the staging area.
6. `git commit -m "message"` – Make your new commit.
7. `git push origin [branch-name]` – Push your changes up to the remote.
