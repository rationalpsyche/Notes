# Commit ranges

Example

```
*   8d8faff Merge branch 'branch1'
|\  
| * 63014a8 B2
| * 2f17a05 B1
* | b9ea9df M4
* | da3150d M3
|/  
* c817b83 M2
* 9b08429 M1
```

## Double dot

`git log A..B` means all the commits reachable from B that are not reachable from A

```
$ git log HEAD^1..HEAD^2 --oneline
63014a8 B2
2f17a05 B1
$ git log HEAD^2..HEAD^1 --oneline
b9ea9df M4
da3150d M3
```

## Triple dot

`git log A..B` means all commits reachable from A and B but not from both of them

```
$ git log HEAD^1...HEAD^2 --oneline
63014a8 B2
b9ea9df M4
2f17a05 B1
da3150d M3
```

Build example:

```
mkdir commit-ranges
cd commit-ranges
git init
touch foo
git add foo
git commit -m "M1"
echo line1 >> foo
git commit -a -m "M2"
git branch branch1
git checkout branch1
touch bar 
git add bar
git commit -m "B1"
echo line1 >> bar
git commit -a -m "B2"
git checkout master
echo line2 >> foo
git commit -a -m "M3"
echo line3 >> foo
git commit -a -m "M4"
git merge branch1
git log --oneline --graph
```

