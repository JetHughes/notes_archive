---
title: "14-processes-and-system-calls"
aliases: 
tags: 
- cosc204
- lecture
sr-due: 2024-07-14
sr-interval: 349
sr-ease: 250
---

- heirarchical structure in software systems
- system calls and interrupts
- representing process in OSs
- overview of process scheduling

# Heirarchical structure
software systems have modularity
- os kernel
- system programs
- applicatioin programs
![Heirarchical structure diagram|400](https://i.imgur.com/Tf7QDTy.png)

## application programs
Defn: a program that ordinary usrers interact with, running in user space

e.g.,
- word processor
- video player
- web browser
- games
- etc

## system programs/libraries
Defn: a program which provides general purpose power level function, packeages in a way which is convenient for a user (e.g., sys admin or programmer) to employ

system program types include.,
- file manipulation progarms
- status info programs
- network and device management programs
- compilers assemblers and interpreters
- various library code
- command shell programs (e.g., command interpreters)

also runs in user space

# system calls
processes issue requests to the kernel by making system calls

![system call diagram|300](https://i.imgur.com/GAktF7t.png)

they are requesets to the OS kernel made through interrupt handlers

the set of system calls is termed the programmer interface to OS

System calls in xv6
- fork() Create a new process 
- exit() Terminate the current process 
- wait() Wait for a child process to exit 
- kill(pid) Terminate a process identified with pid 
- getpid() Return the ID number of the current process 
- sleep(n) Put the current process into sleep for n seconds 
- exec(filename, *argv) Load a file named filename and execute it with arguments in argv 
- sbrk(n) Update the process memory space by n bytes 
- open(filename, flags) Open a file named filename with flags indicating read/write 
- read(fd, buf, n) Read n bytes from an open file fd into buf 
- write(fd, buf, n) Write n bytes from buf to an open file fd 
- close(fd) Close the open file fd
- dup(fd) Duplicate the open file fd into another file 
- descriptor (the return value) 
- pipe(p) Create a pipe and return the file descriptors in p 
- chdir(dirname) Change the current working directory of the process to dirname 
- mkdir(dirname) Create a new directory dirname 
- mknod(name, major, minor) Create a device file name with major and minor numbers 
- fstat(fd) Return status information about an open file fd 
- link(f1, f2) Create another name f2 for the file f1 
- unlink(filename) Remove a file named filename

## interrupts
### detecting interrupt
CPU hardware containes a wire called the interrupt requirest line

when a cpu is running an instruction-execute cycle
- fetch instruction from memory and store it in instruction register
- decode/execute instruction

an extra step is included
- sense the interrupt request line.
- it it has a signal, then respond to the interrupt

### responding interrupt
when interrupt detected, CPU switches to kernel space, and a handler function provided by the OS is invoked
- the context of the current instructionis saved
- control is transferred to a fixed memory location holding an interrupt-handling routine
- when the routine is finished, it restores the context of the interrupted process

the interrupt vector is an array of lications thta hold the addresses of these interrupt-handling routines. (usually held in low memory)

this is hard to do
- how to restore context?
- nested handlers?

### what causes them
generated by:
- errors: e.g., division by zero, invalid memory access
- I/O device signals:; e.g., completion of IO operation or arrival of network packet
- system calls (also called trap or soft interrupt) with special instruction (int or svc)

a system call generates an interrupt and the OS transfers control to a system call handler

# Processes
a process is dynamic

a given program can be executing many times of a given machines: each instance is a separate process

process components
- text section/code section: the program code itself 
- data section: any global variables used by the program 
- process stack: any local variables currently being used 
- program counter: a pointer to some place in the program code 
- contents of CPU registers 
- memory management information 
- device/file allocation information 
- accounting information

## process control blocks
the OS keeps a record of each process in the system, with a data structure called *process control block* (PCB)

![example block|400](https://i.imgur.com/UTDFjse.png)

![example linux processes|400](https://i.imgur.com/ar19swB.png)

## scheduling processes
processes take turns to run on the CPU. processes wait to run in one of two queues:
- ready queue: process ready to execute
- device queue: processes waiting to use a particular device. (one queue per device)

generally represented as linked lists

## flow of processes
![process flow diagram|400](https://i.imgur.com/ib1t78H.png)

Rounded rectangles are events. 
Rectangles are queues where processes wait. 
Circles are processing resources that serve the events/queues.

## process creation
created by another process: parent process creates a child process
- process can copy itself using fork
- child process can then call exec() to load a new program
	- a child process can run concurrently with parent
	- child process can share the resources of its parent if not restricted

system start with one process called *init*

## procees heirarchy
processes for a tree
![process tree diagram|400](https://i.imgur.com/SNTlCNZ.png)
