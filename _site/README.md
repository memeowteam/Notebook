# Embedded Notebook
Nothing, just Mike and Johnny's notebook

<br> [<kbd> <br> ABOUT US <br> </kbd>][ABOUT_US]<br>

# Some Words About This Notebook
## Because two people are contributing to this notebook, there are differences in styles 
**Mike's articles** written as if you have already known the basic and the knowledge only remind but not clearly for you to understand from zero
## Some huge parts will be separated to another files
**C++** \
**Python** \
**Robot Operating System** 
## We are not familiar with web applications so our GitHub Webpage is for fun, our main target is knowledge

# Table of contents
- [Table of contents](#table-of-contents)
- [Some Words About This Notebook](#some-words-about-this-notebook)
- [1. C](#1-c)
  - [1.1. C keywords](#11-c-keywords)
  - [1.2. Variables declaration](#12-variables-declaration)
  - [1.3. Memory Layout](#13-memory-layout)
  - [1.4. Volatile keyword](#14-volatile-keyword)
  - [1.5. Pointer](#15-pointer)
  - [1.6. Function pointer](#16-function-pointer)
  - [1.7. Struct & Union & Enum](#17-struct--union--enum)
  - [1.8. Extern & Static](#18-extern--static)
  - [1.9. Compilation Model](#19-compilation-model)
  - [1.10. Static & Dynamic Library](#110-static--dynamic-library)
  - [1.11. Function Invoker](#111-function-invoker)
  - [1.12. Inline Function](#112-inline-function)
  - [1.13. Dynamic Memory Allocation](#113-dynamic-memory-allocation)
- [C++](C++/C++.md)
- [Python](Python/Python.md)
- [2. Computer Architect](#2-computer-architect)
  - [2.1. Von Neumann & Harvard](#21-von-neumann--harvard)
  - [2.2. Little endian & Big endian](#22-little-endian--big-endian)
- [3. Embedded](#3-embedded)
  - [3.1. Digital & Analog](#31-digital--analog)
  - [3.2. Embedded Systems](#32-embedded-systems)
  - [3.3. Cypher-Physical Systems](#33-cypher-physical-systems)
  - [3.4. Sensors & Actuators](#34-sensors--actuators)
  - [3.5. Internet of Things](#35-internet-of-things)
- [4. Micro-controller](#4-micro-controller)
  - [GPIO](#gpio)
  - [Interrupt](#interrupt)
  - [ADC & DAC](#adc--dac)
  - [PWM](#pwm)
  - [Protocol & Interface](#protocol--interface)
  - [Some Couple Term In Protocols](#some-couple-term-in-protocols)
  - [USART](#usart)
  - [I2C](#i2c)
  - [SPI](#spi)
  - [CAN](#can)
  - [WiFi](#wifi)
  - [Bluetooth](#bluetooth)
  - [MQTT](#mqtt)
- [5. Operating System](#4-operating-system)
  - [5.1. OS Definition](#41-os-definition)
  - [5.2. OS Functions](#42-os-functions)
  - [5.3. OS Types](#43-os-types)
  - [5.4. OS Components](#44-os-components)
- [6. RTOS](#5-rtos)
- [Robot Operating System](ROS/ROS.md)
- [7. Linux Embedded](#6-linux-embedded)
- [Available soon](#undistributed) 

# 1. C

## 1.1. C keywords

 auto	          | double	      | int	          | struct 
 :---:          | :---:         |  :---:        | :---:        
 **break**	    | **else**	    | **long**	    | **switch**    
 **case**	      | **enum**	    | **register**	| **typedef**   
 **char**	      | **extern**	  | **return**	  | **union**     
 **continue**	  | **for**	      | **signed**	  | **void**      
 **do**	        | **if**	      | **static**	  | **while**     
 **default**	  | **goto**	    | **sizeof**	  | **volatile**  
 **const**	    | **float**	    | **short**	    | **unsigned**  

## 1.2. Variables declaration
*type-qualifier(s) type-modifier data-type variable-name = initial-value;* \
`type-qualifier`: *const, volatile, restrict* \
`type-modifier`: *short, long, unsigned, signed* \
`data-type`: *integer (int), floating point (double, float), enumerated, derived (array, struct, union, pointer), void* 

## 1.3. Memory Layout
**Memory layout** from low to high addresses in C includes: 
* `Text Segment` (code segment): executable instructions - sharable & read-only
* **initialized data**: global variables, static variables initialized (declared $\neq$ 0)
* **uninitialized data**: global variables, static variables uninitialized or initialized to 0
* **heap**: dynamic memory allocation (forget deallocation cause **Memory leak**)
* **stack**: automatic variable storage, function frame (runout of *stack memory* cause **Stack overflow**)

**Notice**: memory layout in C is not memory layout in computer, this will be discussed in Operating Systems part

## 1.4. Volatile keyword
**volatile**: used to indicate to the compiler that a variable's value may change unexpectedly \
*volatile* is usually used when you turn on compiler's optimization function 
* Peripheral register mapping to memory 
* Interrupt Service Routines (ISRs) 
* Multi-thread applications
**const volatile**: same as volatile but you can't change its value by the code

## 1.5. Pointer:
**pointer** is variables that hold address \
*pointer* point to any type have same size \
In C, we don't have reference parameter so we can use *pointer* to substitute

## 1.6. Function pointer:
**function pointer** is a pointer to const because function address place on *code segment* which is *read-only* \
*syntax*: data-type (*function-name)(parameter) \
e.g. `void (*pointer_function)()`: pointer function point to a function with no parameter and return void

## 1.7. Struct & Union & Enum
**struct**, **union** and **enum** are user-define data types \
**struct** is used to group related variables (members) into one  
`struct in C` need to use *typedef* to don't use *struct* keyword whenever declare a new *struct variable*. In C++, it is not necessary \
**union** allows to store different data types to same memory     \
**enum** is usually used to assign name to integral constants \
`data structure alignment` is the term that means compiler "padding" into space between 2 data "naturally aligned", this mechanism help compiler better performance. We should arrange data in *struct* reasonable to optimize memory and performance

## 1.8. Extern & Static
**extern** is used to notify to the compiler that variable is memory allocated and don't need to allocate again, it is usually used in multi-source file projects \
**static** have 2 meaning: 
* If a variable is declared as global, that variable is only used in that file (multi-source file projects)
* Else if that variable is declared as local in a function (or a class in C++), that variable is memory allocated once until the program ends meaning that the variable will not be destroyed when the function call ends so it will use its last "state" when the function called again

## 1.9. Compilation Model
**Preprocessing**: *preprocessor* will replace preprocessor directives (#) \
**Compiling**: *compiler* will compile code to assembly code (.s/.asm) \
**Assembling**: *assembler* will change assembly code to machine code in object code files(.o) \
**Linking**: *linker* will link object code files together to *shared library* or *executable file* \
A little bit about *preprocessing* and *linking*: *preprocessing* replaces header file (.h) but it usually only contains declarations not definitions and the *linking* link the definitions to these declarations

## 1.10. Static & Shared Library
**Static library** is linked in compile time \
**Shared/Dynamic library** is linked in run time

## 1.11. Function Invoker
When you invoke a function, there are 2 important additional parts called **prologue** and **epilogue** \
`prologue` is the concealed code run before the function is invoked, it is responsible to take the function's parameter to save to *stack* \
`epilogue` is the concealed code run after the function is invoked, it is responsible for returning the function's result to the function invoker and removing the parameter saved to *stack* \
*function*, *prologue* and *epilogue* take the same memory size no matter how many times the function is invoked which means the more you call the function, the more memory is saved \
But there is a paradox in programming that the advantage in memory comes with the disadvantage in speed \
The worst case is the function is too short that is shorter than *prologue*/*epilogue*

## 1.12. Inline Function
**inline** is used to define a macro-like function, meaning that the function's instructions will be replaced directly to its invoke in *preprocessor* step \
This helps improve speed but paying by program size

## 1.13. Dynamic Memory Allocation
As discuss in [**1.3. Memory Layout**](#13-memory-layout) there is a memory layer for *dynamic memory allocation* called heap. So how we manage *dynamic memory allocation* \
There are some keyworks to manage dynamic memory
* **malloc**: dynamically allocates a single large block of memory, returns *void* pointer and has the default garbage value initially. **Syntax**: `ptr = (data-type*)malloc(byte-size)`
* **calloc** like *malloc* but has some differences: dynamically allocates the number of blocks of memory, blocks initialized with default value 0. **Syntax**: `ptr = (data-type*)calloc(size, element-size)`
* **realloc**: dynamically change the memory allocation of a previously allocated memory, maintains the already present value and new blocks will be initialized with the default garbage value. **Syntax**: `ptr = realloc(ptr, new byte-size)`
* **free**: dynamically de-allocate the memory. **Syntax**: `free(ptr)`

# 2. Computer Architect

## 2.1. Von Neumann & Harvard
**Von Neumann** is the computer architect that have intercommunity bus for program memory and data memory \
**Harvard** is the opposite, so it have better performance

## 2.2. Little endian & Big endian
**endian** is a storage mechanism so it is opposite to our thinking \
**Little endian** is from LSB to MSB and **Big endian** is the opposite

## 2.3. Memory Architect
There are two memory types in computer: **volatile** and **non-volatile** \
`volatile` with  representation is `RAM`, also called memory, loses contents when power is off, a temporary workspace for data because it is high-speed \
Some *volatile memory*:
* SRAM or *static RAM*: fast, small capacity, high energy consumption, used for *caches*
* DRAM or *dynamic RAM*: slower than SRAM, higher capacity, requires periodic refresh, used for *main memory*

`non-volatile` with  representation is `ROM`, also called storage, preserves contents when power is off, used to store data \
Some *non-volatile memory* (their name say all about them):
* PROM or *programmable ROM* and MROM or *mask ROM*
* EPROM or *erasable programmable ROM*
* EEPROM or *electrically erasable programmable ROM*

There are also some additional memory types:
* Cache: *SRAM* application
* Flash: erased a "block" at a time, limited number of program/erase cycles 
* Bootloader: on power up, transfers data from non-volatile to volatile memory
* Disk

Memory component speed ordered from fastest to slowest: register, cache, main memory, non-volatile memory, hard-disk drives, optical disk, magnetic tapes

# 3. Embedded

## 3.1. Digital & Analog
Our world is *analog* but computer's world is *digital* \
**analog** refers to a continuously changing representation of a continuously variable quantity \
**digital** refers to representing these variable quantities in terms of actual numbers, or digits \
So we have to do something for computers to understand our world, there will be discuss in [ADC & DAC](#adc--dac) part

## 3.2. Embedded Systems
Embedded system is computer system with a **dedicated function** *embedded* as a part of a complete device and have limited resources as *memory*, *peripheral*, *speed*, ... \
They have some features as: *small size*, *low per-unit cost*, *low power consumption*, ...

## 3.3. Cypher-Physical Systems
### Stay tuned !
This part will be added later

## 3.4. Sensors & Actuators
**Sensors** are devices that measure physical quantities \
`sensor` can be seem as input of a system, it responsible to *"read from physical world"* \
**Actuators** are devices that modify physical quantities \
`actuator` can be seem as output of a system, it responsible to *"write to physical world"* 

## 3.5. Internet of Things
### Stay tuned !
This part will be added later

# 4. Micro-controller

## Micro-processor & Micro-controller
**Micro-processor**: \
**Micro-controller**

## GPIO
**General-Purpose Input/Output Ports**  handles both incoming and outgoing digital signal \
They can be *INPUT* or *OUTPUT*, *LOW* or *HIGH* \
Also, they can be configurated for other functions, called *alternate function* \
`Pull-up resistor` is pulled *HIGH* the GPIO when the button is not pressed and pulled *LOW* the GPIO when the button is pressed \
`Pull-down resistor` is the opposite to *pull-up* \
`Open-drain` make the GPIO can only be *LOW* or *floating*, so we have to use external *pull-up* resistor.

## Interrupt

## Timers

## ADC & DAC
**Analog to Digital Converter** and **Digital to Analog Converter** are very important components in electronic equipments \
*ADC* and *DAC* architect won't be mention here, let's go to their parameters 
* Reference Voltage: 
* Resolution: 
* Quantization: 

## PWM
**Pulse Width Modulation**

## Protocol & Interface
A *protocol* usually come together with that *protocol's interface* so there are many people have ambiguous between *protocol* and *interface*. So, how are they different ? \
`protocol` is a set of rules for devices to communicate with others as *preamble*, *data length*, *conditions*, *crc*, ... and they need to be agreed by all devices \
`interface` is the way devices connect to others as wires, radio waves, ... 

## Some Couple Term In Protocols
**Synchronous** and **Asynchronous**: these are two important term in communication, they imply to *clock*. *Synchronous transmissions* are synchronized by a *clock* and *asynchronous transmissions* are not \
**Wire** and **Wireless**: just *wire* and *wireless* \
**Serial** and **Parallel**: data transmission *serial* or *parallel* (*e.g.* one wire or multi wires) \
**Simplex**, **Half-duplex** and **Full-duplex**: in simplex mode the signal is sent in one direction (only one device can sent data), in half-duplex the signal is sent in both directions but one at a time, in full-duplex signal is sent in both directions at the same time \
**Master** and **Slave**: *master* will be the *clock* controller \
**Server** and **Client**: *client* is requester and *server* serves

## USART
**Universal Synchronous/Asynchronous Receiver-Transmitter** protocol:
* Simplex, Half-duplex, Full-duplex
* Single Master - Single Slave (in UART there is not master and slave, both devices peer)

UART is asynchronous and USART is synchronous, their name said about it \
In UART there are some definitions that must be the same on devices:
* Baudrate: transceive data rate
* Start bit
* Stop bit
* Data frame length: it can be 5, 6, 7 or 8 (even 9 when don't use parity bit)
* Parity bit: used to check data correction. When parity bit = 0 number of bit 1 must be even and when parity bit = 1 number of bit 1 must be odd unless the data is wrong

I have never used USART so I don't have information about it exclude it is synchronous \
In addition, there is another mode called Multiprocessor UART, maybe I will add it later

## I2C
**Inter-Integrated Circuit**, also called **Two Wire Interface** protocol:
* Half-duplex
* Multi Master - Multi Slave
* Synchronous

## SPI
**Serial Peripheral Interface** protocol:
* Full-duplex
* Single Master - Multi Slave
* Synchronous

## CAN 
**Controller Area Network** protocol:


## WiFi


## Bluetooth


## MQTT


## DMA
*Direct Memory Access*

## Bootloader



# 5. Operating System

## 5.1. OS Definition
**Operating System** is software or it can be seem as the intermediate between user and hardware that runs on a computing device and manages the hardware and software components that make up a functional computing system 

## 5.2. OS Functions
Hardware management \
Provide interface for users \
Application installation \
Connect hardware \
Interaction between application and hardware \
CPU scheduling \
Process coordination and synchronization \
Resource management \
Access control and protect system \
Integrity maintenance, error control and recovery

## 5.3. OS Types
Base on processing:
* Uniprogramming OS
* Multiprogramming OS
* Time-sharing OS
* Parallel/multiprocessor/tightly-coupled OS
* Clustered/distributed/loosely-coupled  OS
* RTOS

## 5.4. OS Components
Process/thread management \
Primary memory management \
File management \
I/O system management \
Secondary memory management \
Protect system \
Command line interpreter system 

## 5.5. Process
**Process** is the active *application* instant, *application* become *process* when *executable file* loaded into memory (called *process image*) \
**Process layout** is as same as [Memory Layout In C Program](#13-memory-layout) \
**Process initialization step**: allocate identifier, allocate memory for process load, initialize *Process Control Block* (PCB), setup necessary relation (e.g. arrange PCB to queue) \
**PCB** is one of the most important data structure in OS to manage and control the execution of processes, it typically contains the following components:
* ***Process ID*** (PID): unique identifier assigned to each process by the operating system
* ***Program counter*** (PC): address of the next instruction to be executed by the process
* ***Process state***: current state of the process, includes new, ready, running, waiting, terminated, suspended
* ***CPU registers***: values of the processor registers that are being used by the process
* ***Memory management information***: information about the process’s memory allocation, such as the base and limit registers
* ***I/O status information***: information about the process's I/O operations, such as open files and network connections 
* ***Accounting information***: information about the resources used by the process, such as CPU time and memory usage
* ***CPU scheduling information***: information about the process’s priority and scheduling requirements

**Thread** is a segment of a process or a lightweight process, threads share memory, data, resources together \
There are 3 *thread mapping model*
* Multi user thread mapping to single kernel thread: any user thread blocked cause all user thread blocked, user threads can't run parallel because only one user thread can use kernel at one time
* Single user thread mapping to single kernel thread: create a user thread also create a kernel thread, better concurrency because any user thread blocked don't affect to other threads, limited number of threads
* Multi user thread mapping to multi kernel threads: solve the disavantages of the two below but hard to setting

## OS Scheduling
**Scheduling in OS** is **process scheduling** with PCB: *process scheduling* is a crucial function in OS and PCB in OS plays a vital role in this function \
**Scheduler** include several types:
* **Long-term scheduler** used to schedule *job* (or *process*), decide which program accepted to load into system to run, control system's multiprogramming, maintain both CPU-bound and I/O-bound process
* **Short-term scheduler** used to schedule CPU, decide which process in ready queue will take CPU to run next, trigger events: clock interrupt, I/O interrupt, OS call, signal, ...
* **Mid-term scheduler** (in time-sharing system) used to adjust system's multiprogramming (swap in - move process from memory to disk and swap out - move process from disk to memory)
*Scheduler* will change the CPU control permit for the choosen process, includes:
* Context change 
* User mode change
* Jump to the position in process to running proccess again
*Scheduling* cause time consumption called dispatch latency, time that scheduler stop current process and start another process
**Scheduling criteria** 
* User-oriented: response time - time since process receive request to first request is responsed (time-sharing, interactive system) minimum, turnaround time: time since process loaded into system to process terminated minimum, waiting time: sum of process waiting time in ready queue minumum
* System-oriented: process utilization - schedule to make the CPU busiest maximum, fairness - all process treated peer, throughput - number of done process in a time maximum
**Scheduling features**
* Selection function: used to choose which process in ready queue run usually based on priority, resources request, process 
* Desicion mode: used to choose time to choose selection function for scheduling, there are two desicion mode: non-preemptive - when running process will run until end or blocked by I/O request and preemtive - running process can be interrupt to ready state, more cost but more better response time because no case that a process take CPU too long
**service time** is the time process need CPU in a CPU-I/O period, processes have large service time are CPU-bound processes

## Scheduling algorimth

# 6. RTOS

## Stay tuned !

# 7. Linux Embedded

## Stay tuned !

# Undistributed

These parts will be completed or distributed soon

<br> [<kbd> <br> FEEDBACK <br> </kbd>][FEEDBACK] 
 [<kbd> <br> EMAIL <br> </kbd>][EMAIL] <br>

[ABOUT_US]: about-us/about-us.md
[FEEDBACK]: https://github.com/memeowteam/Notebook/discussions
[EMAIL]: mailto:memeowteam@gmail.com
