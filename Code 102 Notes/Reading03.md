# Reading 03

## Version Control

* Version Control allows a user to revert back to older commits on a given file or project
* This is useful so the user may review changes made or correct mistakes

### Local Version Control

* Stores changes to files on your hard disk
* LVCS

### Centralized Version Control

* More collabrative than Local
* CVCS
* Provides a server that can be accessed by several users
* Allows for collaboration

### Distributed Version Control

* Creates mirrored repo's
* DVCS
* Keeps people from losing all of their work in the event of corruption

## What is Git?

### Snapshots

* DVCS that stores data stores files in the form of snapshots
* Each save changed version of file is called "Commit"

### Local Operations

* Git relies on local operations
* Most necessary info can be found in local resources
* Puts project on local disk and allows user to work offline or on VPN

### Tracking Chages

* All changes tracked by Git
* Gatekeeper
* Git will always detect corruption or loss of info in transit

### Loss of Data

* Git is setup to minimize loss of data
* Difficult for snapshot to be lost

### States

* 3 main states

#### Committed

* Data securely stored in local database

#### Modified

* File has been changed but not securely stored

#### Staged

* Flagged a files changed version to be stored in next snapshot

## Check File Status

* Determine state of file
* git status command
* Indicates what branch you're on
* Working directory clean meaning files have tracked or modified status

## Tracking and Staging a New File

### Single File

* Track one file only by using following format
* git add filename

### All Files

* Track all files in repository using following command
* $ git add *
* After using these commands files are tracked and stagged for committing
* After adding new file called EXAMPLE, you will see info about changes to be committed when using git status command
* $ git status
* This info tells us there are changes to be committed and the file has been staged

## Committing a File

* After staging on eor multiple files, commit the changes and record a commit message
* $ git commit -m "made change x,y,z"
* This step has committed changes for the file or files
* You can have one commit message for multiple files

## Committing All Changes

* $ git commit -a
* This command commits a snapshot of all mods to tracked files in working directory

## Pushing Changes

* Push changes to remote repository
* $ git push origin master
* This command pushes changes from local "master" branch to remote repo named "origin"
* Cloned repo, Git will automatically give the name "origin" to the server from which you cloned and the name "master" to your local repo
* these names can be changed by the user
