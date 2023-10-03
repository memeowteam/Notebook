# Embedded Notebook
Nothing, just Mike and Johnny
# Table of contents
- [Table of contents](#table-of-contents)
- [About us](/about-us/about-us.md)
- [Introduce](#introduce)
- [1. C/C++](#1-cc)
  - [1.1. C keywords](#11-c-keywords)
  - [1.2. Variables declaration](#12-variables-declaration)
  - [1.3. Volatile keyword](#13-volatile-keyword)
  - [1.4. Pointer](#14-pointer)
  - [1.5. Function pointer](#15-function-pointer)
  - [1.6. Struct & Union & Enum](#16-struct--union--enum)
  - [1.7. Extern & Static](#17-extern--static)
- [2. Computer Architect](#2-computer-architect)
  - [2.1. Von Neumann & Harvard](#21-von-neumann--harvard)
  - [2.2. Little endian & Big endian](#22-little-endian--big-endian)
- [3. Embedded](#3-embedded)
- [4. Operating System](#4-operating-system)
- [5. RTOS](#5-rtos)
- [6. Linux Embedded](#6-linux-embedded)
# Introduce
Some words about this notebook: because two people are contributing to this notebook, there are differences in styles \
**Mike's articles** written as if you have already known the basic and the knowledge only remind but not clearly for you to understand from zero
# 1. C/C++

## 1.1. C keywords
|           |           |           |           |
| :---:     | :---:     |  :---:    | :---:     |
| auto	    | double	  | int	      | struct    |
| break	    | else	    | long	    | switch    |
| case	    | enum	    | register	| typedef   |
| char	    | extern	  | return	  | union     |
| continue	| for	      | signed	  | void      |
| do	      | if	      | static	  | while     |
| default	  | goto	    | sizeof	  | volatile  |
| const	    | float	    | short	    | unsigned  |

## 1.2. Variables declaration
type-qualifier(s) type-modifier data-type variable-name = initial-value; \
`type-qualifier`: *const*, *volatile*, *restrict* \
`type-modifier`: *short*, *long*, *unsigned*, *signed* \
`data-type`: *interger*(int), *floating point*(double, float), *enumerated*, *derived*, *void* 

## 1.3. Volatile keyword
**volatile**: used to indicate to the compiler that a variable's value may change unexpectedly. *volatile* is usually used when you turn on compiler's optimization function 
* Peripheral register mapping to memory 
* Interrupt Service Routines (ISRs) 
* Multi-thread applications

**const volatile**: same as volatile but you can't change its value by the code

## 1.4. Pointer:
**pointer** is variables that hold address \
*pointer* point to any type have same size \
In C, we don't have reference parameter so we can use *pointer* to subtitute

## 1.5. Function pointer:
**function pointer** is a pointer to const because function address place on *code segment* which *read-only* \
*syntax*: data-type (*function-name)(parameter) \
*e.g.* `void (*pointer_function)()`: pointer function point to a function with no parameter return void

## 1.6. Struct & Union & Enum
**struct**, **union** and **enum** are user-define data types \
**struct** is used to group related variables (members) into one  
`struct in C` need to use *typedef* to don't use *struct* keyword whenever declare a new *struct variable*. In C++, it is not neccessary \
**union** allows to store different data types to same memory     \
**enum** is usually used to assign name to integral constants \
`data structure alignment` is the term that means compiler "padding" into space between 2 data "naturally aligned", this mechanism help compiler better performance. We should arrange data in *struct* reasonable to optimize memory and performance

## 1.7. Extern & Static
**extern** is used to notify to the compiler that variable is memory allocated and don't need to allocate again, it is usually used in multi source file projects \
**static** have 2 meaning: 
* If variable is declared as global, that variable is only used in that file (multi source file projects)
* Else if variable is declared as local in a function (or a class in C++), that varible is memory allocated once until the program end meaning that variable will not be destroyed when the function call end so it will use it last "state" when the function call again
# 2. Computer Architect
## 2.1. Von Neumann & Harvard
**Von Neumann** is the computer architect that have intercommunity bus for program memory and data memory \
**Harvard**  is reverse, so it have better performance
## 2.2. Little endian & Big endian
**endian** is a storage mechanism so it is opposite to our thinking \
**Little endian** is from LSB to MSB and **Big endian** is reverse
# 3. Embedded
## Stay tuned !
# 4. Operating system
## Stay tuned !
# 5. RTOS
## Stay tuned !
# 6. Linux Embedded
## Stay tuned !