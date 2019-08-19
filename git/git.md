# Documenting Git Workflow and Git commands


# What is Git

Quoting [wikipedia](https://en.wikipedia.org/wiki/Git) verbatim , it is a "distributed version control system (dvcs)" for tracking
changes in source during software development

[The book](https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control) provides a nice description on local version control,
centralized version control and finally distributed version control systems  

Compared to other version control systems like CVS, subversion, etc, while these other VCS store files, and changes made to each file
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

- Check which remote repo the current repo was cloned from
    git config --get remote.origin.url

-  Check user name
    git config --get user.name

-  Check user.email
    git config --get user.email

-  Change user name or email only for current git repo  
    In repo of interest, type  
    git config user.email "abc@gmail.com"[3](3)



# Managing multiple github/gitlab accounts from same machine  

Issue - If you have multiple git hub accounts, when you clone/init/push ; how would you associate to right account ?    

[A good link](https://code.tutsplus.com/tutorials/quick-tip-how-to-work-with-github-and-multiple-accounts--net-22574)  



















# References

1. [A good visual reference on git workflow and commands](http://marklodato.github.io/visual-git-guide/index-en.html)

2. [(Official book on git)](https://git-scm.com/book/en/v2)




[2] : https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3Fs

[3] : https://help.github.com/en/articles/setting-your-commit-email-address
