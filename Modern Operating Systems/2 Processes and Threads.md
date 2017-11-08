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

## POSIX threads

Thread call | Description
--- | ---
`pthread_create` | Create a new thread
`pthread_exit` | Terminate the calling thread
`pthread_join` | Wait for a specific thread to exit
`pthread_yield` | Release the CPU to let another thread run
`pthread_attr_init` | Create and initialize a thread's attribute structure

The call `pthread_create` is very much like `fork` (except with parameters), with the thread identifier playing the role of the PID.
Sometimes a thread is not logically blocked but it feels that it has run long enough and wants to give another thread a chance to run.

## InterProcess Communication

In IPC there are 3 issues: 
* how can one process pass information to another
* how to make sure two processes do not get into each other way
* proper sequencing when dependencies are present

### Race Conditions

In order to avoid race conditions we need **mutual exclusion**.

The part of the program where the shared memory is accessed is called *critical region* or *critical section*. A requirement to avoid race conditions is that no two processes are in their critical region at the same time. However this condition itself is not sufficient for having parallel processes cooperate correctly and efficiently. We need the following:

1. No two processes may be simultaneously inside their critical regions
2. No assumption may be made about speeds or the number of CPUs
3. No process running outside its critical region may block any process 
4. No process should have to wait forever to enter its critical region

#### Mutual exclusion by busy waiting

** Disable interrupts**

On a single processor system the easiest solution is to have each process disable all interrupts after entering its critical region and re-enable them just before leaving it.

This approach is unacctractive since it is unwise to give user processes the power to turn off interrupts. What if one process does not turn them on? It would be the end of the system.

** Lock variables **

We could consider a shared (lock) variable set to 0. If the lock is 0 the process sets it to 1 and enters its critical region. If the lock is already 1 the process waits until it becomes 0.

Unfortunately there is a flaw: suppose one process reads the lock and sees it is 0. Before it can set the lock to 1 another process is scheduled, runs and sets the lock to 1.

** Strict alternation **

```
while (TRUE) {
	while (turn != 0) critical_region();

	turn = 1;
	noncritical_region();
}
```

Continuously testing a variable until some value appears is called **busy waiting**. It should be avoided since it wastes CPU time.
A lock that uses busy waiting is called a **spin lock**.

Taking turns is not a good idea when one of the two processes is much slower than the other.

This situation violates condition 3 set above.

** Peterson's solution **

```
#define FALSE 0
#define TRUE  1
#define N	  2

int turn;
int interested[N];

void enter_region(int process) {
	int other;
	other = 1-process;
	interested[process] = TRUE;
	turn = process;
	while (turn == process && interested[other] == TRUE) /* null statement */ ;
}

void leave_region(int process) {
	interested[process] = FALSE;
}
```

**The TSL instruction**

`TSL RX, LOCK`

The TSL (Test and Set Lock) instruction works as follows: it reads the content of the memory word *lock* into register `RX` and then stores a non zero value at the memory address lock. The operations of reading the word and storing into it are guaranteed to be indivisible. 

It is important to note that locking the memory bus is very different from disabling the interrupts. Disabling interrupts then performing a read on memory word followed by a write does not prevent a second processor on the bus from accessing the word between the read and write.

```
enter_region:
	TSL REGISTER,LOCK		// copy lock to register and set lock to 1
	CMP REGISTER,#0			// was lock zero?
	JNE enter_region		// if it was not zero lock was set, so loop
	RET

leave_region:
	MOVE LOCK,#0
	RET
```

An alternative instruction to TSL is XCHG which exchanges the content of two locations atomically.

**Sleep and Wakeup**

Both Peterson's solution and the ones using TSL or XCHG are correct, but both have the defect of requiring busy waiting. In essence what these solutions do is this: when a process wants to enter its critical region, it checks to see if the entry is allowed. If it is not the process just sits in a tight loop waiting until it is.

Not only this approach wastes CPU time but also leads to unexpected results. Let us have two processes H and L, with high and low priorities respectively. When L is in its critical region, H becomes ready to run. H begins busy waiting but since L is never scheduled while H is running, L never gets a chance to leave its critical region, so H loops forever. This is sometimes referred to as the **priority inversion problem**.
