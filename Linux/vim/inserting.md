# Inserting

* `i` insert on the cursor
* `I` as `i` but beginning of line (first non blank character)
* `a` appends text after cursor position
* `A` appends to end of line
* `o` create a line below
* `O` create a line above

Count works also with insert: e.g. 

* `10ia` will give aaaaaaaaaa
* `5o#`
* `5o10.11.12`

* `R` replace mode
* `r` replace single character
* `cw` change a word; same as `dw` but goes into insert mode

* `~`  switch case
* `g~w` as above to word 
* `g~$` as above until end of line
* `U` upper case (instead of switch)
* `u` lower case
* `J` join two lines

