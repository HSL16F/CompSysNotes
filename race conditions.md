Race conditions occur when multiple processes/threads access a shared resource such as a shared variable. The results depend on the timing of the code's execution, the order in which instructions are executed and the results are indeterminate and vary unpredictably across different executions.
![[Pasted image 20240410002403.png]]
![[Pasted image 20240410002434.png]]
![[Pasted image 20240410002454.png]]
![[Pasted image 20240410002703.png]]
Two important concepts for avoiding race conditions are:

**Critical Region**: part of the program where resources are shared
**Mutual Exclusion**: Guarantee that only 1 process/thread executes within the critical region at any given point in time
Important to understand and be able to calculate run time of some algorithims for MST
![[Pasted image 20240410002927.png]]
If property of mutual exclusion then, transcript 2 would never occur but 1 would execute fine
![[Pasted image 20240410003004.png]]
![[Pasted image 20240410003050.png]]
**Conditions for a *good* mutual exclusion:**
- No processes can access their critical region at the same time (Mutual Exclusion)
- One can not make assumptions on speed or number of CPU's
- Processes outside of the critical region can not block other processes
- No process can wait forever to enter the critical region (Starvation)
Mutual Exclusion is typically achieved via locks to control access to the critical region, with an Acquire Lock to enter the critical region and a Release lock when exiting the critical region, only process/thread with the lock can exist in the critical region
![[Pasted image 20240410110413.png]]
A context switch is the method in which the OS stops execution of one thread/process (t/p) and starts execution of another t/p, in the case of the above example, the context switch is right after exiting the loop but just before executing the instruction, in this case, lock = 1; however its important to note in the above example, as there is the exception that the execution of a thread is stopped right after executing the loop and just before the setting lock to 1, then its possible to have two threads in the loop. If we assume that 2 threads are executing in the threadFunction(),
1. ThreadA tests lock !=0 -> false exits loop, lock is 0
2. ThreadB tests lock !=0 -> false exits loop, lock is 0
3. ThreadA executes lock = 1 (lock is 1) enters critical region
4. ThreadB executes lock = 1 (lock is 1) enters critical region
In the case above, threadA and B both check if the lock is 1, before ThreadA can set it to 1, ThreadB also checks if the lock is 1 and finds its at 0, so they both proceed to enter the critical region

To achieve some form of mutual exclusion, several methods and techniques are applied such as **Busy Waiting** and **Blocking**
#### Busy waiting
- Strict alteration
- TSL with busy waiting
When a process wishes to enter the critical region, we check if entry is permitted, if not the process executes a loop to continuously check if/when it may enter the region, this has the drawback of wasting cpu and the [[Race Conditions Cases|Priority Inversion Problem]]
Busy waiting approach has 2 p/t which take turns running in the critical region (One is busy, the other/s waiting), for example [[busy waiting example|busy waiting example with strict alteration]]
In the example linked, thread B is blocking A from entering the critical region, however Thread B is outside of the critical region, to prevent this problem of strict alteration, we apply **Test and set Lock (TSL)**.
Hardware supports locking and TSL instruction has a TSL register, lock.
We copy contents of LOCK into REGISTER and proceed to store non-zero value in LOCK, this is an example of atomic operations which are indivisible, that means that either the operations occur or they do not.
TSL is the LITERAL HARDWARE LOCK

**Mutual Exclusion** with **TSL** and busy waiting has the following instruction set
1. TSL REGISTER, LOCK
2. If REGISTER is 0, enter critical region
3. if REGISTER is not 0, lock is set so go back to step 1 (Busy wait)
When leaving the critical region, we set lock to 0, implying critical region is ready to be accessed and locked again
Some assembly
![[Pasted image 20240410115613.png]]
#### Blocking
- Mutex
Useful for when a thread wishes to enter its critical region, checking if entry is allowed, for when its not, another thread uses CPU while waiting for the lock, this can occur via a block or yield. Blocking works though has various drawbacks depending on the specific approach, such as starvation, overhead of system calls, overhead of context switches etc
Mutex is unlocked, basically
![[Pasted image 20240410115756.png]]
![[Pasted image 20240410115806.png]]
Deadlocks occur if each process in the set is waiting for an event that only the another process in the set can cause, this can exist under various shared resource settings such as driving in a busy city as a classic example. You can't go till the other person lets you but they can't go cause you're blocking them.

