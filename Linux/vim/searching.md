# Searching

## Search in line

* `f{character}` move forward to the next occurrence of character
* `F{character}` as above but backward
* `;` repeat last search in the same direction
* `,` repeat in the opposite direction
* `t` as `f` but before the character
* `T` as `F` but after the character

The commands are motions hence they can be combined as usual, for example:

* `dtw`

## Search in all file

* `/` forward
* `?` backward
* `*` over a word search the whole word
* `n` next result
* `N` previous

## Change a word
`/and`, `cw`, type the new word, esc, `n` to next occurrence and `.` to repeat the last command

## Find and replace

* `[range]s/old/new[flags]` (the default range is the current line)
* g flag replace all recurrences
* `1,5s/old/new/`
* `.,$` (`.` represent the current line, `$` the last line in the file)
* `%` is the entire file (shortcut of `1,$`)
* `/pattern1/,/pattern2/s/old/new/`
* `/pattern/,$s/old/new/`
* what if you want to replace slashes without escaping? Use another pattern separator
* `:#/var/spool/#/usr/local/#`

