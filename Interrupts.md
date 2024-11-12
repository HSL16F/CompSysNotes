When Interrupts occur, CPU loads:
- PSW to indicate execution in kernel mode and the PC with the address in the specified entry in the interrupt vector which is the address of the interrupt handler function
Once handler finishes running, the execution of the interrupted application continues where it was left off except for case when the OS killed the application or scheduled another application.

Several types of interrupts:
External interrupts which are generated by external devices at unpredictable times:
- Clock interrupts tells the OS that a certain amount of time has passed
- I/O device interrupts tells OS that an I/O operation has completed
Internal interrupts which caused by exception when executing current instruction, process cannot complete the instruction so it transfers responsibility to OS
- Error condition: When current application has performed illegal operation (Divide by zero, attempt to issue privileged instruction etc)
- Temporary problem: Process access page of memory that not allocated to at moment (miss), which can be solved by OS bringing required page to memory