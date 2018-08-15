# Relative commit names

The caret `^` is used to **select a different parent**

The tilde `~` is used to **go back before a parent** and select a preceding generation

If HEAD was a merge then:
* **first parent** is the branch into which we merged
* **second parent** is the branch we merged

For linear history `~` is equivalent to `^`

## Example

* `HEAD~2`: 2 commits older than HEAD
* `HEAD^2`: the second parent of HEAD, if HEAD was a merge
* `HEAD~~`: 2 commits older than HEAD
* `HEAD^^`: 2 commits older than HEAD

```
*   b890a4d Merge branches 'branch1' and 'branch2' into integration
|\  
| * 81d9113 B2
| * 151c8d7 B1
* | a45a1d9 A3
* | d865aa3 A2
* | 1598477 A1
|/  
* 7b79408 First commit
```

Build example:

```
mkdir tilde-caret
cd tilde-caret
git init
touch foo
git add foo
git commit -m "First commit"
git branch branch1
git branch branch2
git branch integration
git checkout branch1
echo line1 >> foo
git commit -a -m "A1"
echo line2 >> foo
git commit -a -m "A2"
echo line3 >> foo
git commit -a -m "A3"
git checkout branch2
echo line1 >> bar
git add bar
git commit -m "B1"
echo line2 >> bar
git commit -a -m "B2"
git checkout integration
git merge branch1 branch2
git log --oneline ---graph
```