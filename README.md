

# Introduction to OS (1)

How to get started:
1) in terminal ```gcc –std=c99 –o helloWorld helloWorld.c ```
2) run ```./helloWorld```

Lecture 1

Kernel is running at all times on the computer.

Computer system can be broken to 4
1) Hardware (CPU), I/O devices
2)OS - control system
3)Apps 
4) Users- people, other machines


When computer starts "bootstrap program" is loaded which is stored in ROM or EPROM (firmware). It initilases all aspects of the system, loads kerner and begins execution.

- interrupt
Tells CPU that something stopped or requies attention to figure out the next move. The "interrupt" is is sent to interrupt service routes that contains all the serivces running. A Trap or exception is caused by error or if if a user requested which shuts the programm. AN OS is interrupt driven.  Basically a computer can do 1 task at the time, but it computes so fast and interupts processes that are not neeed, which might give an impression that everythng works conccurently on your computer.

- 
killobyte 1024
MB 1024^2
GB 1024^3
TB 1024^4
PB 1024^5

- Direct memory access
Devices transfer blocks of data from buffer storage directly without CPU intervention. 

- Storage structure
Larger storage is slower comparing to smaller main ones. 
The hieargy is :
1) speed
2) cost
3) volatility

- Caching
Caching is taking information into a faster storage system.

If neeed to access info, checks cache first, and if its there it uses it, if no, then save to cache and use it
between CPU and memory is cache section as well. 

- Computer system arhitecture
Multiprocesors known as parallel system, tighly coupled system
The advantage of this : 
1) Economy of scale
2) Increased reliability
With 2 types, assymetric, and symetric (all processors are symmetrical, no dominant) 

- Dual core design
UMA - unified memory arhitecture
NUMA - non - unified

- Clustered systems
A few PC, solving a common problem, have SAN (storage area network).
Asymetric - one machine in standby
Symmetric - all working conccurently
Apps can be written in paralesization.
Sometimes have DLM (distributed lock manager) to avoid conflicts

- OS structure
Multiprogramming - u can have a few more threads of execution at the same time. Cannot keep CPU and IO devices busy at all times. Job scheduling, to have a better managment of CPU usage.

Timehsaring - CPU switches jobs. CPU scheduling for processes, if no memory that swaping moves them in and our to run. 

Interrupt driven by hardware, if error happens an exception or trap is thrown (infinte loops).Dual mode allows OS to protect itself and other system components:
1) User mode
2) Kernel mode

Practical 1

PROGRAMMING
stdio.h
printf() for printing output
scanf() to get read input

Types:
1)Integral => unsigned short 2 bytes, unsigned 4 bytes, unsigned long 8 bytes, non neg numbers || signed integers => short, int, long, whole numbers.
Floating => float 4 bytes, double 8 bytes, long double 16 bytes

Char
char c = "a" with ASCI encoding is 97
so if c + 1 , it would be "b" if we do printf("%c", c + 1) but if we change "%c" to "%d" and do + 2 then we will get 99. SO depending on what exactly we need to display.

chars start from 65 (A) to 90 (Z) and 97(a) - 122(z)

the sizeof 
unsigned n = sizeof(char);

Pointers
Storing memory address of a variable

(type) *pointer; will store an address of something yet to be declared
int *p;

int i = 3, *p;
p = &i; which will be sotring the address of I, so any manipulations with p will affect i.

void *pointer; is for any type

```man man``` is the guide for linux


# Operating system structures (2)
Lecture 2
OS gives envrionemnt for app execution and services to users and other apps.One set, User find helpful:
1) User interface (CLI, UI, GUI, Batch(old))
2)apps
3)I/O
4)FIle system manipulation
5)Communication - processes might exchange information with one another, or different users.
6) Error detection 

Another set is for ensuring efficiency
1) Resource allocation - if apps working concurently must allocate CPU and other resource in adequate manner
2)Accouting - task manager
3)Protection and security - what belongs to who

From set 1
CLI - command line interface - sometimes made in kernel or by sys apps, sometimes multiple flavours - shells, can work directly with kernel
GUI - Desktop and all other things

System calls
If a user wants to access something or an app, a system called is invoked. Mostly used via API (application programming interface). For example, open file, copy, and paste it somewhere. A user choses something and it goes to API (system calls table) which invokes system calls.
Parameteres of system call are pushed onto the stack by the app and popped off by the OS.

Types of system calls: Process control (abort, execute, load etc), File managment(create, copy etc), Device manager, Information Maintenance (time, data etc), Protection (ownership, acces to resouces), Communication (connectivity).

Fork() duplicates the process, if PID returns more than 0 then its a parent, if no its a parent so if(pid > 0) {parent};

Layyered approach, 
MS-DOS was before, single tasking system, CMD if what u use
FreeBSD - Unix - multisking, user login, uses fork, exec to start the prgrammm

Sys apps, expose users to create system calls in convinient manner to manipulate files, other apps, etc.

