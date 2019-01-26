# Bash cheatsheet

## Variables 

```
HOST="localhost"
echo $HOST

# assign to a variable the output of a command
HOST=$(hostname)
```

### Variable scope

Variables are global by default. They can be defined as local with the `local` keyword

```
f() {
	GLOBAL_VAR=1
}

g() {
	local LOCAL_VAR=1
}
```

## Conditionals

### if/elif/else

```
$SHELL=$0

if [ $SHELL = "bash" ] 
then
	echo "bash"
elif [ $SHELL = "csh"]
	echo "csh"
else
	echo "Other"
fi
```

**Remark.** `[]` is portable across shells while `[[]]` is an extension to the standard and support [extra operations](https://www.gnu.org/software/bash/manual/bashref.html#Conditional-Constructs)

### and or

```
HOST="google.com"
$(ping -c 1 $HOST) && echo "Host up"
$(ping -c 1 $HOST) || echo "Host not reachable"
```

### Case statement

```
case "$1" in 
	yes|YES)
		echo "start"
		;;
	[nN]|[nN][oO])
		echo "stop"
		;;
	*)
		echo "Usage: $0 [start|stop]"
esac
```

## Loops

### for

```
for COLOR in red green blue
do
	echo "Color: $COLOR"
done

for FILE in *.txt
do
	echo $FILE
done
```

### while

```
while [[ $@ ]]; do
	echo $1
	shift
done

INDEX=1

while [[ $INDEX -lt 6 ]]; do
	echo $INDEX
	((INDEX++))
done
```

## Functions

```
function f() {
	echo "hi $1"
	return 0
}

f marck
```

## Special parameters

* `$1 $2 ...` expand to the first,second, ... parameter
* `$@` expands to the positional parameters starting from one
* `$?` expands to the exit status of the last command
* `$$` expands the process id of the shell
* `$0` expands the name of the shell

## User input

`read -p "Enter input: " INPUT`

## Debugging

* `#!/bin/bash -x` display commands and their arguments as they are executed
* `#!/bin/bash -v` display shell input lines as they are read
* `#!/bin/bash -e` exit upon error

```
echo "Debug on"
set +x
echo "Debug off"
set -x
```
