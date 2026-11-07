# Viva Session 1: Operating Systems Notes

Operating Systems Concepts:
1. Deadlock: A situation where a set of processes are blocked because each process is holding a resource and waiting for another resource held by another process.
Four Coffman Conditions: Mutual Exclusion, Hold and Wait, No Preemption, Circular Wait.
Prevention: Violate at least one of the four conditions.
Avoidance: Banker's Algorithm uses resource allocation state and safe state detection.

2. Paging and Virtual Memory:
Virtual memory allows execution of processes not completely in physical memory.
Paging divides virtual memory into pages and physical memory into frames.
Page Fault: Occurs when a program accesses a page mapped in virtual address space, but not currently in physical RAM.
Thrashing: A state where the CPU spends more time swapping pages in and out than executing actual process instructions due to insufficient memory.

### Question 1:
In Deadlock handling, both Prevention and Avoidance aim to keep the system out of a deadlock state, but they do so fundamentally differently. Explain the core difference in how they operate, and specify which Coffman condition the Banker’s Algorithm primarily targets or eliminates.

### Candidate Answer:

Deadlock Prevention works by placing static constraints on resource requests to ensure that at least one of the four Coffman conditions (Mutual Exclusion, Hold and Wait, No Preemption, Circular Wait) can never hold.

Deadlock Avoidance, on the other hand, dynamically tracks resource allocation state and makes decisions at runtime to ensure the system always remains in a "safe state".

Regarding Banker's Algorithm: It does not eliminate any Coffman condition statically. Instead, it dynamically avoids deadlocks by ensuring that resource allocation never leads to an unsafe state, primarily preventing the occurrence of Circular Wait at runtime.

### Question 2:
Moving on to Paging and Virtual Memory:

1.Walk through the exact sequence of events that the Operating System and hardware perform from the instant an instruction triggers a Page Fault to the moment that instruction resumes execution.

2.If multiple processes trigger excessive page faults simultaneously, the system enters Thrashing. Why does increasing the degree of multiprogramming in this situation usually make thrashing worse rather than better?

Explain the control flow clearly.

### Candidate Answer :

1. Sequence of events during a Page Fault:
- The CPU attempts to access a memory address whose valid-invalid bit in the page table is set to 'invalid', triggering a hardware trap/interrupt to the OS.
- The OS traps into kernel mode and saves the process state (registers, program counter).
- The OS verifies whether the memory reference is valid. If invalid, the process is terminated; if valid, it needs to bring the page from backing store (disk).
- The OS finds a free physical frame (using page replacement like LRU/FIFO if no free frame exists).
- A disk I/O operation is scheduled to read the desired page from secondary storage into the allocated physical frame.
- While waiting for I/O completion, the CPU schedules another process.
- Once disk I/O completes, an I/O interrupt occurs. The OS updates the page table (sets the frame number and flips the bit to 'valid').
- The original process state is restored, and the instruction that caused the fault is restarted from the exact point of interruption.

2. Why increasing degree of multiprogramming worsens Thrashing:
- When thrashing occurs, CPU utilization drops because all current processes are blocked waiting for page-swapping I/O.
- If the OS misinterprets low CPU utilization as the system being underloaded and increases the degree of multiprogramming, it brings more processes into memory.
- These new processes demand even more frames from the already scarce pool of physical memory.
- Existing processes lose their working set frames, resulting in an exponentially higher page fault frequency.
- As a consequence, the paging disk queue becomes completely saturated and the system grinds to a near halt.

### Question 3:
To conclude the session, let's look at how the OS actively detects and resolves Thrashing:How does Peter Denning’s Working-Set Model prevent thrashing? Define what the working-set parameter ($\Delta$) represents and how the OS decides whether to suspend or resume a process based on memory demand.Alternatively, how does the Page-Fault Frequency (PFF) scheme achieve dynamic frame allocation without continuously tracking referenced pages across a sliding window?Take a moment to explain the operational logic of both approaches.

### Candidate Answer:

1. Peter Denning's Working-Set Model:
- Working-Set Parameter (Δ): Represents a fixed number of most recent page references (the working-set window). The set of distinct pages referenced within the last Δ time units forms the Working Set (WSS_i) of process P_i.
- Demand Calculation: The total memory demand is D = Σ |WSS_i|.
- Allocation/Suspension Decision: 
  * If D > total available frames (m), thrashing is imminent. The OS suspends (swaps out) one or more active processes, releasing their allocated frames to remaining processes.
  * If D < m, memory demand is safely accommodated; the OS can resume or admit a new suspended process to maintain high CPU utilization.

2. Page-Fault Frequency (PFF) Strategy:
- Operational Logic: PFF directly measures the rate at which a process faults instead of tracking every reference across a sliding window.
- Upper and Lower Bounds: The OS establishes two static thresholds: an upper bound (U) and a lower bound (L).
- Dynamic Adjustment:
  * If a process's page-fault rate exceeds U, it lacks sufficient frames -> the OS allocates an additional physical frame to it. If no free frames exist, a process is suspended.
  * If its page-fault rate drops below L, it has excess allocated frames -> the OS reclaims unused frames from it.
- This creates direct, event-driven feedback during page faults without continuous tracking overhead.


Topic,Focus Area,Performance & Key Strengths,Status
Deadlock Handling,Prevention vs. Avoidance & Banker's Algorithm,Distinguished static constraints vs. dynamic state analysis; correctly identified that Banker's algorithm prevents circular wait dynamically without eliminating Coffman conditions upfront.,Mastered
Virtual Memory & Paging,Page Fault Control Flow,"Accurate sequence from invalid bit trap and kernel mode switch to backing-store I/O, page table update, and exact instruction restart.",Mastered
System Degradation,Thrashing Mechanics,Explained the CPU scheduler's feedback loop and why increasing multiprogramming exacerbates memory starvation.,Mastered
Thrashing Mitigation,Working-Set Model & PFF,"Correctly defined Δ, D>m admission/suspension rules, and the upper/lower bound event-driven logic of PFF.",Mastered



