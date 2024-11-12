Here lists various problems and cases for race conditions
Priority Inversion Problem:
	For the case of a computer running 2 processes
	  `P_high` has high priority
	  `P_low` has low priority
	Scheduling rules: `P_high` always gets to run as long as it is not _blocked_
	At a particular moment:
	`P_low` is in the critical region
	`P_high` becomes ready to run (e.g., I/O operation completed)
	`P_high` starts running and begins busy waiting (can't enter critical region because `P_low` is in it)
	`P_low` never gets to exit the critical region because it never gets scheduled to use the CPU while `P_high` is running
	`P_high` loops forever
The issue comes as a result of where the P_high always runs when the needed, and P_low no longer runs, but for this case, p_high needs to run whilst the p_low is in the critical region it can't leave whilst p_high is running since p_low has the lock