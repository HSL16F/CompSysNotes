Memory management supports multiprogramming, is important security and isolation between processes and OS memory. It enables a computer to run more processes with larger memory requirements, a single process can use more memory than what's physically possible, the sum of memory requirements is permitted to be larger than what's physically possible.
Before memory abstraction, programs reference memory directly, the only way to achieve multiprogramming is to physically have running process in memory and all other processes on desk, context switch swap the disk and memory processes. Slow and inefficient.
![[Pasted image 20240411095157.png]]
For multiple processes, two programs and loaded into memory and take up physical space, issues arise in the say jump 28 instruction
![[Pasted image 20240411095257.png]]
We notice how the jump 28 in program 2, is valid in its own program but does not consider the new memory, it accesses the wrong program
**Memory abstraction** solves this issue, abstract away from physical addresses. Programs prefer to a logical address which is bound to a separate independent address. Programs only act in logical address, OS manage physical and hardware translate logical to physical in runtime (OS DOES NOT TRANSLATE)
There are two methods of memory abstraction, Dynamic relocation and Paged virtual memory
### Dynamic relocation
For DR with base and limit registers, program is loaded into consecutive memory where room fits. Two registers in CPU are used to delimit the physical memory location of the process. Base register and the limit register.
The Base register contains physical address where program begins, the beginning bound and the limit contains the length of the program so the upper bound can be calculated.
The values of the registers are determined by the OS and maintained in the [[Process Scheduling|PCB]]. They are loaded into CPU when process is allocated to CPU.
![[Pasted image 20240411101438.png]]
Here the hump to 28 is 28+16384=16412
In order to translate logical to physical addresses, the CPU (hardware) checks the logical address is less than the value of the register, if not then an exception is raised as the logical address is not within the bounds of the process.
For when the logical address is within bounds, hardware adds base on value of logical address. The CPU performs the address translation in the **Memory Management Unit**
![[Pasted image 20240411102059.png]]
![[Pasted image 20240411102121.png]]
The drawback with this process is it required contiguous sequence, the OS also needs to manage physical memory by tracking memory usage, allocating free (contiguous) memory to processes and deallocating memory when a process is swapped to disk/terminates
Linked Lists are a common approach to track memory usage, each entry contains:
- Hole (H) or Process (P)
- Address which it starts
- Length of hole/allocation
- Pointer to next entry
This is best explained with the following diagrams
![[Pasted image 20240411102507.png]]
To allocate contiguous memory, a free block must be chosen, once chosen, its divided into 2 pieced. One for the process and another for the unused space (VERY RARELY does it perfectly fit)
First fit, Best fit and worst fit are 3 algorithms for this task
First Fit:
- Allocated to the first free block that can fit the process, reduce search time
Best Fit:
- Search through entire list and allocate to smallest valid fit. This tends to create small free blocks as the smallest holes are left remaining
Worst Fit:
- Allocate largest available free block, leaves greatest left over memory hole

The process to deallocate contiguous memory can either terminate or swap out of memory. To swap, when not running, swap memory to a backing store (such as disk) and bring back to memory when executing, allows for total physical address of all processes to exceed real physical memory of system.
![[Pasted image 20240411103632.png]]
But the data structure representing the physical state of memory most be updated accordingly. Holes merged together
![[Pasted image 20240411103717.png]]

External fragmentation occurs when processes are loaded and removed from memory, leading to the case of free memory broken into small pieced, there might be enough cut sets to satisfy the memory request, however its not contiguous.![[Pasted image 20240411104023.png]]

Summary of content:
Entire process must be loaded into contiguous memory, process cannot be larger than physical memory, when more space needed, entire process swapped to disk, external fragmentation can occur, if memory usage of process grows, OS may be required to move its location.

### Paged Virtual Memory
Breaks up address spaces into fixed-sized pieces referred to as pages.
Physical memory is broken up into fixed size slots called page frames
Pages map to frames, generally the same size, each frame contains a single page and pages *do not* need to be stored in contiguous frames.
Not all pages must have physical memory at the same time to run a process, during the lifetime of a process, pages start on disk and move between disk and memory multiple times. When page is moved to disk and back, it may be put in a different page frame than previously. No requirement for the same page, frame pair.
![[Pasted image 20240411105459.png]]
Its important to ensure that there's a 1-1 mapping
![[Pasted image 20240411105542.png]]
Internal fragmentation occurs when a process is divided into fix sizes pages, there may be some leftover space on the last page. For example,
- page size = 4 bytes, process size = 13 bytes, process needs 4 pages, 4 pages is 16 bytes, internal fragmentation: 16-13=3 bytes wasted
If we select larger page sizes, more internal fragmentation occurs and smaller page tables exist (Intendent of fragmentation issue), for smaller pages, less fragmentation and greater table
![[Pasted image 20240411110433.png]]
Physical address is calculated from frame number * frame size + offset, note that offset is calculated via logical address mod page size (Typically same as the frame size), so in the case above, frame number is in the page table and the frame stated, so page 0 goes to 5, page 1 goes to 6, page 2 goes to 1 etc. This yields frame numbers 5, 6 and 1 respectively. frame size is stated as 4 bytes. 32/8 (Physical memory size/total number of frames) is another method.

