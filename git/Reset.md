# Reset

`git reset` changes the HEAD ref to point to the given commit

|     | `--soft` | `--mixed` | `--hard` |
| --- | --- | --- | --- |
| `HEAD` | point to new commit | point to new commit | point to new commit |
| index changes | keep | discard | discard |
| working directory | keep | keep | discard |
