

# Version Control system

**Git** is a **version control system**. It is software **for tracking changes** in any set of files, usually used while collaborating with team on any project. Git’s building block is called “repositories”.

A Git repository is a virtual storage of your project. It allows you to save versions of your code, which you can access when needed. it is called local working directory

**Github** provides a hosting service to store Git repositories and much more.


## Git

A Git _repository_ is, to a large extent, just a big database of _commits_
A remote is simply a copy of the repo _somewhere else_

### .git directory

The **Git directory** (located in `YOUR-PROJECT-PATH/.git/`) is where Git stores everything it needs to accurately track the project. This includes metadata and an object database which includes compressed versions of the project files.
##### commits : 
Commits exist in the `.git/objects` directory **with the first 2 letters as a directory**, and the remaining 38 as a file.

to inspect files within the git's data store
`git cat-file -p <some-sha>`

```
➜ git cat-file -p 48d06ff tree 6282551fedc655bc5ee9180ad67021c22245fdae 
parent 5ba786fcc93e8092831c01e71444b9baa2228a4f 
author ThePrimeagen <the.primeagen@gmail.com> 1706387467 -0700 
committer ThePrimeagen <the.primeagen@gmail.com> 1706387467 -0700 
second
````

```
git cat-file -p 6282551fedc655bc5ee9180ad67021c22245fdae 
100644 blob 9a71f81a4b4754b686fd37cbb3c72d0250d344aa first.md 
100644 blob 7f112b196b963ff72675febdbb97da5204f9497e second.md
```

```
➜ git cat-file -p 9a71f81a4b4754b686fd37cbb3c72d0250d344aa hello world
```

- tree: tree is analagous to directory
- blob: blob is analagous to file

git stores _pointers_ to the ENTIRE worktree, not the entire worktree itself which means its significantly more efficient space wise.

##### branch details :
`cat .git/refs/heads/rewrite`


### Staging area

The **staging area** is a file (also called the "index", "stage", or "cache") that stores information about what will go into your next commit. A commit is when you tell Git to save these staged changes. Git takes a snapshot of the files as they are and permanently stores that snapshot in the Git directory.


#### Index : 

The Git index is a critical data structure in Git. It serves as the “staging area” between the files you have on your filesystem and your commit history. When you run git add , the files from your working directory are hashed and stored as objects in the index, leading them to be “staged changes”.

### Git clone URL / SSh :

How to use ssh for connecting to git? You should put your public key on the github or gitlab account and then clone the repository by using the SSH not URL

### configure your username and email :

- `Git config (–global) user.name "Sahel Bloukat"`
- `Git config (–global) user.email "sahel.bloukat@ancud.de"`

### Git config :

- Git uses a series of configuration files to determine non-default behavior that you may want. **The first place Git looks** for these values is in **the system-wide** **[path]/etc/gitconfig**  **file,** which contains settings that are applied to **every user on the system and all of their repositories**. If you pass the option `--system` to git config, it reads and writes from this file specifically.

- The next place Git looks is the **~/.gitconfig** **(or**  **~/.config/git/config**** ) file **, which is** specific to each user **. You can make Git read and write to this file by** passing the  `--global` option.

- Finally, Git looks for configuration values in the **configuration file in the Git directory (****.git/config****) of whatever repository you're currently usin**g. These values are specific to that single repository, and represent passing the `--local` option to git config. If you don't specify which level you want to work with, this is the default.

- to show the config content 
	- `cat .git/config`

- to add a key value, execute `git config --add <section>.<keyname> <value>`
	- `git config --global --add user.name "Sahel Bloukat"`
	- `git config --local --add user.name "Sahel Bloukat"`

- you can view any value of git config by executing `git config --get <key>`
	- This will grab the latest value from the local version 
	- `git config --get user.name`

- To list all the config elements
	- `git config --list | grep <thing>`
	- `git config --list --local`

config keys are not unique. You can have the same key more than once.

- You can "unset" a value 
	 `git config --unset user.name`
- If there are multiple values for one key then you should use "unset-all"
	 `git config --unset-all user.name`

Each of these "levels" (system, global, local) overwrites values in the previous level, so values in .git/config trump those in [path]/etc/gitconfig, for instance.    




![](Git.png)

### Commits:

 Commit is a point in time representing the project in its entirety.
 Git does not store diffs, git stores complete version of the entire source at the point of each commit. Each commit contains all the information to completely reconstruct the source code that was tracked.
 
 - git commits come with a sha (a hash with 0-9a-f characters).
 - You can specify the first 7 characters of a sha for git to identify what you are referring to.
- Each commit has a big, ugly, incomprehensible _hash ID_ number such as e9e5ba39a78c8f5057262d49e261b42a8660d5b9 (often abbreviated, e.g., e9e5ba3). These _appear_ random, though in fact they're entirely non-random.
- A commit has a _full snapshot of every file_. Commits don't store _changes_, so when Git shows you changes, it's really doing a git diff of two _snapshots_.

A commit also stores some _metadata_, or information about the commit itself. This includes things like the name and email address of the author


## Create a new repository :

- **Install gh** (github command line tool) in our system.

  Like “Git” has a command line tool, “Github” also has a command line tool called “gh” .

- #### Log into our github account.

  After installing gh in our system. To log into our github account, we need to type the below command :

```
 $ Git auth login
