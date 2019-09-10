# **Git**

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

### Check to ensure settings are correct
> git config --list

#### Helpful links to setting up git 
https://help.github.com/en/articles/configuring-git-to-handle-line-endings#platform-all


# 2. Creating a Repository (`git init`)
## 2.1 Create a directory in your Desktop for this workshop
```
cd ~/Desktop
mkdir workdir
cd workdir	
```

## 2.2 Create a repository, where git store versions of your file

Create a repository within a folder
> git init

Check that a hidden folder `.git` has been created
> ls -a 

Check the status of git
> git status

# 3. Tracking Changes (`git add & commit`)

## 3.1 Adding new files/modification to staging area (`git add`)
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

## 3.2 Saving these changes to the repository (`git commit`)

Commit the file and note the identifier for this commit (e.g., `f22b25e`):
> git commit -m "Add foo.txt to repo"

What have we done so far? Lets check the log, which list all the commits made so far. 
> git log

## BONUS - Checking what has changed before add/commit (`git diff`)
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



# 4. Exploring History (`git diff & show`)
## 4.1 Difference between current file and N commit ago (`git diff HEAD`)
Lets add another line to `foo.txt`
> echo world >> foo.txt

Check what is different from your current version of foo.txt compare to the last commit
> git diff HEAD foo.txt

Check difference compare to two commits ago
> git diff HEAD~1 foo.txt

Check difference against a specific commit based on identifer (the unique identifier is different for you, use `git log` to check!)
> git diff 7be71q foo.txt 

## 4.2 What was done in ____ commit? (`git show`)
Sometimes we want to check what was done during a certain commit (instead of comparing differences)
> commit show HEAD~1 foo.txt

# 5. Reverting to a previous commit (`git checkout`)
## 5.1 Going back to a specific version of a file (`git checkout`)
Before going back to a previous state of a file, COMMIT what you have now
> git add foo.txt

> git commit -m "Add world"


Recover the `foo.txt` that doesn't have "world" in it (use HEAD~1 or unique identifier)
> git checkout HEAD~1 foo.txt

Check what is in `foo.txt`
> cat foo.txt

Go back to the state where "world" was in the file
> git checkout HEAD foo.txt


## 5.2 Going back to an entire commit - Detached HEAD (CAUTION)
If you `git checkout` a previous commit without also specifying a file, you will revert the entire directory to a previous condition
> git checkout HEAD~1 

You should get a message like this
```
You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -b with the checkout command again. Example:

 git checkout -b <new-branch-name>
```

Use `git checkout HEAD` to return to most recent state. IF you checkout a previous commit without first committing your current state, then anything not committed would be lost!!!


# 6. Telling git to ignore certain files
Make a file named `.gitignore` (you can also use nano/any-text-editor to do it)
> touch ignore_this.txt
> echo ignore_this.txt >> .gitignore

Try `git add ignore_this.txt`, and you will see git will not add it. 

If you want to `add` a suppsoedly ignored file, use `-f`
> git add -f ignore_this.txt


# **Github and other remote hosts**


# 7. Git is not Github

Thus far, everything is within your local computer and done using `git`. That is the **version control** portion of git, which is important and powerful. However, what makes git a efficient tool for collaboration is its power to share through remote hosts like **Github**.

