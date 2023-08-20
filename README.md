# Physical Design for ASICs

<img width="503" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/7846569a-39e8-497d-9242-2a38cf3de04a">

# Introduction
**VLSI physical design for ASIC** is the process of converting a conceptual chip design into a physical layout suitable for manufacturing. It encompasses tasks such as arranging components, optimizing connections, managing power and clock distribution, addressing manufacturing challenges, and ensuring design compliance. This meticulous process guarantees a functional and manufacturable integrated circuit tailored to specific applications.

# System requirments
- Ubuntu 20+
- RAM : 6Gb (minimum)
- Disk space : 100Gb (minimum)
  
# Installation
https://github.com/kunalg123/riscv_workshop_collaterals/blob/master/run.sh
- Download the run.sh
- Open terminal
- cd Downloads
- ./run.sh
  
# CONTENTS
<details>
<summary>DAY 1</summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigation)
## DAY 1
**Introduction to RISCV ISA and GNU Compiler Toolchain**
+ Introduction to RISC-V Basic Keywords
  - [Introduction](#introduction)
  - [From Apps to Hardware](#from-apps-to-hardware)
  - [Detail Description of Course Content](#detail-description-of-course-content)

+ Labwork for RISC-V Toolchain
  - [C Program](#c-program)
  - [RISCV GCC Compiler and Dissemble](#riscv-gcc-compiler-and-dissemble)
  - [Spike Simulation and Debug](#spike-simulation-and-debug)

+ Integer Number Representation  
  - [64-bit Unsigned Numbers](#64-bit-unsigned-numbers)
  - [64-bit Signed Numbers](#64-bit-signed-numbers)
  - [Lab For Signed and Unsigned Numbers](#lab-for-signed-and-unsigned-numbers)


# DAY 1    
 
# Introduction to RISc-V Basic Keywords
## Introduction
RISC-V Architecture -> RTL -> Layout

## From Apps to Hardware
## Flow
+ Application Software 
+ System Software
  - Operating System
  - Complier
  - Assembler
+ Hardware
<img width="502" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/eb287951-3c15-4b47-b5fe-1f471c84fe14">

## Detail Description of Course Content
- Pseudo Instructions
- Base integer Instructions RV641
- Multiply extension RV64M
- Single and double precision floating point extension RV64F & RV64D
- Application binary interface (ABI)
- Memory allocation and stack pointer

# Labwork for RISC-V Toolchain
## C Program
- Text editor used : leafpad
- To install leafpad in ubuntu : `sudo snap install leafpad`

## C program for sum from 1 to N
`leafpad sum1ton.c` : creates a text file called sum1ton.c
``` c
#include<stdio.h>

int main(){
	int i, sum=0, n=10;
	for (i=1;i<=n; ++i) {
	sum +=i;
	}
	printf("Sum of numbers from 1 to %d is %d \n",n,sum);
	return 0;
}
```
Compile using gcc complier
`gcc sum1ton.c`
`./a.out`

<img width="502" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/bcec2cbb-9a78-441d-84d6-f341d2645825">

## RISCV GCC Compiler and Dissemble
Compile using RISC-V gcc complier
- using -O1 optimisation
```
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
riscv64-unknown-elf-objdump -d sum1ton.o
```
Number of instructions = 15
<img width="502" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/242d83e5-c7c4-47cf-aa04-2c3db3373bd2">
- using -Ofast optimisation
```
riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
riscv64-unknown-elf-objdump -d sum1ton.o
```
Number of instructions = 12
<img width="502" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/b772a095-3460-4396-aba4-5c86296b4c34">

`riscv64-unknown-elf-objdump -d sum1ton.o` : gives the disassembled (Assembly Language Programming )ALP code

## Spike Simulation and Debug
`spike pk sum1ton.o` : To Verify the simulations using RISC-V complier

<img width="502" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/cdf11383-ad59-47e8-8007-abc80cd560ce">

`spike -d pk sum1ton.c ` :To debug

<img width="502" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/99241fdb-3988-4a42-b9f5-853648bd595d">

# Integer Number Representation 
+ 8-bits -> byte, 4-bytes -> word, 2-words or 8-bytes -> doubleword
## 64-bit Unsigned Numbers
- A 64-bit unsigned number can represent non-negative integer values using 64 bits, with no sign bit to indicate whether the number is positive or negative.
- Range: [0, (2^n)-1 ]

## 64-bit Signed Numbers
- A 64-bit signed number can represent both positive and negative integer values using 64 bits. The first bit, often referred to as the "sign bit," indicates whether the number is positive or negative.
- Range : Positive : [0 , 2^(n-1)-1] Negative : [-1 to 2^(n-1)]

## Lab For Signed and Unsigned Numbers
+ C program that shows the maximum and minimum values of 64bit unsigned numbers
```c
#include <stdio.h>
#include <math.h>

int main(){
	unsigned long long int max = (unsigned long long int) (pow(2,64) -1);
	unsigned long long int min = (unsigned long long int) (pow(2,64) *(-1));
	printf("lowest number represented by unsigned 64-bit integer is %llu\n",min);
	printf("highest number represented by unsigned 64-bit integer is %llu\n",max);
	return 0;
}
```

<img width="502" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/f0c93d75-c326-42ec-b3de-e1290c23b192">

+ C program that shows the maximum and minimum values of 64bit signed numbers
  
```c
#include <stdio.h>
#include <math.h>

int main(){
	long long int max = (long long int) (pow(2,63) -1);
	long long int min = (long long int) (pow(2,63) *(-1));
	printf("lowest number represented by signed 64-bit integer is %lld\n",min);
	printf("highest number represented by signed 64-bit integer is %lld\n",max);
	return 0;
}
```

<img width="502" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/7fef9481-74ef-4fcb-8462-eb0a7dc40cd9">

</details>

<details>
<summary>DAY 2 </summary>
<br>

[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigation)
# DAY 2


## DAY 2 
**Introduction to ABI and Basic Verification Flow**
+ Application Binary Interface
  - [Introduction to ABI](#introduction-to-abi)
  - [Memory Allocation for Double Words](#memory-allocation-for-double-words)
  - [Load, add and store instructions](#load-add-and-store-instructions)
  - [32-Registers and their ABI Names](#32-registers-and-their-abi-names)

+ Labwork using ABI Function Calls
  - [Algorithm for C Program using ASM](#algorithm-for-c-program-using-asm)
  - [Review ASM Function Calls](#review-asm-function-calls)
  - [Simulate C Program using Function Call](#simulate-c-program-using-function-call)

# Application Binary Interface

## Introduction to ABI
+ Base Binary Instructions
  - Base integer instructions refer to the fundamental set of instructions that operate on integer data in a computer's instruction set architecture (ISA)
  - These are arithmetic, logical, Comparison, Data Movement, Control Flow performing operations
+ Application Binary Interface (ABI)
  - An Application Binary Interface (ABI) serves as a crucial bridge between the software and hardware components of a computer system.
  - ABIs enable software components to seamlessly communicate and collaborate, even across diverse programming languages, compilers, and hardware architectures.
<img width="600" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/e25eba01-5478-4113-b402-e96d3da1ba9d"> 

## Memory Allocation for Double Words
- RISC-V has **32** registers
  - 32 bits for RV32
  - 64 bits for RV64

- Memory addressing system
  - **Little-Endian** (Risc-V belongs to little-endian)
  - **Big-Endian**
  
<img width="650" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/76ab920b-3abd-4085-b1b7-96e40af4945b"> 

## Load, add and store instructions
Load, Add, and Store instructions are often used to manipulate data within a computer's memory and registers.
1. **Load Instructions:**
Load instructions are used to transfer data from memory to registers. They allow you to fetch data from a specified memory address and place it into a register for further processing.

Example `ld x6, 8(x5)`

In this Example
- `ld` is the load double-word instruction.
- `x6` is the destination register.
- `8(x5)` is the memory address pointed to by register `x5` (base address + offset).
2. **Store Instructions:**
Store instructions are used to write data from registers into memory.They store values from registers into memory addresses

Example `sd x8, 8(x9)`

In this Example
- `sd` is the store double-word instruction.
- `x8` is the source register.
- `8(x9)` is the memory address pointed to by register `x9` (base address + offset).
3. Add Instructions:
  Add instructions are used to perform addition operations on registers. They add the values of two source registers and store the result in a destination register.

Example `add x9, x10, x11`

In this Example
- `add` is the add instruction.
- `x9` is the destination register.
- `x10` and `x11` are the source registers.

<img width="750" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/9df00634-f508-4c5f-9e55-86d4bf03be9f"> 

## 32-Registers and their ABI Names
The ABI names provide meaningful and consistent labels to the registers, which simplifies understanding their roles in function calls, data manipulation, and other operations.

<img width="350" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/320a926d-6867-4803-bb13-4abcecbe1467"> 

# Labwork using ABI Function Calls
## Algorithm for C Program using ASM
- This allows you to take advantage of assembly language's low-level control and optimizations while still benefiting from C's higher-level constructs.
- When you call an assembly function from your C code, the C calling convention is followed, including pushing arguments onto the stack or passing them in registers as required.
- The program executes the assembly function, following the assembly instructions you've provided.

## Review ASM Function Calls
- C code and assembly code are written in separate files
- Declaring assembly functions with appropriate signatures that match the calling conventions of your platform in assembly file
 
**C Program**
  
  `1to9custom.c`
  
  ``` c
  #include <stdio.h>
  
  extern int load(int x, int y);
  
  int main()
  {
    int result = 0;
    int count = 9;
    result = load(0x0, count+1);
    printf("Sum of numbers from 1 to 9 is %d\n", result);
  }
  ```
**Asseembly File**

`load.s`

``` s
.section .text
.global load
.type load, @function

load:

add a4, a0, zero
add a2, a0, a1
add a3, a0, zero

loop:

add a4, a3, a4
addi a3, a3, 1
blt a3, a2, loop
add a0, a4, zero
ret
```
## Simulate C Program using Function Call

Compile and execute the files 

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/87bb8d8a-1ce6-4631-8fcf-65116d2e32f7"> 

Disassemble the code 

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/038da5c5-6402-4e90-825c-9c8548353a95">

</details>













  
