Logical addresses for the same physical memory can be the same or different. Usually two processes won't have access to the same memory, since then one can corrupt the other. However, if they have arranged to use some form of shared memory, they will usually map that shared memory to different addresses. Virtual addresses are more or less a type of logical address, so if you have an operating system that supports VM, and two processes map shared memory, they will usually see that memory as being at different addresses, the same as if there was no virtual memory.


# Segmentation
segments don't have a fixed size and by that form holes, when being loaded to -. and dropped out of the main memory
- hardware support is provided and implemented by the memory
management unit (MMU)
- the MMU provides protection for segmentation violations
	- verification of access rights to read, write and execute commands depending on segments
	- traps indicate segmentation violations () segmentation fault)
	- programs and operating system are protected from each other
- replacing the segment base on each context switch
	- processes have their own translation table () stored in its PCB)
- simplification of swapping
	- after swapping-in only the segment table must be adjusted
- shared segments for text (program code) and data (shared
memory) are possible
	- Segment-table base register (STBR) points to the segment table’s location in memory
	- Segment-table length register (STLR) indicates number of segments used by a program

##### Problems 
- memory fragmentation due to frequent swapping in/out (or start/termination) of processes (**external fragmentation**)
-> solution: compacting:
	- segments are moved to defragment memory in order to close holes
	-  segment table needs to be adjusted and updated
	-  performance penalty
- issue: long I/0 time overhead due to swapping-in/out
	
https://www.geeksforgeeks.org/segmentation-in-operating-system/


# Paging
- pages have fixed size 4(4096 Bytes) K or 8 K
-  can be located at any position in the physical address space
	- solves the fragmentation problem
	- no more compacting necessary
	- simplifies memory allocation and swapping in and out
- virtual memory is also subdivided into pages, which map to the physical memory


### Problems 
- paging leads to **internal fragmentation**
	- last page my not be used completely
- page size
	- small pages reduce internal fragmentation, but increase size of page table(and vice versa)
- large table that must be kept in memory
- many implicit memory accesses necessary


## Paging, regarding swapping in/out
- it is no longer necessary to swap-in/out an entire segment
-  pages can be swapped in and out individually
-  page faults, hardware support
-  if the presence bit is set, everything
remains as before
-  if the presence bit is cleared,
a trap is triggered (page fault)
-  trap handling can now be used for
loading the page from the background
memory and repeat the memory
access afterwards (requires hardware support in the CPU


## paging Discussion on Operational Costs
- page faults may occur very frequently
- page translations (virtual to physical addresses) are expensive
- translation lookaside buffer(TLB): hardware cache stores recent translations of virtual memory to physical memory addresses
- https://www.geeksforgeeks.org/paging-in-operating-system/