```

  Then select Github.com >>> Select HTTPS >>> Select “Login with a web browser” >>> Copy the one-time code and press enter >>> A web page will open asking the one-time code, paste it and click submit >>> Switch to your terminal and press enter.

  below command will show you with which username you are logged in

```
 $ git auth status
```


  After logging into our github account, we need to create a directory (folder) where we can store our repository.

- #### Initialize a new local repository using git

  we need to initialize our local repository here using ‘git’:

```
  $ git init
```

  This command will create a `.git` folder inside the current directory, that contains all of the state of the git repo
  The repository we created now is a local repository (beacause it stores in our local file system). The repository we will create in github is a remote repository.
  

```
git config --global init.defaultBranch <name>
```

This will chnage the initial branch name as you wish.


```
git branch -m <name>
```

This will change current branch name.


- #### Create a new remote repository in github using gh

  enter the below command to create a new remote repository:

```
$ gh repo create
```

  Give a meaningful repository name (let’s say ‘test\_repo’ ) and press enter >>> Give a meaningful description to repository (or leave it blank) and press enter >>> Select visibility and press enter >>> prompt says that the location to the new remote repository will be labelled as “origin”, press ‘Y’ and enter >>> Your new repository named on github is created >>> prompt asks whether do you want to connect to the repository or not, you can choose ‘no’ >>>

- #### Push our first commit

  We will commit the changes to the local repository , then will push it to the remore repository but First, we will check whether our remote repository is stored under the label ‘origin’ or not:

```
$ git remote -v
```

  If the output is like this : 

      origin https://github.com/<<GITHUB\_USERNAME>>/test\_repo.git (fetch)

      origin https://github.com/<<GITHUB\_USERNAME>>/test\_repo.git (push)

  Then we will push the changes to the remote repository , otherwise we have to add the remote repository link to the label ‘origin’ (‘origin’ is just a standard label, we can name it anything meaningful) :

      git remote add origin https://github.com/username/repo_name.git

  Now, we can push our commit to the master branch of remote repository which is labelled under ‘origin’:

      git push -u origin master

  #### for pushing to another branch:

      git push origin branch_name

  #### for merging one branch with the master branch : 

  run the following command in the main branch:

      #switch to the main branch
      git checkout main  

      #merge changes from new branch to the main branch
      git merge branch_name  

  ![](Repo.png)

  adding a file named Readme to our local repository, a file with the header My Project
      echo  “# My project “ Readme.md


#### Force push

Force push (`git push --force`) is used to overwrite the remote branch with your local branch when you've rewritten history locally (e.g., after amend, rebase, or reset). It replaces the remote commits with your new ones, which is useful for cleaning up commit history on a feature branch before merging. However, because it discards the remote history, it's important to use it carefully—prefer `git push --force-with-lease` for safety, as it ensures you don't accidentally overwrite someone else's work on the branch.

### git init :

To create a new repo, you'll use the **git init** command. git init is a one-time command you use during the initial setup of a new repo. Executing this command will **create a new .git subdirectory** in **your current working directory**. This will **also create a new main branch**.

### Bare vs. cloned repositories :

If you used git clone set up your local repository, your repository is already configured for remote collaboration. git clone will automatically configure your repo with a remote pointed to the Git URL you cloned it from. This means that once you make changes to a file and commit them, you can git push those changes to the remote repository.

If you used git init to make a fresh repo, you'll have no remote repo to push changes to. A common pattern when initializing a new repo is to go to a hosted Git service like Bitbucket and create a repo there. The service will provide a Git URL that you can then add to your local Git repository and git push to the hosted repo. 

Now we want to add this new file to the repository :

`git clone`* “ path of the remote repo on your local machine ” or “path of the remote repo on github”
echo “#My project” Readme.md

#add 
add the file to the ***staging area***
`git add Readme.md or git add` .

#commit 
commit the changes on the local repository
`git commit -m  “initialized my project with a readme”`  

#push 
push the changes on the remote repo on the master branch   (with this command the working directory will know that all the changes will go to this remote repo to the master branch , actually it is connecting the local repo to the remote repo master branch)

`git push` ---> this will push changes to the remote branch master
git status

#log 
show you the last commit that is done and the status of local and remote repo
`git log | head`

#branch 
A branch _POINTS_ to a commit, it is not a set of changes.

Create a new branch :
`git branch branch_name`

Switch to a newly created branch :
`git switch <branch name>` 
OR
`git checkout <branch name>`

Create and switch to a new branch in one commit :
`git checkout -b <branchname>`

Track a branch :
after creating a branch locally (this approach) you should push the branch to the remote using:
`git push origin branch_name`

but Its often convenient to setup local branch to track remote branch because we can use `push` and `pull` without specifying the target branch

`git branch --set-upstream-to=origin/remote_branch_name local_branch_name`
`git branch --set-upstream-to=origin/trunk trunk`

Delete a branch :
`git branch -d branch_name`

Force delete a branch :
`git branch -D branch_name`

Switch to a branch :
`git checkout branch_name  or git switch branch_name`

#Fetch 
fetch new data from a remote repository
`git fetch`                (it fetches all remotes) 
`git fetch origin`         (this fetch only remote branch origin)

#Pull
Update your current local working branch with all new commits from the corresponding remote branch, you just want the changes merged for you into your branch
`git pull <remote> <branch>`
`git pull origin master`
`git remote add origin [url]`

grabs online updates and merges them with your local work
`git pull REMOTE-NAME BRANCH-NAME ----> git pull origin test`

Anytime you see a branch that is `<remote>/<name>` it means that it is the last known state of the `<remote>` repo's `<name>` (branch).

#RebasePull
When you add the `--rebase` flag to pull, instead of merging the remote changes, Git **rebases** your local commits on top of the remote changes.
`git pull --rebase 

