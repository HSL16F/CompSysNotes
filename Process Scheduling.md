A process is a running program and fundamental abstraction provided by the OS, provided programs their own dedicated abstract machine to run on, multiple processes can run the same program. A program can be thought of as the code which is static or a recipe, whilst a process can be thought of in a more dynamic light such as executing the program or as cooking.
Processes exist to run multiple programs simultaneously on a single CPU, and therefore supports multiprogramming (MP)
MP allows programs to share a CPU and pseudo run in parallel due to the OS providing illusion of parallelism via very rapid and efficient switching of processes
![[Pasted image 20240408235619.png]]
For MP, process execution is interleaved, is not parallel, but akin to it, MP increases efficiency and scheduling programs determine which process runs next and for how long.

A process can be created via 4 main causes:
- System initialisation
- Execution of a process creation [[Operating Systems|system call]] by a running process
- User requests to create a new process
- Initiation of a batch job

In unix, fork() is such a system call which creates a clone of the calling process with different address space, same memory image, program counter, registers and open files
![[Pasted image 20240409000141.png]]
fork() is usually followed by an invocation to a function in the exec() family, for example; execave() causes the program that is currently running by the calling process to be replaced with a new program, with newly initialised stack, heap and data segments.

Several termination processes:
- Normal exit (voluntary)
- Error exit (voluntary)
- Fatal Error (involuntary)
- Killed by another process (involuntary)

Processes exist within 3 states and represented via the following state diagram:
![[Pasted image 20240409085820.png]]
The states that can exist are:
- Running: Using CPU
- Ready: Runnable, but temporarily stopped
- Blocked: unable to run until some other external event occurs
![[Pasted image 20240409091128.png]]

### Process Control Block (PCB):
- Stores information regarding process execution environment and data structure referred to as the PCB. The process table is an array of PCB's. OS maintains a list of PCB's, with one PCB per process
- Examples of data stored in PCB's include: Process ID, process state, parent process, memory management information, file descriptors, priority, used CPU time, PC, stack pointer, [[scheduling algorithms]] etc

### Threads
Threads provide execution context to a process, they are a sequential execution of a set of instructions which has a PC, stack pointer, registers and a stack
To run, the execution context of the thread is loaded into the CPU's registers: PC, SP and general purpose registers with intermediate values for ongoing computations
When not running, the context is not in the CPU, its stored in memory and the processor's register will hold the context of another thread. PC and SP register points point to instructions and stack of other threads respectively.
Example of at Multi-threaded execution
![[Pasted image 20240409093127.png]]

Threads are permitted to execute within the environment as defined by a process, a process *can* have one or more threads.
Per-process items:
- Address space
- Global variables
- Open files
- Child processes
- Pending alarms
- Signals and signal handlers
- Accounting information
Per-thread items:
- Program Counter
- Registers
- Stack
- State

Note that all threads of a process share the same address space, code, data, heap memory shared between threads and each thread has its own stack
An example of a single threaded process
![[Pasted image 20240409094721.png]]
Whilst a multithreaded process looks as follows
![[Pasted image 20240409094739.png]]

The benefit of threads includes parallelism and enables the overlapping of I/O with other activities
A program has potential to use multiple processors to each perform portions of the work, speeding up the completion of a program and performing operations on a very large array where each thread operations on intendent sections of the array.
Multi-threading with I/O allows us to avoid blocking processes whilst waiting for I/O. One thread can manage I/O and other threads can perform more useful activity in the CPU, contexts where this is useful includes web severs and databases.

Threads share an address space, are faster and incur less overhead when switching oppose to processes but do not provide isolation, one thread can bring an entire process down.
Processes enable applications to parallelised beyond a single machine (Useful for servers), provide isolated execution environments and incur in interprocess communication overhead

The Thread Control Blocks (TCBs) is where the context data of the thread is stored in. It differs from PCBs where processes are stored.
Examples of TCB data includes: Thread ID, SP, PC, Register Values, state (running, blocked, ready), pointer to PCB of the process to which thread belongs to.

POSIX is a standard API for thread creation and synchronisation, functions start with pthread, include pthread.j and threads have an id of type pthread_t
![[Pasted image 20240409104026.png]]
