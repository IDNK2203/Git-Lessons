# Understanding Git Basics

## Recording Changes to the Repository

`git diff` shows changes that are yet to be staged

`git diff --staged` shows staged changes that will be included in the next commit  

the -a option is used with commit to stage all modified files in the workspace  and commit command , used as `git commit -a`

### Removing files

we use the `git rm` command it reomves the file from the working directory so you don't  see it as untracked file , the process looks like this .

- we delete/remove file  from the working directory

- we call `git rm` to stage the removal of the as changes  

- we commit changes

### Renaming and Moving Files  

we used the git mv command , it work like this

- `git mv file_from file _to`

## Viewing the Commit History

the `git log` is most basic and powerful tool used for this purpose

- the `-patch` or `-p` option is used to show the difference introduce in each commit and a number option can also be  included to limit the number of entry such as `-2` .

- the `--stat` option is used to print a commit list entry with their respective modified file showing lines added and lines removed.

- they are some other option used in getting printing a controlled commit history but we'll skipped that for now.

## Undoing things

- the `git commit --amend` is used to redo your last commit

- the `git reset HEAD` is used to unstaged a staged file

- while the git checkout replaces all that changes that has not been staged/commited to the last commited version  

## working with Remotes

### Showing your Remotes

- `git remote` is used to lists the shortnames of each remote handle you’ve specified.

- `git remote -v` shows you the URL stored in this shortnames.

### Adding Remote Repositories

- git remote are bindings used to store reference to a project in remote server

- `git remote add [shortname] [url]` is used to add git remote repository .

- you can use the shortname with commands to perform operations in the command line

### Fetching and Pulling from Your Remotes

- `git fetch origin` fetches any new work that has been pushed to that server since you cloned (or last fetched from) it. The command only downloads the data to your local repository

- The `git pull remote branch` command generally fetches data from the server you originally cloned from and automatically tries to merge it into the code you’re currently working on.

### Pushing to Your Remotes

- The `git push remote branch` commad is used to push commit to your online repository.

- This command works only if you cloned from a server to which you have write access and if nobody has pushed in the meantime.(only when the repo commit histories are the same)

### Inspecting a Remotes  

- `git remote show [remote]` show information about a particular remote

- It lists the URL for the remote repository as well as the tracking branch information.

### Renaming and Removing Remotes

- `git remote rename`  is use to change a remote’s shortname

- it used like this `git remote rename old_name new_name`

- while `git remote remove or git remote rm` is used to remove a remote

## Tagging

git tags are used to mark specific points in a repository’s history as being important

- The `git tag` shows  entire list of tags

- `the git tag --list/-l pattern` is used to show a list of tag matching a specific patten

### TYPES OF TAGS

#### lightweight tags

- A pointer to a specfic commit
- `git tag [tag_name]`

#### Annotated tags

- They are stored as full objects in the Git database.

- They hold information like date, tag message , tagger name and email etc.  
- The `git tag -a [tag_name] -m [tag msg]`
- The `git show [tag_name]` shows the tag data along with the commit that was tagged .

### Tagging Later

Tag a commit later, you specify the commit checksum (or part of it) at the end of the command .

### Sharing Tags

By default, the git push command doesn’t transfer tags to remote server.  

- you can run `git push origin [tagname]` to push tags to the shared server  

- `git push --tags` transfer all of your tags to the remote server that are not already there.  

### Deleting Tags

- `git tag -d [tagname]` is used to a tag on your local repository  

- `git push origin --delete [tagname]` is used for deleting tags fromm your remote server.

## Git Aliases

This is a git feature that gives you flexiblity when it comes to git commands. it allows you to
create aliases for git commands , ( sort of like renaming a command ) and this has several benefits.
The command for initiating this process can be shown below.

- `git config --global alias.[new_comand_name_extension] [old_command_name_extension]`

Here are a couple of examples .

> - $ `git config --global alias.co checkout`
> - $ `git config --global alias.br branch`
> - $ `git config --global alias.ci commit`
> - $ `git config --global alias.st status`