**Rebase** rewrites the commit history to create a cleaner, linear history. Your local commits will be reapplied as if they were made after the changes from the remote branch, avoiding merge commits.

Example :
- Git fetches the remote changes (`A -> B`).
- It temporarily sets aside your local commits (`C -> D`).
- It applies the remote changes to your branch first (`A -> B`).
- Then, Git reapplies your local commits on top of the remote changes (`A -> B -> C -> D`)


**Note** :If there are **conflicts** during the rebase, Git will stop and prompt you to resolve them before continuing. After resolving, you can use `git rebase --continue` to proceed with the rebase.


#Merge
A merge is attempting to combine two histories together that have diverged at some point in the past. There is a common commit point between the two, this is referred to as the best common ancestor ("merge base" is often the term used in the docs).

combines your local changes with changes made by others (can be made on different branches)
you'd merge a remote-tracking branch (i.e., a branch fetched from a remote repository) with your local branch
you should switch to the branch you want to apply merging on and then use following command using the local branch_name you want to merge and then push the merged branch to the remote repository

`git checkout dev`
`git merge REMOTE-NAME/BRANCH-NAME`    ----> `git merge origin/perf`
`git push origin dev`

OR
**Merge branch rewrite on the branch dev**
`git checkout dev`
`git merge rewrite`

Then Git will use your system's default editor for you to accept/make any changes to commit messages.

show a merge commit 
`git log --oneline --decorate --graph --parents 
* `ccf9a73 a665b08 16984cb (HEAD -> trunk-merge-foo) Merge branch 'foo' into trunk-merge-foo`
	- This shows the last commit that is "ccf9a73" and it is a merge commit as you see the commit message 
	- The branch name is "trunk-merge-foo"
	- This merge commit has two parents "a665b08" and "16984cb"
	- This commit merged the two commits  "a665b08" and "16984cb" together by finding its best common ancestor

#stash
You have made a change... but you need to pull in changes from a remote repo without commiting your half baked changes first

`git stash` will take every change _tracked_ by git (by `git add`)(change to index + change to work tree) and store that result, much like a commit, into the "stash."\
The command saves your local modifications (unstaged/uncommitedchanges) away and reverts the working directory to match the HEAD commit.
Stash is a STACK of temporary changes

You can push your changes into the stack by using :
`git stash`
`git stash -m "my lovely message here"`

Stashes can be listed out :
`git stash list`
`git stash show [--index <index>]`

To pop the latest stash :
`git stash pop`
`git stash pop --index <index>`

#### git switch vs git checkout : 
`git checkout`  commnad is splited into two seperate commnads (git restore, git switch) in the recent updates


`git fetch` downloads new data from a remote repository - but it doesn't integrate any of this new data into your working files. Fetch is great for getting a fresh view on all the things that happened in a remote repositor

`git pull` , in contrast, is used with a different goal in mind: to update your current HEAD branch with the latest changes from the remote server. This means that pull not only downloads new data; it also directly **integrates** it into your current working copy files.

`gitignore` : .gitignore tells git which files (or patterns) it should ignore. It's usually used to avoid committing transient files from your working directory that aren't useful to other collaborators, such as compilation products, temporary files IDEs create, etc, it is at the git directory of the repository


Note: local branch(**Head -> master**) is on the same level as **remote branch** (**origin/master**)


Note: bear in mind that add and commit are both still happening on the local repository , and the changes will be made to the remote repository first when you push changes

Note: Because pull performs a merge on the retrieved changes, you should ensure that your local work is committed before running the pull command. If you run into [a merge conflict] you cannot resolve, or if you decide to quit the merge, you can use git merge --abort to take the branch back to where it was in before you pulled.

#### To store a new change :

    git add 
    git commit -m "commit message"
    git push origin

Note: bear in mind that you **should never ever work in the master branch**, because master branch is a holy gray that should always be a working version of the project , therefore you have to always create a new branch and work on that branch and then if everything goes well you could merge your branch with the master branch

Note: if you commit to a remote branch that someone else has already made changes you will get a merge conflict (you should alwys pull chnages and then commit your new changes), but if you encounter this issue just do the following:

    git config pull.rebase false
    git pull
    git commit -m "this commit message whould be something like: Merge branch 'main'"
    git push

### commit messages:

the structure of a git commit message should be like this:

    <type><scope(optional)><description>

#### Different Types of commits :

- **Build** : The build type (formerly known as chore) is used to identify development changes related to the build system (involving scripts, configurations or tools) and package dependencies.

- **docs**: The docs type is used to identify documentation changes related to the project -	

- **Style**: The style type is used to identify development changes related to styling the codebase, regardless of the meaning - such as indentations, semi-colons, quotes, trailing commas and so on.

- **feat** : The feat type is used to identify production changes related to new backward-compatible abilities or functionality.

- **Fix**: The fix type is used to identify production changes related to backward-compatible bug fixes.

Refactor : The refactor type is used to identify development changes related to modifying the codebase, which neither adds a feature nor fixes a bug - such as removing redundant code, simplifying the code, renaming variables, etc.

Test : The test type is used to identify development changes related to tests - such as refactoring existing tests or adding new tests.


` `**access GitHub account using SSH-keys :**

We have to repeat below four steps, for every github account we want to access through SSH Public Key authentication. you have to upload your public key on github

### Different types of merge

![](1_merge.png)
##### - Merge
A standard merge will take each commit in the branch being merged and add them to the history of the base branch based on the timestamp of when they were created.

It will also create a merge commit, a special type of “empty” commit that indicates when the merge occurred

![](2_merge.png)

 

#### - Fast Forward Merge

If we change our example so **no new commits** were made to the base branch since our branch was created, Git can do something called a “Fast Forward Merge”. This is the same as a Merge but **does not** create a merge commit.

This is as if you made the commits directly on the base branch. The idea is because no changes were made to the base branch there’s no need to capture a branch had occurred.

![](3_merge.png)

##### - Squash and merge

Squash takes all the commits in the branch (A,B,C) and melds them into 1 commit. That commit is then added to the history, but none of the commits that made up the branch are preserved

![](4_merge.png)

##### - Rebase and merge

A rebase and merge will take where the branch was created and move that point to the last commit into the base branch, then reapply the commits on top of those changes.

This is like a fast forward merge, but works when changes have been made into the base branch in the mean while.

When using rebase you can have a clean history with no merge commits.

Rebase will make the history linear.

`git rebase <targetbranch>`

![](5_merge.png)


## Merge Conflicts 

Merge conflicts occur when competing changes are made to the same line of a file, or when one person edits a file and another person deletes the same file

To resolve a merge conflict caused by competing line changes, you must choose which changes to incorporate from the different branches in a new commit.

1. To see the beginning of the merge conflict in your file, search the file for the conflict marker `<<<<<<<`. When you open the file in your text editor, you'll see the changes from the HEAD or base branch after the line `<<<<<<< HEAD`. Next, you'll see `=======`, which divides your changes from the changes in the other branch, followed by `>>>>>>> BRANCH-NAME or Sha of incomming conflicted change

  In this example, one person wrote "open an issue" in the base or HEAD branch and another person wrote "ask your question in IRC" in the compare branch or `branch-a`.
	
 text
