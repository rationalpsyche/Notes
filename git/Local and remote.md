# Local and remote

## Local branches

You can list them with `git branch`

#### Non tracking local branches

Non tracking local branches are not associated with any other branch. You create them with `git branch <branchname>`

#### Tracking local branches

Tracking local branches are branches associated with another branch, usually a remote tracking branch.

You can list them with `git branch -vv` or inspect `.git/config`

## Remote

A *remote* is a short name used to refer to a specific git repository. For convenience a remote called *origin*
is automatically created when you clone a repo, pointing to the repo you cloned from.

To list all remotes `git remote -v`

Each remote has a directory under `.git/refs/remotes/`

### Remote tracking branches (still on your machine)

Think of your remote tracking branches as your local cache for what the remote machines contain. You can update them with `git fetch`.

You can list them with `git branch -r`


## Whole process

```
Workspace          Index    Local repo    Remote Repo
    |                |           |             |
    |<--- diff ----->|           |             | 
    |<--- checkout --|           |             |
    |<------- checkout HEAD -----|             |
    |------ add ---->|           |             |
    |                |---commit->|             |
    |<-------------- fetch or pull ------------|
    |                            | --- push -->|
```