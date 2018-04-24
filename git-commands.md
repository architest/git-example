# Git Commands

This is a set of recipes to use Git, partly based on a very good tutorial in
'Real Python' called [Introduction to Git and GitHub for Python Developers](https://realpython.com/python-git-github-intro/)

## Basic, day-to-day commands

1. Initialize a new local repository (repo) from scratch: Create a directory, get into it, and use 'git init'
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

5. Create another file and add it to repo. Original `hello.py` was also modified, so it must be again added and commited
```
touch myname.py
git add hello.py myname.py
git status
git commit -m "Added myname module. Minor modification to hello.py"
```

6. The `.gitignore` file is special, because it contains the names of the files which should be ignored by Git, like for instance, python `.pyc` files. It is Ok to use wildcards inside it
```
vim .gitignore
git add .gitignore
git commit -m "created .gitignore"
```

7. See a log of the changes. This can be verbose when you have commited many changes
```
git log
```

8. Make a change in `.gitignore`, but then changed your mind and **drop it**. Change file back to where it was at last commit
```
vim .gitignore
git checkout -- .gitignore
```

9. Decided to apply and commit other change
```
vim .gitignore
git status
git add .gitignore
git commit -m "modifying .gitignore to exclude all .pyc files"
```

10. Take a look at what is different from our last commit. In this case we want the diff of our most recent commit, and we can refer to it using **_HEAD_**
```
git diff HEAD
```

11. We can unstage files by using the `git reset` command
```
git reset octofamily/octodog.txt
```

## Handle branches

# To see all branches
git branch

# To create a new branch AND MOVE THERE
git checkout -b my_new_feature

# To see all branches again (current branch is marked with '*')
git branch

# Back to the top of the main branch (master)
git checkout master

# Change back to new branch
git checkout my_new_feature

# Add a change in the NEW 'my_new_feature' branch
git add hello.py
git commit -m "Added code for feature x"

# Get back to the top of the master branch
git checkout master

# Compare the state of two branches
git show-branch my_new_feature master
git show-branch my_new_feature
git show-branch master

# 'HEAD' is where the repository is currently pointing to (last commit in
# 'my_new_feature')
git show-branch HEAD

# This is like regular 'show-branch' but using SHA codes instead of names
git show-branch --sha1-name my_new_feature master

# Go back to 'master' and MERGE changes from 'my_new_feature' to 'master'
git checkout master
git merge my_new_feature

# Removing a branch which is no longer needed
git branch -d my_new_feature

# Checkout (use) the repository at an specific point in time (98011e69...)
# The long number is the (unique) SHA code
git checkout 98011e69fda0df3937e99e2d7ac11ca3a1e37959


## Miscellaneous instructions

# Rename a file
git mv <old-file> <new-file>
git commit -m "Renaming file"

# Removing files (wildcards are also valid)
git rm <target-file>

# Removing directories
git rm -r folder_of_cats

# Set user email and name _for every repository_ in your computer
git config --global user.email "user@example.com"
git config --global user.name "User Surname"

# Set user email and name _for a single repository_
git config user.email "user@example.com"
git config user.name "User Surname"


## Handling remote repositories

# Download a full repository
git clone https://github.com/jima80525/github-playground.git

# Download to the current computer the changes in an already present repository
git pull https://github.com/architest/git-example

# Upload the local changes to GitHub:
git push https://github.com/architest/git-example master

# 'origin' is an alias for server repository (if we started by cloning a repo)
git push origin master

# The same, but the '-u' option tell Git to remember the parameters, so
# afterwards we only need to write 'git push'
git push -u origin master

# Pulling, but in a more compact way
git pull origin master

# Add a remote repository to push our local repo to the GitHub server
git remote add origin https://github.com/try-git/try_git.git


## Configure Git to sync your fork with the original repository

- First, fork the repository using GitHub facilities for that

  Original repository is: https://github.com/jima80525/github-playground.git
  The forked repository is: https://github.com/architest/github-playground.git

- Then, clone the repository to the local machine

git clone https://github.com/architest/github-playground.git

- Get into the cloned repository. It is good to check the current configured
  remote repository

git remote -v

  The result should be something like:

origin  https://github.com/architest/github-playground.git (fetch)
origin  https://github.com/architest/github-playground.git (push)

- Add the path to the original repository

git remote add upstream https://github.com/jima80525/github-playground.git

- Verify that it worked:

git remote -v

origin  https://github.com/architest/github-playground.git (fetch)
origin  https://github.com/architest/github-playground.git (push)
upstream    https://github.com/jima80525/github-playground.git (fetch)
upstream    https://github.com/jima80525/github-playground.git (push)

- Now, in order to fetch changes from the 'upstream' repository you do:

git fetch upstream

- Possible changes are in 'upstream/master'. Make sure you're in 'master':

git checkout master

- Merge changes from 'upstream/master' into local 'master' branch

git merge upstream/master

- Updated!!!


Simple git workflow:
====================

1. git status – Make sure your current area is clean.
2. git pull – Get the latest version from the remote. This saves merging
   issues later.
3. Edit your files and make your changes. Remember to run your linter and do
   unit tests!
4. git status – Find all files that are changed. Make sure to watch untracked
   files too!
5. git add [files] – Add the changed files to the staging area.
6. git commit -m "message" – Make your new commit.
7. git push origin [branch-name] – Push your changes up to the remote.
