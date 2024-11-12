### Pre-emptive
After picking a process,
- Let it run for maximum set fixed time (Referred to as a quantum)
- If the thread is still running at end of quantum, suspend it and the scheduler will decide some other process to run
- Clock interrupts are needed to give control of the CPU back to the scheduler and typically result in more context switches oppose to non pre-emptive scheduling algorithms
### Non Pre-emptive
- Pick a process to run and let it run until it blocks or voluntarily releases the CPU
- Context switches are only performed when absolutely necessarily, such as the cases when the process cannot use the CPU

The goal of all scheduling systems is fairness and efficient use of resources.
Fairness is defined by processes that get a fair share of the CPU, comparable processes should receive comparable service.
Efficient use of resources is defined by reducing overhead by minimisation of switches. For example, allowing I/O bound jobs to use CPU when they need it, as to ensure that I/O devices are always kept busy.

Batch systems maximise throughput and number of processes that are completed per time uni and minimise **turnaround** time via the interval from time of submission of a process to the time of completion.
Interactive systems **minimise** response time via time between issuing a command and getting a result

NPE algorithms include:
### First-come First-served FCFS
Run process in order they are ready to execute in
Current running process stops executing (blocks) the process that has been ready to queue for the longest time. FIFO Queue is applied, process at head of queue gets to run, append new *ready* process to tail of queue
![[Pasted image 20240410183806.png]]
Simple and effective, low context switching overhead
Convey exists, short processes wait behind long process, I/O bound may spend long time queuing, leads to reduced utilisation (I/O idle whilst I/O bound process wait for CPU), this therefore has longer turnaround times. Starvation possible if entirely CPU bound (No I/O operations) such as the case of infinite loop in CPU bound
### Shortest Job First SJF
Schedule job by the least amount of work (Shortest bound) until next I/O request or completion
![[Pasted image 20240410184418.png]]
Issue in requiring estimating length of CPU bursts, optimal average turnaround time for a given set of jobs that are available simultaneously. Within the context of the OS, a job is the next CPU process
However there is the issue that a processes with a long CPU burst can be starved with shorter processes constantly arriving

PE algorithms
### Round Robin
Runs a process for a quantum, switches to next job ready in queue, repeat until all processes are finished. If process blocks/completes before its quantum, pick next process.
Important to calculate the turnaround time and `T_avg`
We note that the estimated response time (CPU burst) of a process produced a response time as soon as it runs, so the response time = time of first run - arrival time (ready in queue)
![[Pasted image 20240410222042.png]]
![[Pasted image 20240410222149.png]]
![[Pasted image 20240410222400.png]]
![[Pasted image 20240410222414.png]]
Note that its important to choose the *right* Quantum, too long and RR becomes FCFS, less context switching overhead and less responsive. When shorter more context switch overhead but more responsive
Length of quantum needs to minimise responsiveness and minimise context switching
its generally easy to implement, but not good for turn around time, good for response time, generally fair but favours CPU bound process over I/O. Overhead of context switch depends on length of quantum and no starvation present

### Priority Scheduling
Weighted approach via assigning a priority to each job and allocating CPU to highest priority process that is ready to run/
Priorities can be assigned statistically at process creation or dynamically adjusted throughout execution process.
To avoid starvation, priority adapts and changes, decrease priority after each clock interrupt (clock tick), preempt process if its priority dropped below that of the next highest process
One example is Multi-level Feedback Queue
### Multi-level Feedback Queue
![[Pasted image 20240410225057.png]]
![[Pasted image 20240410225107.png]]
I/O bound processes are given priority over CPU bound ones, good performance for short-running jobs and makes long running CPU intensive workloads
CPU bound processes get large quantum every once in while oppose to small quant frequently. No priori knowledge required of the processes needed, can observe their behaviour and prioritise them accordingly. The following parameters are included: Number of queues, scheduling algorithm per queue and the quantum for each queue.
