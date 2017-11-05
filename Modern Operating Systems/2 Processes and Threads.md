# Processes

A child process can itself create more processes, forming a process hierarchy. A process has only one parent so a process is more like an hydra than a cow. A process and all of its children and descendant form a process group.

All processes in the whole system belong to a single tree, with `init` at the root.

When a process is created the parent is given a **handle** to control the child. However this token can be passed to some other process, invalidating the hierarchy.

A process can be in one of three states: running, blocked, ready

# Threads

Each process has an address space and a single thread of control. Nevertheless it is desiderable to have multiple threads of control in the same address space running in quasi-parallel as if they were (almost) separate processes (except for the shared address space).

threads are faster (10-100 times) to create and destroy compared to processes. Morevoer threads are useful on systems with multiple CPUs where real parallelism is possible.

**Example 1.** Word processor

If a word processor were single threaded then whenever a disk backup started, commands from the keyboard and mouse would be ignored until the backup was finished. We can think of a thread that interacts with the user, a second that reformats the document when asked to and a third that writes content from ram to disk periodically. Having three different processes here would not work because they all need to operate on the document.

**Example 2.** Web server

A dispatcher thread to read incoming requests from the network and worker threads to handle the requests.

There exists an alternative to simulate threads and their stacks the hard way: finite state machine. 

Model | Characteristic
--- | ---
Threads | Parallelism, blocking system calls
Single thread system process | No parallelism, blocking system calls
Finite state machine | Parallelism, non blockig system calls, interrupts


## Classical thread model

Processes are used to group resources together. Threads are the entities scheduled for execution on the CPU.

When a multithreaded process is run on a single CPU, the threads take turns running.

**Remark.** different threads in a process are not as independent as different processes. All threads have the same address space, which means they also share the same global variables.
One thread can read, write or even wipe out another thread's stack. There is no protection mechanism between threads because it is impossible and it should not be necessary. Unlike different processes, which may be from different users, a process is always owned by a single user.

Per-process item | Per-thread item
--- | ---
Address space | Program counter
Global variablles | Registers
Open files | Stack
Child processes | State
Pending alarms | 
Signals and signals handlers | 
Accounting information | 

