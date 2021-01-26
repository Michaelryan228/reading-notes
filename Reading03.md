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
