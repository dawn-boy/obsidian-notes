# 1. Lifecycle of a process
A process goes through different stages during execution. That is
- New -> Process is being created
- Ready -> Waiting to be assigned CPU
- Running -> Currently executing
- Waiting (because its blocked) -> Waiting for I/O or event
- Terminated -> Finished execution

==Context switching happens when CPU moves between processes==
# 2. Definition of Kernel
The Kernel is the core part of an operation system that directly interacts with hardware. Its functions are
- Process management
- Memory management
- Device management
- System calls handling

==The Kernel is the central component of an OS that manages system resources and provides services to programs==

# 3. Batch Operation system
A Batch OS executes jobs in groups (batches) without user interaction. It
- Collects the jobs and processes it sequentially
- has no real-time interaction
- has high throughput but slow response

# 4. Multithreaded programming
It is the ability of a process to execute multiple threads concurrently
Benefits: 
- Offers better CPU utilization
- Faster execution
- Improved responsiveness

Types of modes:
- Many-to-One
- One-to-One
- Many-to-many

==The Important thing to note is that the Threads share the same memory but just runs independantly==

# 5. Conditions for Deadlock
Deadlock occurs when these 4 conditions hold simultaneously:
1. Mutual Exclusion - Resource cannot be shared
2. Hold and wait - holding one resource and waiting for another
3. No Preemtion - Resource cannot be forcibly taken
4. Circular wait - Circular chain of process exeuction

# 6. Mutual exclusion
It ensures that only one process accesses a critical section at a time
Purpose: 
- Prevents data inconsistency
- Avoids race conditions

Methods:
- Software: Peterson's algorithm
- Hardware: Test-and-set
- Semaphores / Mutex

# 7. FCFS (First Come First Serve)
Processes are executed in order of arrival.
- There are Non-Preemptive
- Simple to implement
- Can cause convoy effect (long waiting time)

# 8. SJF (Shortest Job First)
Process with smallest exection time is selected first.
Types: 
- Non-Preemptive
- Preemptive (Shortest remaining time first)
Advantages: 
- Minimum average waiting time
Disadvantage:
- starvation of long processes

# 9. Real-time scheduling
Used in systems where time constraints are critical
Types:
- Hard real-time -> Deadline must be met
- Soft real-time -> Deadline can be missed slightly

# 10. Synchronization solution for voting process (using semphore)
- Mulitple voters vote
- Counting should happen only after all votes are cast

