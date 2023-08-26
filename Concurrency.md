# Concurrency
Concurrency means Simultaneity. Actions are Simultaneous or atleast they can appear to be simultaneous but could actually be pretty fast teamwork by the processes.

## Types of Concurrency Methods
### Pre-emptive Multitasking
In Preemptive multitasking, the Operating system takes control of when to stop a task so an other one can run. This could lead to a task not be completed as it was stopped midway
- CPU Cores required = 1 core.
- eg - Threading.
  
### Cooperative Multitasking 
Also known as Non-preemptive multitasking, here the process has the control to give up its control, This method requires some changes and additions in the code but it could be worth it as no process are stalled or stopped half a way and thus one can know when a process gives up its control.
- CPU Cores required = 1 core.
- eg - Asyncio.
  
### Multitasking
In this Method the CPU has to have more than One core as the process are actually run simultaneously. There are complexions but python does a pretty good job it handling them or so have I read.
- CPU Cores required = multi cores.
- multiprocessing.

#### Types of Problems
- ##### CPU Bound process
These process does not have the need to talk to an external device and thus they don't have to wait until they receive their data from the outside. So there are inherently faster than I/O bound process.
- ##### I/O Bound Process
These processes do have to wait for an external connection to provide them with the necessary resources to start working and hence more time is spent on waiting for the data then actually processing them.