Microkernel, software that has a very little amount of functions and features required to implement an operating system. Minimal number of mechanism, just to start the system, so other parts of OS can be more efficient since it doesnt impose lots of policies. Performance cn be overhead

Practical 2
Array declaration
int grades[100] - one dimension
int a[2][3] - 2 dimensions
int b[2][3][4] - 3 dimensions

initialisation
int c[] = {1,2,3}
int c[3] = {1,2,3}

int a[2][3]= {{1,2,3},{4,5,6}} no need to specify the first param of the array, but the rest is a must
int (*b)[3][4] 
int a[5]; from 0 to 4

an array name is an adress or pointer adress of the first element  the array. To assign array to another array like 'arayOne = arayTwo' is not allowed, but can be done through the loop.

Main arguments

To read command line arguments from main we should include the following into parameteres ```int argc, char *argv[]``` argc stands for the quantity of arguments passed and argv is the argument itself and can be accessed via ```argv[0]``` argv[0] to get the name of the file

Structure (Struct)

Quite similar to objects but in C you have to define the type of a variable like 
```
struct student {
char *last_name;
int student_id;
char grade;
}
``` and then struct student s1, class[100];
so after u can implement something like s1.grade = "A" etc.

Memory in C

4 catgories, goes in the following order
1) Code memory
2) Static data memory - variables. Initialised before the main begins and exists till the end.
3) Runtime stack memory - function calls (return address, params, local variable(inside of functions), internal registers machine specific info)
4) Heap memory - the memory that is given during runtime, dynamic

callcoc() and malloc() memory allocation <sdlib.h>
calloc(size_t n, size_t s), n => object, s => bytes
malloc(size_t s) just the size, should be manually deactivated
both should be positive, if u want to free, then free(address).

# Processes (3)
Lecture 3

IS executes various aps
1) Batch system jobs (processesor in task manager)
2)Time -share sysstems (user apps or tasks)

.The code is called - (text section)
.Stack keeps the local variables, params, return addresses
.Data section - global variables
.Heap memory allocating during run time (malloc)

Programm becomes a process after executable file exe. is loaded. Can be started with GUI, mouse clicks, CMD etc. One app can be multiple processes.

Process states:
1) New - creation
2) Running - instructions are executed
3) Waiting - waiting for any event to happen
4) Ready - ready to be assigned to processor
5) Terminated - finished execution
 The logic is NEW -> READY -> RUNNING -> either: READY || WAITING(i/o) || TERMINATED

TASK CONTROL BLOCK
Keepng the information about the processes
1) State
2) Counter (ID)
3) CPU register, pointers to STACK etc
4) CPU scheduling -> prioritisation
5) Memory managment -> how much memory is used for something or allocated
6) Accounting information ->  Task manager
7) I/O status information 

Threads
Process has a single thread of execution. Multiple threading will require more programm counters. Must have a storage for thread details.

Process scheduling
TO maximise to CPU performance, process scheduler selects among available processes for next execution on CPU. 
Job queue - set all processes in the system
Ready qeue - residing in main memory waiting to execute
Device queue- I/O

Schedulers
Long term - selects what to be into ready queue, might be slow(mins, secs), degree of multi-programming, 
Short term - which one to be executed next, works in miliseconds
Processes can be either: 
1) I/O bound process - most of the time waiting, no computation
2) CPU bound processes, computations
Medium term scheduler - Mix between the two

Context switch
When CPU switches between processes it records the states and saves the one one
Time dependant on hardware. Context switch is overhead so doesnt do anything much, its just something we need to do.

Process creation
Parent process creates children process, and forming a tree of processes, you can view ```pstree -ap``` or ```pstree -ap | grep (what u neeed)``` will show you PID and the process itself. 
Options for children and parents:
1)PArents and children share all resources
2)Children share subset of parents resources
3) No sharing
Exec options
1) Can start parents and children conccurently
2) Parent wait until children is terminated
Address space, child duplicate of parent, child has a programm loaded into it
Fork() dublicates the process -> can then call exec to call other processes and then exits and merges with waiting parent.
CHild returns ALWAAYS = 0
PARENT returns the process ID of the process
Child can also find out it own PID after a system call. Can also wait(NULL) for all children to execute.

Process termination
Process asks the OS to delete it ```exit()```
Parent may terminate the excution of children by abort(), if no needed, or resources have exceeded, or if parent is shutting down. if no parent waiting then its a zombie process, if parent is terminated then its children are orphans.

Interprocess communication
Reasons for cooperation: information sharing, computation speedup, modularity, convinience. Two models of IPC (interprocess communication):
1)shared memmory
2) Message passing, to synchronise actions, communicate with each without sharing variables. send(message) and receive(message) can be used
Implemention is either physical or logical 

Producer-consumer problem
Unbounded buffer - places without limit on the size of buffer
bounded buffer - with limits

Syncronisation
Blocking is considrred synchronous
Blocking send has a sender block until the message is recieved
Blocking recieve has a reciver block untill a message is available

Non -blocking - is async
It doesnt wait, it sends and resumes normal operations.

Practical 3
