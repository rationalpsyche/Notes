# Memory Management

## A memory abstraction: address spaces

Exposing physical memory to processes has several major drawbacks. First, if user programs can access every byte of memory they can easily thrash the operating system. Second, it is difficult to have multiple programs running at once.

An address space is the set of addresses that a process can use to address memory. Each process has its own address space.

## Virtual memory

Each program has its own address space which is broken up into chunks called **pages**. Each page is a continuous range of addresses. These pages are mapped onto physical memory but not all of them have to be mapped at the same time.

Virtual memory is a generalization of the base-and-limit register idea.

### Paging

When virtual memory is used, the virtual addresses do not go directly to the memory bus. Instead they go to an MMU (Memory Management Unit) that maps the virtual addresses onto the physical memory.

The virtual address space consists of fixed-size units called pages. The corresponding units in the physical memory are called **page frames**. The pages and page frames are usually the same size.

### Page Tables

The virtual address is split into a virtual page number (high order bits) and an offset (low order bits). The virtual page number is used as an index into the page table to find the entry for that virtual page.

The page frame number is attached to the high order end of the offset, replacing the virtual page number, to form a physical address.

#### Structure of a page table entry

`| | Caching disable | Referenced | Modified | Protection | Present/Absent | Page frame number |`

* *present/absent* is set to 1 the entry is valid and can be used. Accessing a page set to 0 causes a page fault.

* *protection* tells what kinds of access are permitted

* *modified* and *referenced* keep track of pag usage

	When the O.S. reclaims a page frame, if it has not been modified it can be abandoned since the disk copy is still valid.

* *referenced* helps the O.S. to choose which page to evict when a page fault happens. Pages that are not being used are far better candidates.

