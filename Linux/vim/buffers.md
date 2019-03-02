# Buffers

## Open multiple files

* `vim file1 file2 ...` or `vim file*`
* `:edit filename` or `:e`
* `badd file` to add a buffer without switching to it
* `bd` delete buffer, examples: `bd1,3`, `bd2`, `bd filename`
* `:Explore` to open a file

## Inspect buffers

* `:buffers` or `:ls`
* change buffer with `:b<number>` or `:bfilename`
* `:b` ctrl d to see the buffers
* `:bn` next, `:bp` previous
* `:bf` first, `:bl` last
* switch to the previous opened buffer `ctrl ^` (notice with `:ls` how the indicators `a` and `#` switch)
* to switch buffer without saving append `!`

A buffer can be in 3 states:
* a active - loaded in memory and being displayed
* h hidden - loaded in memory and not displayed
* inactive - (no indicators) not loaded in memory

## Options

* `set hidden` to switch buffer without saving
* `qall` or `wall`
* `:bufdo set nu` to set an option for all buffers
* replace in all buffers `bufdo %s/#/@/g | w` (the pipe is the command separator)
