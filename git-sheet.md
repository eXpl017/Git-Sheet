## GIT
----

### Below are the basic, really basic stuff regarding GIT. Use the manual and internet for further help.
======================================================================================================
  - check version
	```git --version```

  - getting help for git command:
	```
	git <cmd> -help		# for git command specific help
	git help --all		# see all possible commands
	```

  - initialise a repo, go to folder and then do following
	```git init```

  - once file added/modified/deleted, check status:
	```git status --short```    OR    ```git status```

	- two types of files:	
		- tracked and untracked
		- tracked: git knows about them, are added to repo, changes are being tracked so can go back to prev self
		- untracked: present in dir, but not added to repo by git, changes not being tracked

	- in short status, flags are:
		- ?? \- Untracked files
		- A \- Files added to stage
		- M \- Modified files
		- D \- Deleted files

  - add files for tracking:
	`git add <file-name>`    OR    `git add .`    OR    `git add --all / git add -A`
	- *--all* is for staging all changed files

  - before commiting, need to specify who you are:
	`git config --global user.name "<name>"`    AND    `git config --global user.email "<email>"`
	- *--global* is used to set this for all the repos you create, can be omitted if you wanna use other accuont at other places

  - commit files to repo:
	`git commit -m "<commit message here>"`

	- when changes in file are very small:
		- `git commit -a -m <message>`
		- *-a* is for automatically staging any changed, already tracked file

  - view commit log
	- `git log`
	- `git log --oneline`    # to see commit in a single line

  - create new branch and switch
	- `git branch <name>`    AND    `git checkout <name>`		# for creating andd then switching to it
	- `git checkout -b <name>`		#creates new branch and switches to it simultaneously

  - merge branch
	- switch to master branch, then
		```git merge <branch-name>```

  - delete branch
	```git branch -d <name>```

  - what is revert?
	- taking an old commit and adding it as a new one.
	- do git log and find the commit you want to revert:
		- if latest commit needs to be reverted:
			```git revert HEAD --no-edit```
			- HEAD points to the latest commit, and --no-edit skips the commit message (but adds the default commit message)
		- if earlier commits need to be reverted:
			```git reveert HEAD~i --no-edit```
			- i here is a number, 1 means go back 1 more commit, 2 means go back to 2 more commits ....(if you wanna go 2 commits back, HEAD~1)

  - what is reset?
	- going back to an earlier commit state, and deleting all changes made after that one
	- find the commit -> note commit-hash -> use commmand to reset:
		```git reset <commit-hash>```
	- even though the commits are not showing up, they arent removed by git.
	- so we can undo the reset if the know the commit-hash of the most recent commit:
		```git reset <recent commit-hash>```

  - what is amend?
	- modify the most recent commit
		```git commit --amend -m "<message>"```

  - dont want file to be tracked by git:
	- make *.gitignore* file, write files to be ignored:
		- \*.log for ignoring all log files
		- temp/ for ingoring whole temp dir	(a lot of regex allowed too, for ignoring files)

  - .gitignore can be seen by others, so to excluded personal local files:
	*.git/info/exclude*	works same as .gitignore but not seen to anyone else


======================================================================================================


### GIT REMOTE
-----------

  - check remote origin:
	```git remote -v```

  - change name or origin to <name>:
	```git remote rename origin <name>```

  - add origin as <name>:
	```git remote add origin <name>```

NOTE: by convention, keep own repo as "origin" and the og from where you forked as "upstream"

  - add remote repo as origin to local repo:
	```git remote add origin "<repo url>"```

  - push changes to remote:
	```git push --set-upstream origin <branch name>```

  - get all changes in repo for a branch and merge the changes in your local:
	combination of two:
		fetch and merge:
			```
			git fetch origin
			git merge origin/master
			```
	one shot:
		pull:
			```git pull origin```

  - show diff between origin/master and local master:
	```git diff origin/master```


======================================================================================================


### GIT FORK
---------

fork anothers repo on github or other hosting platforms
this repo now available as your own repo (copy)
clone this repo to your local and contribute
push changes to your own repo


=======================================================================================================


### Connect GIT and Github
-----------------------

authenticating using passphrase is not allowed now, can do using keys.

create new pair of keys:
	```
	ssh-keygen -t rsa -b 4096 -C "<any comment here/can omit>"		# can press enter when asked for file location, passphrase or set them according to your needs
	```

when you clone, use ssh link
set origin to ssh link, if it is http link then you will be asked uname/pass which doesnt work as a mean to auth anymore
	```
	git remote set-url origin <link>		# can be other stuff instead of origin too, like upstream
	```

to clone your private repos, you need to generate PAT (Personal Access Tokens):
	Settings -> Developer Settings -> Personal Access Tokens
	can create Tokens (classic):
	do create new token -> fill a note -> tick repo (without which you cant clone private repo)
		-> Create
	once you have the token, clone this way:
		```git clone https://<token>@github.com/<account>/<repo>```

NOTE: the above is needed only for the http link and not the ssh link, ssh link directly uses the keys to auth and 
	  clones the repo


=======================================================================================================
