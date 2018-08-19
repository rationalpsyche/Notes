## Detached HEAD

A *ref* is a name for a SHA. Branches or tags are refs.

HEAD is a symbolic reference to the tip of a branch, it usually points to a ref instead of directly to the SHA.

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