Logical addresses are contracted with page number and page offset
![[Pasted image 20240411111210.png]]
m bits represent logical address, size is 2^m, in previous case, logical address space is 2^4, and logical address is 4 bits long
n bits represents the offset, 2^n, so page size is 2^2=4. 2 bits is logical address used for the page offset, it can be 0, 1, 2 or 3.
m-n bits represent the page number, process can have 2^m/2^n=2^(m-n) pages, for example, 2^4/2^2=2^2=4 pages, 2 bits are used for the page number
![[Pasted image 20240411111509.png]]
![[Pasted image 20240411111544.png]]
Page table entry contains useful information about a page, present/absent bits indicate if a page is in physical memory (1) or on disk (0), if 0, MMU will NOT translate address and page fault [[Interrupts]] is triggered
A referenced bit is when a page is referenced/accesses, MMU sets reference bit to 1
A modified bit is when a page is written to, MMU sets modified bit to 1
![[Pasted image 20240411111825.png]]
Page faults occur as some processes may not be mapped to frames, they are not in physical memory and are in some backing store (typically disk), for when a process page is not mapped, page fault is raised via the MMU (NOT OS) through an interrupt. When a page fault occurs, in the case of no free frames, the OS will pick a page frame to evict and write content to disk (Only if modified bit is set, if not, discard the page), the OS will proceed to fetch page that was referenced from disk and load into newly freed page frame, the page table is updated and restart process at instruction which caused page fault.

### Page replacement algorithms
Its desired for any page replacement algorithm to lead to the fewest number of page faults, evict the page frame that will be accessed furthers in the future and useful as a comparison point but not practical. Common algorithms are First-in, First-out (FIFO), Second Chance and Least Recently Used (LRU)

Principal of locality:
Most programs exhibit temporal and spatial locality, for temporal, if a process is accessed in a particular memory address, it will likely reference the same address in the near future, likewise if a process addresses a particular memory address, it will most likely nearby addresses in the near future. Second Chance and LUR both factor in these properties.
![[Pasted image 20240411130648.png]]
### FIFO
Evict page that has been in memory the longest, maintain a FIFO queue of pages based on load times, the one that's loaded the longest ago is the head, most recent load is tail and we evict the head and put newly mapped at tail.
Simply to implement but risk at evicting heavily used pages/
![[Pasted image 20240411125536.png]]

### Second chance algorithm
Modification of FIFO to avoid evicting recently used pages. Based around observing the referenced (R) bit of oldest page. If 0, page is old and evict, if 1, then recently used. Clear R bit, move page to tail of queue (Given second chance) and update load time of page as if it has just recently arrived
![[Pasted image 20240411130846.png]]

### LRU
Based on the premise that pages that have been accessed recently are likely to be accessed again. Evict least recently used pages, or otherwise the one that's not been used in the longest time.
Can be implemented via: Maintaining a list of all pages with most recently used page at head and least recently used at tail, page of tail of list is chosen for eviction, at every memory reference, find page that is referenced and move it to head, this is possible but has very high performance overhead

Aging can instead be approximated via a bit counter for each page. At each clock interrupt (Clock tick), shift all counters by one bit to right, append referenced bit to leftmost bit (append 1 if was referenced since last clock tick and 0 if not), at page fault evict page with lowest counter
![[Pasted image 20240411131224.png]]
![[Pasted image 20240411131235.png]]
Whilst age may be useful, it does have several limitations. it may evict a page that was not least recently used. Via recording only 1 bit per time interval, the algorithm can't tell between referenced bits earlier in the interval and later in, counters also have finite bits which limits the algorithm past a set time. If 2 pages have counter of 0, we can pick one at randomly, but in reality, one may be referenced 9 ticks ago (9 mod 2 = 0) and another 1000 ticks ago (1000 mod 2 = 0)

A **Translation Look Aside Buffer** (TLB) is an optimisation. Without it, each memory reference requires 2 memory access, one for the page table and one to access the data, TLB is fixed capacity hardware cache in the MMU (NOT OS), it stores copies of recently accessed page table entries, its implemented in associated circuitry with all entries are looked in parallel and each entry of the TLB contains information about one page
![[Pasted image 20240411131828.png]]
![[Pasted image 20240411131849.png]]
On a TLB Miss and entry from the TLB is evicted in the case its full and replaced with an entry for the page that was just looked up.
For a valid TLB bit, indicates if its cached entry is valid or not
If a page is currently running and is swapped out, the corresponding entry of the TLB becomes invalid and the page is not mapped to the frame anymore, the entry for the TLB is invalidated
On a [[CPU Scheduling|context switch]], the TLB contains mappings are only valid for currently running processes (Which are the same virtual page maps to different physical frames for different processes)
One approach is to flush the TLB context switch which invalidated all entries, a newly running process will encounter many TLB misses while the TLB is re-populated with valid entries.
