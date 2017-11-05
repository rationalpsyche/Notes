# Operating System Concepts

## Processes 

A process is basically a program in execution. Associated with each process is its address space, a list of memory locations from 0 to some maximum, which the process can read and write. The address space contains:

* the executable program
* the program's data
* the program's stack

Also associated with each process there is a list of resources, commonly including registers (program counter, stack pointer), a list of open files, list of related processes.

When a process is suspended temporarily it must later be restarted in exactly the same state it was stopped.

Every process started has the same UID of the person who started it.
A child process has the same UID as its parent.

## Files

The process and files hierarchies both are organized as trees but the similarity stops there. Process hierarchies are usually not very deep, they are short lived (generally minutes at most).

An important concept in Unix is the **special file**. They are provided in order to make I/O devices look like files.
Two kind of special file exist: block special files and character special files.

Block files are used to model devices that consist of a collection of randomly addressable blocks, such as disks.
Character files are used to model printers, modems and other devices that accept or output a character stream.
By convention special files are kept in `/dev`

A pipe is a sort of pseudofile that can be used to connect two processes. Thus communication between processes in Unix look like ordinary file reads and writes.

## Onthogeny recapitulates Phylogeny

The development of an embryo (ontogeny) repeats the evolution of the species (phylogeny). In other words, after fertilization, a human egg goes through stages of being a fish, a pig and so on before turning into a human baby (this is a gross semplification but it has a kernel of truth in it).

It frequently happens that a change in technology renders some idea obsolete and it quickly vanishes. However another change in technology could revive it again. In biology extinction is forever but in computer science it is sometimes only for a few years.

## System calls

Making a system call is like making a special kind of procedure call, only system calls enter the kernel and procedure calls do not.

It is worth noting that the mapping of POSIX procedures is not one to one.

### fork

`fork` is the only way to create a new process in POSIX. It creates an exact duplicate of the process. After the fork, the original process and the copy go their separate ways. The program text, which is unchangeable, is shared between parent and child. The fork call returns a value, which is zero in the child and equal to the child's PID in the parent. Using the returned PID the two processes can see which one is the parent and which one the child.