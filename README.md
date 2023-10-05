# Embedded Notebook
Nothing, just Mike and Johnny
# Table of contents
- [Table of contents](#table-of-contents)
- [About us](/about-us/about-us.md)
- [Introduce](#introduce)
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
- [C++](C++/C++.md)
- [Python](Python/Python.md)
- [2. Computer Architect](#2-computer-architect)
  - [2.1. Von Neumann & Harvard](#21-von-neumann--harvard)
  - [2.2. Little endian & Big endian](#22-little-endian--big-endian)
- [3. Embedded](#3-embedded)
  - [3.1. Digital & Analog World](#31-digital--analog-world)
  - [3.2. Embedded Systems](#32-embedded-systems)
  - [3.3. Cypher-Physical Systems](#33-cypher-physical-systems)
  - [3.4. Sensors & Actuators](#34-sensors--actuators)
  - [3.5. Internet of Things](#35-internet-of-things)
- [4. Operating System](#4-operating-system)
- [5. RTOS](#5-rtos)
- [Robot Operating System](ROS/ROS.md)
- [6. Linux Embedded](#6-linux-embedded)
- [Available soon](#undistributed) 

# Introduce
Some words about this notebook: 
## Because two people are contributing to this notebook, there are differences in styles 
**Mike's articles** written as if you have already known the basic and the knowledge only remind but not clearly for you to understand from zero
## Some huge parts will be separated to another files
**C++** \
**Python** \
**Robot Operating System** 
## We are not familiar with web applications so our GitHub Webpage is for fun, our main target is knowledge
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
type-qualifier(s) type-modifier data-type variable-name = initial-value; \
`type-qualifier`: *const*, *volatile*, *restrict* \
`type-modifier`: *short*, *long*, *unsigned*, *signed* \
`data-type`: *interger* (int), *floating point* (double, float), *enumerated*, *derived* (array, struct, union, pointer), *void* 

## 1.3. Memory Layout
**Memory layout** from low to high addresses in C includes: 
* **text segment** (code segment): executable instructions - sharable & read-only
* **initialized data**: global variables, static variables initialized (declared $\neq$ 0)
* **uninitialized data**: global variables, static variables uninitialized or initialized to 0
* **heap**: dynamic memory allocation (forget deallocation cause **Memory leak**)
* **stack**: automatic variable storage, function frame (runout of *stack memory* cause **Stack overflow**)

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
In C, we don't have reference parameter so we can use *pointer* to subtitute

## 1.6. Function pointer:
**function pointer** is a pointer to const because function address place on *code segment* which is *read-only* \
*syntax*: data-type (*function-name)(parameter) \
e.g. `void (*pointer_function)()`: pointer function point to a function with no parameter and return void

## 1.7. Struct & Union & Enum
**struct**, **union** and **enum** are user-define data types \
**struct** is used to group related variables (members) into one  
`struct in C` need to use *typedef* to don't use *struct* keyword whenever declare a new *struct variable*. In C++, it is not neccessary \
**union** allows to store different data types to same memory     \
**enum** is usually used to assign name to integral constants \
`data structure alignment` is the term that means compiler "padding" into space between 2 data "naturally aligned", this mechanism help compiler better performance. We should arrange data in *struct* reasonable to optimize memory and performance

## 1.8. Extern & Static
**extern** is used to notify to the compiler that variable is memory allocated and don't need to allocate again, it is usually used in multi-source file projects \
**static** have 2 meaning: 
* If a variable is declared as global, that variable is only used in that file (multi-source file projects)
* Else if that variable is declared as local in a function (or a class in C++), that variable is memory allocated once until the program ends meaning that the variable will not be destroyed when the function call ends so it will use its last "state" when the function called again

## 1.9. Compilation Model
**Preprocessor** will replace preprocessor directives (#) \
**Compiler** will compile code to assembly code (.s/.asm) \
**Assembler** will change assembly code to machine code in object code files(.o) \
**Linker** will link object code files together to *shared library* or *executable file* \
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

# 2. Computer Architect

## 2.1. Von Neumann & Harvard
**Von Neumann** is the computer architect that have intercommunity bus for program memory and data memory \
**Harvard** is reverse, so it have better performance

## 2.2. Little endian & Big endian
**endian** is a storage mechanism so it is opposite to our thinking \
**Little endian** is from LSB to MSB and **Big endian** is reversed

## 2.3. Memory Architect
There are two memory types in computer: **volatile** and **non-volatile** \
`volatile` with  representation is `RAM`, also called memory, loses contents when power is off, a temporary workspace for data because it is high-speed \
Some *volatile memory*:
* SRAM or *static RAM*: fast, small capacity, high energy consumption, used for *caches*
* DRAM or *dynamic RAM*: slower than SRAM, higher capacity, requires periodic refresh, used for *main memory*

`non-volatile` with  representation is `ROM`, also called storage, preserves contents when power is off, used to store data \
Some *non-volatile memory* (their name say all about them):
* PROM or *programmable ROM* & MROM or *mask ROM*
* EPROM or *erasable programmable ROM*
* EEPROM or *electrically erasable programmable ROM*

There are also some additional memory types:
* Cache: *SRAM* application
* Flash: erased a "block" at a time, limited number of program/erase cycles 
* Bootloader: on power up, transfers data from non-volatile to volatile memory
* Disk

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

# 4. Operating System

## Stay tuned !

# 5. RTOS

## Stay tuned !

# 6. Linux Embedded

## Stay tuned !

# Undistributed

These parts will be completed soon

## GPIO
## Interrupt
## ADC & DAC
## PWM
## USART
## I2C
## SPI
## CAN 
## WiFi
## Bluetooth
## MQTT
## DMA
## Bootloader


<!-- 
  - [2.3. Memory Types](#23-memory-types)
  - [GPIO](#gpio)
  - [Interrupt](#interrupt)
  - [ADC & DAC](#adc--dac)
  - [PWM](#pwm)
  - [USART](#usart)
  - [I2C](#i2c)
  - [SPI](#spi)
  - [CAN](#can)
  - [WiFi](#wifi)
  - [Bluetooth](#bluetooth)
  - [MQTT](#mqtt)
-->