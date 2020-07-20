# Documenting Git Workflow and Git commands


# What is Git

Quoting [wikipedia](https://en.wikipedia.org/wiki/Git) verbatim , it is a "distributed version control system (dvcs)" for tracking
changes in source during software development

[The book](https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control) provides a nice description on local version control,
centralized version control and finally distributed version control systems    

SVN, CVS, Subversion, Perforce are centralized version control systems where a single centralized repository serves as a communication hub between developers, 
and collaboration happens by passing changesheets between the developers local repo and the centralized repo   
The downside of this is that if the centralized repo is down for some reason, or corrupted, chaos happens  

Examples of distrubuted version control systems are git, mercurial, bazaar, darcs  
In this, clients don't store just the latest snapshot of files, but mirror the entire history of the repo (every clone is a full backup of all the data). 
Thus , if if any server dies, the entire history stays on every other client repo.  
Another advantage is that working with several remote repos at the same time with the same project is possible  
A third advantage is that it is blazingly fast as it does not need to communicate with the centralized server much 

Compared to other centralized or distributed version control systems like CVS, subversion, bazaar, etc, while these other VCS store files, and changes made to each file
over tim (delta-based); git thinks of data as a series of snapshots of a file system (a stream of snapshots). Every time a commit
is done, a snapshot of all files are taken and a reference to the snapshot is stored (of course, for efficiency, if some files are not
changed from the previous commit, just a link to the previous file is stored) [2](2)  




# How does Git work

## The 3(+1) states

First, the final (+1) state is not really git, it is the remote/cloud state offered by github where the files in state 3 are pushed to the cloud

A corollary of this is that the 3 states are all local

Here are the 3 states (you can think of them as ordered, where files are created in state 1, and shifted to states 2 and 3)

1. The working directory (where new files are created and existing files modified)

2. The staging or index area , where files from stage 1 which you want to commit are added to

3. The actual (local) git repo, where a snapshot of all files created in the staging area are stored

The commited changes can now be pushed to the (+1) state on the cloud, which can be shared with other people






# Understanding git workflow

We would like to move files which are newly created or modified from state 1 (working directory) -> state 2(stage) -> state 3 (local git repo) to finally push (state 4)

Below, listing all commands to move from any state to any other state

- state 1 -> state 2
    git add "filename" to move a single file from state 1 to state 2

- state 2 -> state 3
    git commit (with some options). All files in state 2 (staged) move to state 3

- state 3 -> state 1  ("undoing local changes and fetching change from last commit ")
    git checkout --"file name"  discards local changes

- state 2 -> state 1 ("unstaging a file")
    git reset HEAD "file name". This unstages a previously staged file

# Changing commits  

If you want to change previous commits, here are some options  

- git commit --amend 
   This is used if you want to make changes to the immediately previous commit. There are two scenarios in 
   which this is useful    
   1) Want to modify the message of the immediately previous commit  
     git commit --amend -m "updated message"   
   2) Have some files in the staging environment (or which you can add to the staging environment) which you want as a part of the same commit  
     once files are staged, 
     git commit --amend --no-edit  
   Note that amend does not really modify the immediately previous commit, but rather replaces it entirely  
   Therefore, avoid ammending commits which other folks have started working on    
   
   

   
- git rebase
   This is used to change older commits or multiple commits in one shot. Again, since  new commits replace the old,
   do not do this on pushed commits  
   
    
   

# to untrack a file/directory
  git rm read.md - deletes the file read.md from working directory , and unstages it 
  git rm --cached read.md - unstages read.md, does not delete from working directory 
  to untrack a file directory instead of a file, do git rm --cached -r dirname
  

# Git Diff

To view differences between any 2 of working directory, staged and commited states

- git diff (no parameters)
    Print out differences between working directory and the stage

- git diff --cached or git diff --staged:
    Print out differences between the stage and current commit (HEAD)

- git diff HEAD:
    Print out differences between working directory and current commit (HEAD)

- git diff --name-only
    Show only names of changed files.

- git diff --name-status
    Show only names and status of changed files.



# Logging commands

Listing logging commands  

All the following commands work on the branch which has been checked out.   
We can also specify branch name explicitly by adding branchname after log



- List all commit logs in reverse chronological order
    git log for current checked out branch or git log branchname for any branch

- List most recent k commits in reverse chronological order
    git log -k

- List most recent commits since a certain time point/until a certain time point
    git log --since=2.weeks  
    git log --since="2019-07-01"
    git log --until="2019-07-01"


- List all commits against whose message  a certain word is grepped  
    git log --grep text finds all commits which contains the word text  

- List all commits which modified a particular directory/file !
    git log -S filename