* Github is not the only option, there are other companies that offer free remote hosting, here are a few alterantives [Bitbucket](https://bitbucket.org/), [Gitlab](https://gitlab.com/)

## 7.1 Git is a remote server that hosts a repository (remote host)

Remember `git init` makes a `.git/` folder in your project. That is a local repository (local=lives on your computer).

Github is essentially a remote server that hosts a `.git/` folder. 
Github also comes with tons of tools to help you visualize and manage your repository.

## 7.2 Create aa repository in on github (a remote repo)

* Navigate to https://github.com/your_username
	+ Click **Repositories** tab
	+ Click **New**
	+ Enter workdir as the Repository name, click **Create repository**

**You now have an empty remote repository and some instructions to populate it!**


# 8. Storing codes on Github

**Key terms/commands:**

**git push**: a commmand to upload your code to a remote repository (like Github!)

## 8.1 Push an existing repository from your local computer
Go back to the loacl directory, workdir that we made in previous sections. 
> cd ~/Desktop/workdir

Add the github repo you just made as a remote repository that you want to push your data to
> git remote add origin https://github.com/your_username/workdir.git

Push your local repository to your Github
> git push –u origin master

## BONUS - SSH keys
Here is a link to help you setup using SSH keys for authentication with Github
https://help.github.com/en/enterprise/2.15/user/articles/adding-a-new-ssh-key-to-your-github-account


# 9. Getting a repository from Github (fork & `git clone`)

**Key terms/commands:**

* **fork**: copy someone's Github repository and putting it in your Github 
* **clone**: copy (download) a remote repo onto your local computer 

## 9.1 Fork a repository (remote -> remote)

**Fork** this repository that you are reading this README file into your github.

* Click the **Fork** icon near the top right corner 
* ...It will take a little while to load...
* You should be redirected to a copy of the same repository in YOUR Github account

## 9.2 Cloning a repository (remote -> local)

**Clone** YOUR git_github_workshop repository onto your local computer: 

> git clone https://github.com/your_username/git_github_workshop.git ~/Desktop/git_github_workshop


# 10. Collaborating (`git fetch & merge`)
**Key terms/commands:**

* **git fetch**: look at the changes that is in your remote repository Github. This commands download the changes into the `.git/` folder so you can compare changes to your local files, but it does not actually modify your files (i.e., files outside of the `.git/` folder). 

* **git pull**: implement the changes you have *fetched* into your local files. 

## 10.1 Setup a fake collaborator, yourself in another directory :) 

Clone the **workdir** repo into your local computer but a different folder as if you have a collaborator
> git clone https://github.com/your_username/workdir.git ~/Desktop/workdir_fake_collab
	
Lets pretend you are the collaborator, and you will make some changes and push it to Github
> cd ~/Desktop/workdir_fake_collab

> touch foofoo.txt

> git add foofoo.txt

> git commit -m "Add foofoo.txt"

> git push origin master


Lets check what is in the current folder 
> ls

Check what is on the workdir repository on Github. It should contain `foofoo.txt`

But what about the original `workdir` folder? 

> cd ~/Desktop/workdir

> ls

`foofoo.txt` should be missing. Now lets say you want to check what changes your collaborator made. 

## 10.2 Implement the changes your fake collaborator made

**fetch** the changes your fake collaborator pushed to Github onto your local computer. 
> git fetch

NOTE that this does not change the files in your directory. But now you can use `git diff` to see what your collaborator has changed
> git diff master origin/master

**Merge** the changes into your local files if you decided these are changes you want (the origainl `workdir`)
> git merge

**Pull** is **fetch** + **merge**. If you are sure you want the changes in the remote repo without first checking the difference out locally, you can use one command to perform both fetch and merge. 

> git pull

## Notes
* `git merge` returns message "Already up to date." when there are changes in the remote.
	+ `git merge` impelment the changes that were fetched by `git fetch`, so fetch first. 
* Will `git fetch` change my stuff? 
	+ Fetching does not change your local file until your pull. 

## BONUS - What is my remote?
What is your remote? 
> git remote -v

Adding a different remote
> git add remote [name] [url]

Changing the URL of the remote (e.g., you change the remote repository)
> git remote set-url [name] [newurl]


## 10.3 Really collaborating on Github

* Adding collaborators in your Github repository
	+ Click **Settings**
	+ Click **Collaborators** and add them (they need to be on Github)
	
* More Advance way to collaborate (won't cover in detail)
	+ **fork** a repository you want to make changes 
	+ **git clone** it to your local computer
	+ Make changes, **git add**, **git commit** and **git push** it to your forked remote repo
	+ Make a [Pull Request](https://help.github.com/en/articles/creating-a-pull-request) in the original repository


# 11. Conflicts

**Key terms/commands:**

* **Conflict** is when the same portion of a file is edited, it will have to be manually resolved before it can be pulled/pushed.

## 11.1 Create a conflict

Go into your fake collaborator's folder and add a line to `foo.txt`

> cd ~/Desktop/workdir_fake_collab

> echo fake_colab >> foo.txt

Add, commit and push the changes to the remote repository 

> git add foo.txt

> git commit -m "Add fake collab line to foo.txt"

> git push

Now go into the original `workdir` and add a different line to `foo.txt`

> cd ~/Desktop/workdir

> echo real_me >> foo.txt

Add and commit the change

> git add foo.txt

> git commit -m "Add real me line to foo.txt"

Try to push it, and you should get an error

> git push

## 11.2 Resolving a conflict

Pull the changes from the remote server, which your fake collab has made a change

> git pull

This should result in a conflict message. Two versions of the conflicting line is shown: 

* Your local version is between <<<<<<< HEAD` and `=======`
* The remote version is between `=======` and `>>>>>>> (unique identifier of the commit)`

Edit the file with conflicting lines

> nano foo.txt

Then add and commit the edited file

> git add foo.txt

> git commit -m "Merge changes from Github"

Push your changes to the remote repo

> git push

Now we pull from the remote repo again


## Tips to prevent conflicts

* Always fetch/merge (or pull) before making changes locally
* Use **branches** 
* Commit often (so people can pull your changes frequently as well)
* Have smaller files, so it is less likely for multiple people to edit the same file. 
* Communicate often with your collaborators :) 



