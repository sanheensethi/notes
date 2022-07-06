## Process vs Program

Process - A process is a program in execution
- For example, when we write a program in C or C++ and compile it, the compiler creates binary code. The original code and binary code are both programs. When we actually run the binary code, it becomes a process. 
- Process : Active Entity
- Program : Passive Entity
- A single program can create many processes when run multiple times; for example, when we open a .exe or binary file multiple times, multiple instances begin (multiple processes are created). 

## Attributes or Characteristics of a Process 
1. Process Id:    A unique identifier assigned by the operating system
2. Process State: Can be ready, running, etc.
3. CPU registers: Like the Program Counter (CPU registers must be saved and 
                  restored when a process is swapped in and out of CPU)
4. Accounts information:
5. I/O status information: For example, devices allocated to the process, 
                           open files, etc
6. CPU scheduling information: For example, Priority (Different processes may have different priorities, for example a shorter process assigned high priority in the shortest job first scheduling)

## States of Process :

![image](https://user-images.githubusercontent.com/35686407/177384421-36974d5a-9eb5-472d-a140-6ec9032f6847.png)

1. `New`: Newly Created Process (or) being-created process.
2. `Ready`: After creation process moves to Ready state, i.e. the process is ready for execution.
3. `Run`: Currently running process in CPU (only one process at a time can be under execution in a single processor).
4. `Wait (or Block)`: When a process requests I/O access.
5. `Complete (or Terminated)`: The process completed its execution.
6. `Suspended Ready`: When the ready queue becomes full, some processes  are moved to suspended ready state
7. `Suspended Block`: When waiting queue becomes full.

## Context Switching :
The process of saving the context of one process and loading the context of another process is known as Context Switching. In simple terms, it is like loading and unloading the process from the running state to the ready state. 

> When does context switching happen? 
1. When a high-priority process comes to a ready state (i.e. with higher priority than the running process) 
2. An Interrupt occurs 
3. User and kernel-mode switch (It is not necessary though) 
4. Preemptive CPU scheduling used. 

## CPU-Bound vs I/O-Bound Processes: 
- A CPU-bound process requires more CPU time or spends more time in the running state. 
- An I/O-bound process requires more I/O time and less CPU time. An I/O-bound process spends more time in the waiting state. 

## Multiprogramming – We have many processes ready to run. There are two types of multiprogramming:

- `Pre-emption` – Process is forcefully removed from CPU. Pre-emption is also called as time sharing or multitasking.
- `Non pre-emption` – Processes are not removed until they complete the execution.

## Degree of multiprogramming – 
- The number of processes that can reside in the ready state at maximum decides the degree of multiprogramming, e.g., if the degree of programming = 100, this means 100 processes can reside in the ready state at maximum.

















