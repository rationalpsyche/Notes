## Detached HEAD

A *ref* is a name for a SHA-1. Branches or tags are refs.

HEAD is a symbolic reference to the tip of a branch, it usually points to a ref instead of directly to the SHA-1.

```
mkdir detached-head
cd detached-head
git init
touch foo
git add foo
git commit -m "C1"

$ git log --oneline
27b59acbba1159365a0c2ec48c549482cd6cea4e

$ cat .git/HEAD
ref: refs/heads/master

$ cat .git/refs/heads/master
27b59acbba1159365a0c2ec48c549482cd6cea4e

git checkout -b branch1
touch bar 
git add bar
git commit -m "B1"

$ git log --oneline -1
94576f196aed3baa69f3b3d226ec3d16ca65b56c

$ cat .git/HEAD
ref: refs/heads/branch1

$ cat refs/heads/branch1
94576f196aed3baa69f3b3d226ec3d16ca65b56c
```

When you checkout anything that is not a proper local branch name then HEAD is no longer a symbolic reference but it actually contains the SHA-1 hash of the commit you are switching to. This is called a **detached HEAD**.