- Display differences displayed in each commit
    git log  -p or git log --patch

- Display summary statistics of each commit (more verbose than just git log)
    git log --stat

- Pretty display :)
    git log --pretty  
    git log --pretty=oneline (displays each commit in one line)  
    got log --pretty==format:"[options](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History#pretty_format)"
    For example
    git log --pretty=format:"%h - %an, %ar : %s" prints abbreviated commit hash, author name, relative author date and subject


- Viewing commit history graphically
    git log --branch shows all commits on different branches in a graphical format   
    This can be combined with pretty obviously  like so  
    git log --pretty=format:"%h %s" --graph





# Working with remotes  

As mentioned earlier in the page, remote is the cloud state which allows collaboration between different users

- Cloning a remote repo (for first time)
    git clone https://github.com/..  

- git remote  
    Displays the shortname which git gives to the remote server (by default origin)  
    git remote -v  Displays URL of remote repo  
    git remote add <shortname> <url>  to add a new remote repo (shortname and URL)  
    git remote show <shortname> Eg : git remote show origin  - verbose information on URL of remote repo, all remote branches,
    local branches which track remote branches, etc  
    git remote set-url <shortname> <url>  - change the URL of remote repo  (local branch made to track a different remote   )

- renaming remotes
    git remote rename peter paul  changes name of remote from peter to paul  (this also changes remote branch names too,
    for example a branch cleaned will be called paul/cleaned instead of peter/cleaned)  

- deleting reference to  remote
   git remote remove paul



- Downloading new changes from remote  
    git fetch  <remoteshortname>
    Downloads (new) data from remote to local. Does not merge, just fetches, so does not harm your current work

- Downloading new changes from remote and merging with local
    git pull <remoteshortname> <localbranchname>  
    Eg : git pull origin master  
    just git pull assumes remote name is current name and branch is current checkedout branch  
    git pull is equivalent to git fetch + git merge

- Pushing changes to remote  
    git push <remoteshortname> <localbranchname>  
    or just git push assumes remote name is current remote name and branch is current checkout branch


# Config  

There are 3 levels of git config, stored in 3 seperate files
    1) stored in /etc/gitconfig - contains values applied to every user in system and all repos 
    adding a --system to git config commands reads and writes from this file specifically  
    2) stored in ~/.gitconfig - contains values specific to you. add a --global to git config commands for this  
    3) stored in .git/config of whichever repo you are currently in - values specific to current repo. use --local with git config, or nothing at
    all as this is default   
    each level overwrites values in previous level   
    
    git config --list --show-origin shows all git parameters and which of the 3 files they are coming from  

- get which remote repo the current repo was cloned from
    git config --get remote.origin.url

-  get and set user name
    git config --get user.name
    git config --user.name "name"
    


-  Check user.email
    git config --get user.email
    git config --user.email "mail"

-  Change user name or email only for current git repo  
    In repo of interest, type  
    git config user.email "abc@gmail.com"[3](3)



# Managing multiple github/gitlab accounts from same machine  

Issue - If you have multiple git hub accounts, when you clone/init/push ; how would you associate to right account ?    

[A good link](https://code.tutsplus.com/tutorials/quick-tip-how-to-work-with-github-and-multiple-accounts--net-22574)  


# Tagging

Used to tag commits with version numbers, tags behave like branches (you can check them out like branches); but don't delete them  
There are two kinds of tags i) annotated (use with a -a option, has more detailed tagging information); and ii) lightweight (use without a -a option, less information than annotated))


Command for tagging a commit version no  
    - git tag -a v1 f855792 -m "First release of code"    (tags commit ID f855792 with tag v1 )  
    
Command for listing all existing tags
    - git tag  
    
Command for listing all existing tags filtered by tag name (like grep)  
    - git tag -l "v1*"  
    
View messages along with tag names (default git tag does not show messages)  
    - git tag -n  (view all tags with tag messages)
    - git tag -n3  view latest 3 tags with tag messages)  
    
Show details of a particular version -   
    - git show v1 (display contents of v1)
    
Deleting tags
    - git tag -d v1 (deletes tag with tag identifier v1)
    
Pushing tags
    Tags are not pushed with rest of code when you do git push  
    You have to specifically do  
    git push origin v1.0
    

    

    

[A good link](https://blog.daftcode.pl/how-to-become-a-master-of-git-tags-b70fbd9609d9)



















# References

1. [A good visual reference on git workflow and commands](http://marklodato.github.io/visual-git-guide/index-en.html)

2. [(Official book on git)](https://git-scm.com/book/en/v2)




[2] : https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3Fs

[3] : https://help.github.com/en/articles/setting-your-commit-email-address
