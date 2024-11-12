For a single core CPU, multiprogramming requires switching CPU among processes which demands [[scheduling algorithms]] 
![[Pasted image 20240410134425.png]]
Scheduling units can be single threaded process or a thread, however its typical to prefer to this as unit as a process, but at a high level, both thread and process apply, for now only referring to process

### Context switch:
Changing execution contexts such as transitioning from executing one process to another. Thread and context switches do differ, where's a thread context switch saves the execution context of the current thread to the [[Process Scheduling|TCB]] and loads the execution context of another thread from another TCB to the CPU.
A process context switch includes saving/loading execution contexts (Like a thread context switch) as well as loading state related to memory management from PCB (Such as pointer to page table) and flushing Translation lookaside Buffer in a paged system with virtual memory
![[Pasted image 20240410135947.png]]
Most processes alternate bursts of computing with I/O requests (Such as disk or network), there are two typical process behaviour.
- CPU-bound processes: Which spend most time in computing and are typically long CPU bursts
- I/O-bound processes: Spend most time waiting for I/O and typically very short CPU bursts
![[Pasted image 20240410140307.png]]
CPU scheduling picks a process to run from a set of ready to execute processes, a blocked process cannot run and if a process is running and initiates an I/O operation, it blocks and the scheduler finds another process to run.
There are two main categories of CPU [[scheduling algorithms ]]which are covered in more detail for the rest of the notes. Non Pre-emptive shortened to NPE and Pre-emptive as PE
There are two main environments for scheduling:
Batch systems and Interactive systems:
**Batch systems** are typically (sometimes) periodic set of jobs that need to run. They don't require interaction from users and NPE and PE scheduling with long quantum are good choice for these environments.
For **interactive systems**, PE is essential, involves users and expect a fast response time from the system. Imagine a powerpoint presentation, videogame etc, all require rapid response based on some input
