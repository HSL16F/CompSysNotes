Note that this page includes mix of OS and hardware
Operating systems includes content for:
- [[Interprocess communication]]
- [[Process Scheduling]]
- [[Memory Management]]
An OS can be thought of as a bridge between the hardware and applications/user, an OS ensures that programs run efficiently and provides hardware abstraction and manage hardware resources
![[Pasted image 20240403230042.png]]
Resource management is critically important has processor, memory and I/O devices all are desired by programs, so OS plays critical role of deciding who and what resource is allocated to which program, when, how much and for how long.
Note that some areas of hardware may be managed by the hardware not OS, but this is typically with regarding memory management
The hardware which runs on a computer consists of two main components
- The CPU which performs computation and the memory which is where data is stored
- Registers are part of CPU
	- General purpose registers which are very fast and typically used to store heavily used variables
	- Special purpose registers (SPR) which control very specific functions
- The ALU is the arithmetic logic unit of the CPU
![[Pasted image 20240403230531.png]]
Each cycle involves a fetch, decode, execute cycle
- CPU gets instruction from memory which involves fetch command, with Program counter which keeps track of memory address of next instruction to be executed in a program, this operates like a stack
- Understand what the instruction is which is decoding
- Executing the instruction which may involve operands from memory to registers, using ALU to perform some operation on values and storing results in another register
![[Pasted image 20240403233037.png]]

Subroutine support involves call and ret instructions, hardware supports the calling of subroutines and returning ret and call instructions from them,
Subroutines do not have visibility into registers/variables of caller function and they require environments to execute
The state of calling function must be maintained when subroutine returns

The stack is quite important which is a special region of memory that stores information on active subroutines which involves various stack frames that correspond to a **call** to a **subroutine** that's yet to be terminated, they contain at least an address to return to when subroutine call is complete, contain input args and loval vars. The stack pointer (SP) points to the top of the stack
![[Pasted image 20240403233413.png]]

Call instructions:
- Store register values on stack at the location pointed by the SP
- Return the address after the call instruction on the stack
- Load the PC with the address entry point of the called subroutine
- Increment the SP to point to the new top of stack
- Visually described as follows
See lec slides for visual example
Ret instruction:
- Restores the register values from the stack
- Loads PC with return address that also stored in stack
- Decrement SP to point to previous frame
The hardware enforces memory boundaries between process, not the OS, this allows OS to prevent any given application from modifying memory of another and to protect itself

Execution mode is determined by the Program Status Word (PSW), kernel and user mode
User mode:
- Code running in user mode cannot issue privileged instructions and can only access memory allowed by the OS
Kernel mode:
- Can issue all instructions and access all memory
- Privileged instructions defined by instructions which affect control of the machine or do I/O
OS operate in kernel mode

[[Interrupts]] are important events which cause CPU to not execute the next instruction, CPU enters kernel mode and execute OS interrupt handler, the interrupt vector (in OS memory) stores addresses of interrupt handlers

System calls are an interface between user programs and OS, the cycle of a system call instruction involves
- Putting system call number in place where OS expects such as a register
- Executing TRAP instruction to switch from user to kernel mode and execute within a fixed address of the kernel
- Kernel code which starts following TRAP examines system call number and dispatches it to correct system-call handle
- System call handler runs
System calls are essentially a way for an OS to execute some operation or command within the kernel mode, they exist for security purposes
![[Pasted image 20240404000517.png]]
![[Pasted image 20240404000526.png]]
