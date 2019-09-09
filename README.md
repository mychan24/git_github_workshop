# 1. Setting up git
## 1.1  Download git

* Mac Users: https://git-scm.com/downloads
* Windows User: https://github.com/git-for-windows/git/releases/tag/v2.23.0.windows.1
	

## 1.2 Configuring git 
This user name and email will be associated with your subsequent Git activity, which means that any changes pushed to GitHub, BitBucket, GitLab or another Git host server in a later lesson will include this information.

### Setup username and email
> git config --global user.name "Your Name"

> git config --global user.email "Your Email"


### Setup the correct linebreaks encoding depending on your OS
**Mac/Linux**
> git config --global core.autocrlf input

**Windows**
> git config --global core.autocrlf true

### Setup "nano" as the text editor to interface with git
> git config --global core.editor "nano -w"

#### Helpful links to setting up git 
https://help.github.com/en/articles/configuring-git-to-handle-line-endings#platform-all



# 2. Creating a Repository (git init)
## 2.1 Create a directory in your Desktop for this workshop
```
cd ~/Desktop
mkdir workdir
cd workdir	
```

## 2.2 Create a repository, where git store versions of your file
```
git init
```

Check that a hidden folder `.git` has been created
> ls -a 

Check the status of git
> git status

# 3. Tracking Changes (git add & git commit)

## 3.1 git add & git commit
Make sure you are in the correct directory
> cd ~/Desktop/workdir

Make a new file `foo.txt`
> touch foo.txt

Check the status
> git status

If there are **untracked files**, we would like to add those files so git will track their changes:
> git add foo.txt

Check the status again, `foo.txt` should now be ready to get committed (a commit is a revision to your files).
> git status

Commit the file and note the identifier for this commit (e.g., `f22b25e`):
> git commit -m "Add foo.txt to repo"

What have we done so far? Lets check the log, which list all the commits made so far. 
> git log

## 3.2 git diff
Add some text to the file `foo.txt`
> echo hello >> foo.txt

Check what has changed between your last commit and now:
> git diff

Add & commit your changes to `foo.txt`
> git add foo.txt

> git commit -m "Add hello in foo.txt"

Check the status and log again (`git status` and `git log`)

###  Notes

* Git does not track an empty directory, so until a directory has a file in it, git would not track it. 
* `git add` adds file to a **staging area**, and `git commit` save these changes in the staging area to the repository.

