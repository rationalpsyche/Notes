# Registers

Register types:
* Unnamed `""` ; 
* Numbered `"0 "1 ..."9`
* Named `"a ... "z` (remark: with uppercase you append instead of replacing)

* `:reg` inspect registers ( `^J` represents a new line)
* `:reg 1as` to inspect desired registers
* `""` holds text from `d,c,s,x` and `y` operations
* `"0` holds last text yanked
* `"1` holds last text deleted `d` or changed `c`
* `"_"` black hole register; it is used to perform the operation without affecting any register

Specify the register to use before the command, e.g. `"0p" or `"cyy"

`[register][count]operator`



