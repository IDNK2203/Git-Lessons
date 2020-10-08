
# Git Branching

Branching means you diverge from the main line of development and continue to do work without
messing with that main line.

## Staging and Commiting (behind the sinces)

let’s assume that you have a directory containing three files, and you stage them
all and commit. Staging the files computes a checksum for each one (the SHA-1 hash )stores that version of
the file in the Git repository (Git refers to them as blobs), and adds that checksum to the staging area.

When you create the commit by running git commit, Git checksums each subdirectory (in this case,
just the root project directory) and stores them as a tree object in the Git repository. Git then creates
a commit object that has the metadata and a pointer to the root project tree so it can re-create that
snapshot when needed.

Your Git repository now contains five objects: three blobs (each representing the contents of one of
the three files), one tree that lists the contents of the directory and specifies which file names are
stored as which blobs, and one commit with the pointer to that root tree and all the commit
metadata.

If you make some changes and commit again, the next commit stores a pointer to the commit that
came immediately before it.

conclusion , Commits object is made up of two principle things a pionter its predecessor commit and
a snapshot of the files that commit was created from .

A branch in Git is simply a lightweight movable pointer to one of these commits.

## Creating a New Branch

we use the command `git  branch [branch_name]` to create a new branch . This only creates a new branch and doesn't
switched to it .

A HEAD is a special pionter that tells you what branch your on .

The `git log` command with the -- decorate  option shows you where the branch pointers are pointing.
This option is called --decorate .it will only show commit history below the branch you’ve
checked out.

## Switching Branches  

To switch  to an existing branch you the git checkout [branch_name] .

The moves the HEAD to the current branch you switched to .

To show commit history for the desired branch you have to explicitly specify it: `git log branch_name`.
To show all of the branches, add --all to your git log command.

If you run `git log --oneline --decorate --graph --all` it will print out the history of your commits,
showing where your branch pointers are and how your history has diverged.

To create a new branch and want to switch to that new branch at the same time
— this can be done in one operation with `git checkout -b [newbranchname]` .

## Basic Branching and Merging

the `git merge [branch_name]` command is used to merge two git branches together.

### Types Of Merging

we will be looking at this two types of now.

1. *Fast forward*

    when you try to merge one commit with a commit that can be reached by following the first commit’s history,
    Git simplifies things by moving the pointer forward because there is no divergent work to merge together.
    to simplify this Git simply moves thepointer forward.

2. Recursive strategy
    Git has to do some work. In this case, Git does a simple three-way merge,
    using the two snapshots pointed to by the branch tips and the common ancestor of the two.
    This is because the commit on the branch you’re on isn’t a direct ancestor of the branch you’re merging in.

Git creates a new snapshot that results from this three-way merge and automatically creates a new commit that
 points to it. This is referred to as a merge commit, and is special in that it has more than one parent .

### Deleting A Branch

the  `git branch -d [branch_name]` command is used to delete a branch.

### Basic Merge Conflict

Occasionally, this process doesn’t go smoothly. If you changed the same part of the same file
differently in the two branches you’re merging, Git won’t be able to merge them cleanly. i.e  If
you git tries to merge two  divergent branchs together and to their last commit recursivly and you've
change a particular portion of the same file in those two branches differently a merge confilct occurs
 when you try to merge the branchs together . This leads to you trying to resolve it.

So, to keep things short  when a merge confilct occurs the console and the editors provides instructions
 that help you resolve it.

Lets look at the steps taken to resolve a confilct.

1. choose to the particular changed portion you want to adapt out of the two branchs.
2. you stage you files by running `git add [file_name]`
3. commit merge  by running `git commit` .
4. final stage *:>* merge confilct succesfully resolved.

## Branch Management

Here are some git commands that will help you with you branch management.

1. `git branch` : This is used to display a list of all your local branches and indicate your current branch.`
    - the `-v` option added their last commit to the branchs  being displayed.
    - the `-d` option is used to delete already merged branchs.
    - the `-D` option is used to force delete branchs that are not yet merged.
2. `git [--merged` / --no-merged] ` :This can filter this list to branches that you have or have not
yet merged into the branch you’re currently on.

## Branching Workflows

we’ll cover some common workflows that this lightweight branching makes
possible, so you can decide if you would like to incorporate them into your own development cycle.

### Long-Running Branches

 This means you can have several branches that are always open and that you use for different stages of your
 development cycle; you can merge regularly from some of them into others.
The idea is that your branches are at various levels of stability; when they reach a more stable level,
 they’re merged into the branch above them.

Many Git developers have a workflow that embraces this approach, were the have three development stages .

1. The master : such as having only code that is entirely stable in their master branch

 — possibly only code that has been or will be released.
2. The develop or next :  they work from or use to test stability — it isn’t necessarily always stable,
 but whenever it gets to a stable state, it can be merged into master.
    - Topic branchs : They are short-lived branches  pull in by the develop or next branch .

### Topic Branches

 A topic branch is a short-lived branch that you create and use for a single particular feature or related work.

## Remote Branching

### Remote-tracking branch

Remote-tracking branches are references to the state of remote branches. They’re local references
that you can’t move; Git moves them for you whenever you do any network communication, to
make sure they accurately represent the state of the remote repository.  
Remote-tracking branch names take the form [remote]/[branch].

### Pushing

If you have a branch named serverfix that you want to work on with others, you can push it up the
same way you pushed your first branch. Run git push [remote] [branch]. (Simplified)

### Pulling

While the git fetch command will fetch all the changes on the server that you don’t have yet, it will
not modify your working directory at all. It will simply get the data for you and let you merge it
yourself. However, there is a command called git pull which is essentially a git fetch immediately
followed by a git merge in most cases.
Generally it’s better to simply use the fetch and merge commands explicitly as the magic of git pull
can often be confusing.

### Deleting Remote Branches

You can delete a remote branch using the --delete option to git push.

git push origin --delete [remote_name]

Fetching your branching  from a server is  and working on them is a topic that request lots of practice and time to
fully understand.

## Rebasing

With the rebase command, you can take all the changes that were committed on one branch and replay them
on a different branch. h, it looks like a linear history: it
appears that all the work happened in series, even when it originally happened in parallel.

This operation works by going to the common ancestor of the two branches (the one you’re on and
the one you’re rebasing onto), getting the diff introduced by each commit of the branch you’re on,
saving those diffs to temporary files, resetting the current branch to the same commit as the branch
you are rebasing onto, and finally applying each change in turn.