If you have questions, please
<<<<<<< HEAD
open an issue
=======
ask your question in IRC.
>>>>>>> branch-a
>>>>>>> 
>>>>>>> 

2. Decide if you want to keep only your branch's changes, keep only the other branch's changes, or make a brand new change, which may incorporate changes from both branches. Delete the conflict markers `<<<<<<<`, `=======`, `>>>>>>>` and make the changes you want in the final merge. In this example, both changes are incorporated into the final merge

3. Add or stage your changes.  `git add .`
4. Commit your changes with a comment.  `git commit -m "Resolve conflicts"`
	- if you do not write a commit message **Git will create a merge commit** to finalize the merge (combining the two branches).

**Not taking upstream's changes** :
If you decide to **keep your own changes** (not take the upstream's changes), you'll resolve the conflict in favor of your code. This is fine if you know your changes are correct, but it means your local branch still differs from the remote branch because you didn't incorporate their updates.

The next time you pull or try to merge, Git will likely attempt to merge again, creating **additional merge commits** every time you pull from the upstream, as the history of your local branch and the remote branch continues to diverge.

This will keep happening until you properly **sync** your changes, either by:

- Merging their changes into your branch
- Rebasing your branch on top of the upstream changes
	- If you use `git pull --rebase`, it re-applies your changes on top of the latest remote changes, which can help avoid repeated merge commits.


## Add/replace the remote repository for an existing git project 

### what is a remote?
probably any of your local repositories (local copy) is connected to a remote repo on a server like github/gitlab 
the default remote repo is **origin**, that is actually the shortcut for the remote repo URL (https://github.com/sahelsb/some-repo)
you can add more remotes to your local repositories with different names

if you have an exisiting git project and a remote repository (franhofer Gitlab), then you want to add another remote repo for this project (your own github) you need to do the following :

first clone the rmeote repository on you local machine

### add a new remote repo

add a new remote repo for your project
`git remote add new_remote_name remote_url      /   git remote add **origin2* https://github.com/sahelsb/some-repo`

push changes to the new repo (origin2)
`git push **origin2** main`
push specific branch (say dev) of current repo to main branch of new repo (origin2)

`git push origin2 dev:main`
`git remote -v `    ----> will show you have two remote repositoiry tracking this poroject


change the name of existing remote repo (origin) to a new name (upstream)
`git remote rename origin upstream`

add the new remote repo as origin
`git remote add origin new_remote_url`

### replace the existing remote repo

set another remote repository as your origin 
`git remote set-url origin remote_url           / git remote set-url origin https://github.com/sahelsb/some-repo`

`git remote -v `     ----> will show you have only one repository (the new remote) tracfking your project



now in this way the new remote repository will bring all the git history (commits, ...) to your new remote repository but if you do not want to transfer git history 

you can create new **orphan** type branch which does not record previous history. Then push this new branch to new repo :

### Removing previous commits or tracking history of current repository

first checkout tpo the branch you want to remove history, then create a new orphan branch
`git checkout --orphan clean_branch`

commit the changes from dev branch to this orphan branch (clean_branch)
`git add . & git commit -m "added code"`

push this clean_branch to the dev branch of the remote repo
`git push origin2 clean_branch:dev`

delete clean_branch
`git branch -D clean_branch`

**so you pushed branch dev from old previous repo to the new remote repo without git history**


### Git Submodule

Git submodules allow you to keep a Git repository as a subdirectory of another Git repository. This is ideal for projects that depend on certain versions of external repositories. By using submodules, you can track the external repositories in a given commit.
Managing project dependencies can be a complex task, especially when your projects depend on external code repositories. One of the common solutions to this challenge in Git-centric workflows is using Git submodules.
### add a repo as a submodule to another repo
    
    #inside the existing repo
    git submodule add <other repo URL>

### clone a repository with its submodules together

- clone the repository with submodule at the same time

    `git clone --recurse-submodules <repo URL>`

- clone the main repo first then add the submodule

    `git clone <repoo URL>`
    Initialize, fetch and checkout any nested submodules, you can use the foolproof
    `git submodule update --init --recursive`

### check for new work in a submodule

go inside the sub directory
    `git fetch `
    `git merge origin/main`

OR 

inside the main directory
    `git submodule update --init`


Note: If you set the configuration setting status.submodulesummary, Git will also show you a short summary of changes to your submodules when you git status in the main directory

    git config status.submodulesummary 1

### pull chnages from submodule

By default, the git pull command recursively fetches submodules changes, if there is anew submodule it will create an empty folder. However, it does not update the submodules so
    
inside the main directory
    `git pull`
    `git submodule update --init --recursive`

### push to submodulke

check that all your submodules have been pushed properly before pushing the main project
    `git push --recurse-submodules=check`

##### Head detached issue wjhn pushing to submodule :
    please pay attention if you push changes to the main repo before pushing changes to the submodule then it will create a new branch in submodule(something like "JE36546") and you see "Head detached at this branch" so be sure to push to the submodule befor e pushing to the main module

### Git Reset

The `git reset` command allows you to RESET your current head to a specified commit. You can reset the state of specific files as well as an entire branch. Git `reset` is best used when you have only made local commits (i.e. not pushed up your changes to a remote branch) and you want to undo those changes.

##### Soft Reset

1. `git [--soft] reset 899679c` (Requires you to locate the commit hash from the log)
2. `git reset HEAD~2` (Tells git to drop the last two commits)

**Running either command above is considered a "soft" reset**. All this means is the code changes that were undone are now brought back to the working directory files. Or put another way, a soft reset removes the commit history but **_preserves_** the changes.

A soft reset can be helpful if, for example, you made some commits on the wrong branch, but you want to keep the work you did and move it over to a different branch. With a soft reset, the commits will be removed, but the revisions will be retained.

##### Hard Reset

In contrast to a soft reset is a "hard" reset where the changes that are undone are completely removed and the files are put back into a "clean" state. To perform a hard reset you would run a similar command to the syntax above, but you would pass in the `--hard` flag.

1. `git reset --hard 899679c`
2. `git reset --hard HEAD~2`


##### What is  `HEAD~<number>`
`HEAD~1` means one commit back from `HEAD`


### Git Revert

The `git revert`  is similar to a `git reset` . It's important to understand that `git revert` undoes a single commit—it does not "revert" back to the previous state of a project by removing all subsequent commits. This is actually called a reset, not a revert.

When a `revert` is run, git will prompt you to add a new commit with a helpful message explaining what got reverted. `revert` is the command we use when we want to take a previous `commit` and add it as a new `commit`, keeping the `log` intact.

###### automatic commit :
The command below will prompt you to create a new commit that will undo the commit with that hash and thus you would have reverted the commit. :

`git revert <commit hash>`
`git revert HEAD`
`git revert HEAD~2`

###### --no-commit :
Does not directly commit the created changes. By default, the reverting changes would be directly committed by Git. With the "--no-commit" option, the changes will only be created, but not committed. You could then edit them further and commit them manually.

`git revert <commit hash> --no-commit
`


Reverting allows you to undo commits cleanly that have already been pushed to a remote branch. A good use case for reverting is if you're working with another team member on the same feature branch and you want to undo a commit you made without compromising the git history.

- With "git revert" we can undo any commit, not like "git reset" where we could just remove "n" current commits.

if any conflicts happend then Finish the revert by fixing the conflicts and then `git add` the changes and then use
`git revert --continue`

### Git Restore
Restore staged files (from git add) to unstage
    git restore --staged pef.py 
    git add 
    git commit

### Git log
	git log | head
    git log --graph --decorate
	 git log --oneline --graph   # shows each commit summarized in one line
	 `git log -3`   # will only show 3 last commits
	 

##### grep : 
`git log` comes with a `--grep` option --->        
`git log --grep "<term>"`
This will search through the commits and look in the commit message for `<term>`.


`-p` will show the commits diff as well
`git log -p -- file1 file2...`



when you call git log you can see a **HEAD** within the log
### What are heads and refs?

In Git, a **ref** is a human readable name that references a Git commit ID. A ref is essentially a pointer to a commit. Examples of refs are Git branch names such as `master` and `dev`. Another example of refs are Git tags such as `v0.1` or `v0.2`. You can think of each of these as a variable name that points to a commit ID. The commit ID that a ref points to is dynamic so it can change over time.

When representing a branch name, a ref such as `master` represents the tip (most recent commit ID) on that branch. Refs are stored in a special hidden location in your Git repository at the path `.git/refs/`.

In Git, a **head** is a ref that points to the tip (latest commit) of a branch. You can view your repository’s heads in the path `.git/refs/heads/`. In this path you will find one file for each branch, and the content in each file will be the commit ID of the tip (most recent commit) of that branch.

##### What is HEAD?

HEAD is a special ref that points to the commit you are currently working on - the currently checked out commit in your Git working directory. You can think of it as a global variable or environment variable within your Git repo that can change depending on which commit you've checked out in your working directory. It is stored in a file called `.git/HEAD`
HEAD usually points to the tip/head of the currently active branch, When you use the `git checkout` command, HEAD is changed to point to the head of the newly checked out branch.

In lowercase, "head" is a general term that means any commit that represents a branch tip. In uppercase, "HEAD" is a specific Git ref that always points to the commit currently checked out in the working directory.

###### Detached HEAD
The `git checkout` command can be used to checkout a specific commit into the working directory using its commit ID.  `git checkout <commit ID>` This places Git into a detached HEAD state, which means that HEAD is not currently pointing to a branch head (branch tip). In this state, you can view and edit any files in your working directory, exactly as they were in that commit.
The catch is that if you make changes and then just switch back to a normal branch, you'll lose any changes and commits you made in the detached HEAD state. If you want to keep any changes or Git commits you may have made starting from the detached HEAD, you can simply create a new branch. This will store your changes in the `tmp` branch and set HEAD to the tip of that new branch

###### When should I use Git HEAD
The ability to return to a previous commit is immensely useful during development. For example, if a commit introduces a breaking change to a file, you can use `git log -p <file>` to view all of the commits that have affected that file. In this interface, you can use the arrow keys to scroll up/down and press Q to exit.

Once you find the commit in question, you can revert the full branch state to it using `git checkout <commit ID>`. This detaches HEAD back to that commit so that you can view that file's old version in context (e.g. to run and test your application). Alternatively, if you only want to revert that specific file, you can run `git checkout <commit ID> <file>` to restore it.

The git show command is a quick way to peek at a commit, including the commit ID, commit message, and a textual diff representation of the changes in that commit. The syntax is `git show <commit-id>`.


### Diff the last commit
    git diff head ^ head

### Pull newly created branch on remote
this command will update all local branches which tranch remote branches but will not create local branches to track remote branches
    `git pull -a`
    
this command will create local branch to track remote branch\
    `git checkout -b local_branch_name origin/remote_branch_name`
    or 
    `git switch -c local_branch_name origin/remote_branch_name`


#### permission denied (Publickey error)
to solve this error I just added ta configuration for my github account to the config file in .ssh as below : 
     ```
```
      Host gitlab-extern.ivi.fraunhofer.de
      User git
      IdentityFile ~/.ssh/verum_orin
```

#### Stashed local changes 
    git stash

#### Unstashed local changes
    git stash pop

#### Remove all local changes (tracked files)
    git clean -f


### Git tags

At some point there are changes in which represents a version of your sofware you want named.
The best way to think about a tag is a branch that cannot be changed. It can only be deleted

```
git tag <name>   # to create 
git tag -d <name>   # delete 
git tag    # to list 
git checkout <tagname>    # to checkout a tag
```
 
 You can push tags to a remote via `git push --tags` and pull via `git pull --tags`


## CI/CD

1. Continuous Integration (CI): Continuous integration (CI) is a software development practice that automates the process of integrating code changes from multiple developers into a central repository. In MLOps, continuous integration (CI) focuses on automating the building, testing, and packaging of machine learning pipelines whenever there are changes to the codebase in the version control system (like Git).

2. Continuous Delivery: Continuous delivery usually means a developer’s changes to an application are automatically bug tested and uploaded to a repository (like GitHub or a container registry), where they can then be deployed to a live production environment by the operations team. In this type, approval is required before GitHub delivers the changes that you have made in the codes to the production.

3. Continuous Deployment: Continuous deployment is a strategy in software development where code changes to an application are released automatically into the production environment. Here, GitHub directly deploys the changes you have made in the codes to the production. In software development, a production environment refers to the final version of the application that’s used by real end-users. In practice, continuous deployment means that a developer’s change to a cloud application could go live within minutes of writing it (assuming it passes automated testing). This makes it much easier to continuously receive and incorporate user feedback

### Github actions

GitHub Actions is based on the concept of workflows, which are automated tasks that are triggered by specific events or scheduled at regular intervals. These events can include code pushes, pull requests, creating issues, and more. When one of these events occurs, GitHub Actions automatically executes an associated workflow that performs a series of predefined steps.

1. Create a .github directory in your repository.
2. Within the .github directory, create a new directory called workflows.
3. In the workflows directory, create a new file named build-test-deploy.yml.
   
When you create a CI pipeline, you first need to give the workflow a name and then set the event that should trigger the workflow. 

```
name: Build, Test, and Deploy

on:
push:
branches:
   - main
paths-ignore: 
   -'README.md'
pull_request:
branches: 
   - main

# Schedule the workflow to run every Monday at 8 a.m. (UTC time)
schedule:
- cron: "0 8 * * 1"

jobs:
integration:             # first job name
name: Continuous Integration
runs-on: ubuntu-latest
steps:
  - name: Checkout Code    # checks out the repository code into 
							 runners workspace
  uses: actions/checkout@v3

  - name: Set up Python    # setup python environment
  uses: actions/setup-python@v4
  with:
	  python-version: 3.11

  - name: Install Dependencies
	run: |
	  python -m pip install --upgrade pip
	  pip install -r requirements.txt
  
  - name: Run Tests
	run: |
	  python -m unittest discover
````
#### Github runner 
In GitHub Actions, a “runner” is essentially a virtual machine or container instance that executes your workflows. When you create a workflow in GitHub Actions, it consists of one or more jobs, and these jobs run on a runner. Runners can be hosted by GitHub (GitHub-hosted runners) or by yourself (self-hosted runners).

#### Remove a file from remote but keep in local folder:
```bash
     git rm -r --cached filename
	 git commit
	 git push
```


   
## Git Large File Storage

An open source Git extension for versioning large files

Git Large File Storage (LFS) replaces large files such as audio samples, videos, datasets, and graphics with text pointers inside Git, while storing the file contents on a remote server like GitHub.com or GitHub Enterprise.

#### Installing Git Large File Storage

In order to use Git LFS, you'll need to download and install a new program that's separate from Git.

Follow the below install it :
[git-lfs/INSTALLING.md at main · git-lfs/git-lfs · GitHub](https://github.com/git-lfs/git-lfs/blob/main/INSTALLING.md)

```bash
sudo apt-get install git-lfs
```

Then you can activate it in your repo :

1. set up Git LFS for your user account by running:

```bash
git lfs install
```

You only need to run this once per user account.

2. In each Git repository where you want to use Git LFS, select the file types you'd like Git LFS to manage (or directly edit your .gitattributes). You can configure additional file extensions at anytime.

```bash
git lfs track "*.jpg"
```

Now make sure .gitattributes is tracked:

```bash
git add .gitattributes
```

Note that defining the file types Git LFS should track will not, by itself, convert any pre-existing files to Git LFS, such as files on other branches or in your prior commit history. To do that, use the [git lfs migrate(1)](https://github.com/git-lfs/git-lfs/blob/main/docs/man/git-lfs-migrate.adoc?utm_source=gitlfs_site&utm_medium=doc_man_migrate_link&utm_campaign=gitlfs) command, which has a range of options designed to suit various potential use cases.

3. There is no step three. Just commit and push as you normally would; for instance, if your current branch is named `main`:

```bash
git add file.jpg
git commit -m "Add design file"
git push origin main
```



# Rebase

**Rebase** is a way to _move_ the base of your commits onto a new starting point.

It “replays” your commits on top of another branch’s tip.

Instead of _merging_ histories (which can create merge commits), it _re-writes_ your commits so it’s like you developed them starting from the latest version of the branch.

```bash
A -- B -- C         (dev)
      \
       D -- E       (feature)

```

You started `feature` from B, but `dev` advanced to C
If you do:

```bash
git checkout feature
git rebase dev
```

Git will:
Take D and E  
Replay them on top of C

```bash
A -- B -- C -- D' -- E'  (feature)

```

**Key idea:**
- Commits D and E get _new SHAs_ (D', E') because they are rebased onto C.
- Clean, linear history.


### How 

**Rebasing** is a way to move your feature branch commits on top of the latest base branch (like `dev`) to maintain a clean, linear history without merge commits. The typical workflow is to first update your `dev` branch to the latest remote state, then rebase your feature branch (e.g., `refactor`) on top of it, force-push the rebased changes to the remote (because rebase rewrites history), and finally fast-forward merge the feature branch into `dev` to avoid merge commits.

### git rebase

```bash
# 1. Update dev branch to match remote
git checkout dev
git fetch origin
### only if need to align local branch and remote dev 
### forcefully ignore local commits
git reset --hard origin/dev

# 2. Switch to feature branch and rebase it onto latest dev
git checkout refactor
git rebase dev

# (Resolve conflicts if needed, then continue)
git rebase --continue  # only if there were conflicts

# 3. Force push the rebased feature branch
git push --force_with_lease

# 4. Merge back into dev without a merge commit
git checkout dev
git merge --ff-only refactor

# 5. Push updated dev
git push

```

### git pull --rebase

```bash
git checkout dev
git pull --rebase

```

It pulls new commits from _remote dev_.  
Then rebases your _local unpushed commits_ on top of the updated remote.
This avoids `Merge branch 'origin/dev'`


---

## Rebase Summary
 
`git rebase origin/dev`
 
- Takes your current branch commits
- Temporarily removes them
- Applies the latest `origin/dev` commits first
- Replays your commits on top of it
- Creates a **clean, linear history**

Result: your feature branch looks like it was built from the latest `dev` from the start.


Use rebase when:

- `dev` has new changes you need
- Before opening a Pull Request
- Before merging feature → dev
- You want to sync your feature branch with latest `dev`


Why use rebase

- Keeps history clean (no messy merge commits)
- Makes PRs easier to review
- Reduces future merge conflicts
- Keeps feature branch up to date with `dev`


---

### What is GitLab CI/CD?

GitLab CI/CD is GitLab’s built-in system for automating tasks in your repository, such as building, testing, and deploying your code. You define instructions for the automation in a file called `.gitlab-ci.yml`, which lives in your repository. Every time you push code or create a merge request, GitLab runs these instructions on its CI runners. This ensures your code is consistently built and tested automatically, and allows you to deploy updates without manual steps.


### What is GitLab Pages?

GitLab Pages is a feature that lets you publish static websites directly from your GitLab repository. It’s useful for hosting project documentation, blogs, portfolios, or any other static site. GitLab Pages takes a folder of generated static HTML, CSS, and JavaScript files and serves them at a public (or private) URL. Typically, your repository contains source files (like Markdown for documentation) and a build process to turn them into a complete website.

### How do GitLab CI and GitLab Pages work together?

To deploy a site to GitLab Pages automatically, you use GitLab CI to _build_ the static site and _upload_ it to GitLab Pages. In your `.gitlab-ci.yml`, you define a special CI job named `pages` that creates the static site and places the final files in a folder named `public`. GitLab CI/CD runs this job whenever you push to the specified branch (for example, `dev`), builds the website, and makes the contents of `public` available at your GitLab Pages URL. This workflow ensures your website is always up to date with your branch.

### What is happening in this specific `.gitlab-ci.yml`?

```bash
image: python:3.11
pages:
  stage: deploy
  script:
    - pip install mkdocs
    - mkdocs build
    - mv site public
  artifacts:
    paths:
      - public
  only:
    - dev   # or "master" or your default branch name
```

Your pipeline definition uses the `python:3.11` Docker image so that it can run Python commands. The `pages` job is part of the `deploy` stage and runs a script that installs MkDocs (a static site generator for documentation), builds the documentation site from Markdown into static HTML in the `site` directory, and then renames `site` to `public`, which is the required output folder for GitLab Pages. The `artifacts` section specifies that `public` should be saved and used as the deployable website content. Finally, the `only: - dev` condition ensures this deployment happens only when you push to the `dev` branch, preventing unnecessary builds from other branches.

### How do you use this in practice?

You maintain your documentation source files (for example, Markdown files and `mkdocs.yml`) in your repository’s `dev` branch. Whenever you commit and push changes to `dev`, GitLab CI automatically runs the pipeline, builds the static site, and deploys it to GitLab Pages. As a result, your documentation website always reflects the latest content in `dev`, without any manual building or uploading. This is especially useful for teams, as everyone can contribute to the documentation, and the site updates automatically whenever changes are merged.

---

### Checkout the commit before a specific commit (read-only state)

If you know the commit hash (e.g. `abc1234`):

```bash
git checkout 'abc1234^'
```

- `^` means "the parent of this commit" (i.e. the state **before** this commit).
- You’ll enter a **detached HEAD** state — meaning you’re not on any branch.
- You can still run your code as it was back then.

If you want to go back to your current branch afterward:

```bash
git checkout main  # or your branch name
```

---

### show a specific stash without applying it

```bash
git stash list   # get the stash hash from this 
git stash show -p stash@{1}
```

`-p` (or `--patch`) shows the **full diff** of what's in the stash


### drop a specific stash

```bash
git stash drop stash@{1}
```

---

### revert a specific commit

```bash
git revert abc1234   ## should provide the commit hash of the bad commit
```

Git will then **create a new commit** that undoes all the changes from that commit.

---

### Squash

In this process, you will grab all the commits with the `git rebase` command with the `i` flag and put them together with `squash`.

```bash
git rebase -i HEAD~3
```

This will open up your editor of choice for Git.

Now, you need to replace all those `pick` with `squash` (or simply `s`) apart from the first one.

`pick` or `p` will only use those commits, but `squash` or `s` will use them and combine them all together.

The first commit is the one you will combine them into without losing your changes.

After doing that, save the file and close it. Git will open up another editor where you can see the new commit message and change it if you want and save the file.

```bash
git push
```
Then push and you see only one commit message instead of the last three.

---


##### Gitlab Default/protected branch

GitLab sets the first branch you push as the default branch, and the default branch is protected automatically

keep working on dev, create main later 
Just keep committing to dev. When your code is solid, create main from dev and make it the default:

```
git checkout -b main
git push -u origin main
Then in GitLab: Settings → Repository → Branch defaults → set default to main.
```


