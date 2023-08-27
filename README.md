# Physical Design for ASICs

<img width="1100" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/2e4c7a2d-b188-403d-9482-a8efac7ceada">



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
<summary> Introduction to RISCV ISA and GNU Compiler Toolchain </summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)
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
<summary> Introduction to ABI and Basic Verification Flow </summary>
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


## Lab to Run C-Program on RISCV-CPU

```
git clone https://github.com/kunalg123/riscv_workshop_collaterals.git
```

```
cd riscv_workshop_collaterals
```

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/2904e4cc-c126-4e06-9b12-4a04ca31ab88">


```
ls -ltr
```

```
cd labs
```

```
ls -ltr
```

```
chmod 777 rv32im.sh
```

```
./rv32im.sh
```

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/3c9bb5d2-0247-436e-a666-c45148e03752">

</details>

<details>
<summary> RTL Design using verilog with SKY130 technology </summary>
<br>

[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)
## Day 1
<details>
<summary> Introduction to Verilog RTL design and Synthesis</summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)



<details>
<summary> Introduction to open-source simulator iverilog </summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)

## Introduction to open-source simulator iverilog
**Introduction to iverilog design test bench**

- **Simulator**
  + Simulators create virtual models of systems, enabling analysis and testing of behaviors without real-world implementation
  + Simulators is the tool used for simulating the design
  + The simulator runs the model using the provided inputs. It calculates the system's behavior over time and produces output data upon change in input (if no change to the input, no change to the output)
  + **iverilog** is the tool used here
     + Icarus Verilog (iverilog) is an open-source simulator for hardware description languages like Verilog, enabling design, simulation, and testing of digital circuits
     + It's used to model and validate digital systems before physical implementation

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/a1fe7cb8-41e6-423c-a986-b4f2fd1308f6">

- **Design**
  + Design is the actual verilog code or set of verilog codes which has the intended functionality to meet with the required specifications
  
- **TestBench**
  + It involves creating a set of test cases and stimuli to apply to the design and then comparing the design's outputs with expected results.
  + Test benches are written using hardware description languages like Verilog or VHDL
  + This verification process is crucial for building reliable and bug-free digital systems
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/3c3fd20b-e3bb-4c9f-b3b7-41593c3356ea">  

</details>


<details>
<summary> Labs using iverilog and gtkwave </summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)


## Labs using iverilog and gtkwave

**Icarus Verilog** simulates the design and generates simulation output files, and **GTKWave** then allows you to visually inspect and analyze the simulation results in waveform format

- [Introduction to lab (Lab1)](#introduction-to-lab-lab1)
- [iverilog GTKwave Part-1 (Lab2)](#iverilog-gtkwave-part-1-lab2)
- [iverilog GTKwave Part-2 (Lab2)](#iverilog-gtkwave-part-2-lab2)

## Introduction to lab (Lab1)
- Environment setup !!!
+ create a directory ` mkdir vsd `
+ change directory ` cd vsd `
+ Git clonning ` git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git`
   + `sky130RTLDesignAndSynthesisWorkshop` folder will be created

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/5eeabad8-63c7-4a6a-aaa9-5b1bd4b10139"> 

## iverilog GTKwave Part-1 (Lab2)
+ ` cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
    + loads verilog source files and associated testbench files into iverilog simulator
    + verilog_files : this folder contains all design files
+ `iverilog good_mux.v tb_good_mux.v` loads mux into the simulator
+ output file `a.out` will be created
+ Execute a.out `./a.out` to dump the vcd file (output of simulator)
+ To load vcd file into simulator ` gtkwave tb_good_mux.vcd`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/c6d25681-de8d-449c-a270-bfd454f15e4a"> 

## iverilog GTKwave Part-2 (Lab2)
`gvim tb_good_mux.v -o good_mux.v` to view the files


**good_mux.v**

``` v
module good_mux (input i0 , input i1 , input sel , output reg y);
always @ (*)
begin
	if(sel)
		y <= i1;
	else 
		y <= i0;
end
endmodule
```
**tb_good_mux.v**

``` v
timescale 1ns / 1ps
module tb_good_mux;
	// Inputs
	reg i0,i1,sel;
	// Outputs
	wire y;

        // Instantiate the Unit Under Test (UUT)
	good_mux uut (
		.sel(sel),
		.i0(i0),
		.i1(i1),
		.y(y)
	);

	initial begin
	$dumpfile("tb_good_mux.vcd");
	$dumpvars(0,tb_good_mux);
	// Initialize Inputs
	sel = 0;
	i0 = 0;
	i1 = 0;
	#300 $finish;
	end

always #75 sel = ~sel;
always #10 i0 = ~i0;
always #55 i1 = ~i1;
endmodule
```

    

</details>


<details>
<summary> Introduction to Yosys and Logic synthesis </summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)


## Introduction to Yosys and Logic synthesis

- [Introduction to Yosys](#introduction-to-yosys)
- [Introduction to Logic synthesis)](#introduction-to-logic-synthesis)


## Introduction to Yosys
- **Synthesizer**
   + Synthesizeris a tool used for converting the RTL to netlist
   + **Yosys** is the synthesizer used in the course
      + Yosys is an open-source synthesis tool that translates hardware description language (HDL) code into gate-level netlists, optimizing designs for efficient hardware implementation.
- **Netlist**
  + Netlist is the representation of the design in the form of standard cells in the .lib
  + Design and .lib files are fed to the synthesizer to get a netlist file
 
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/56f8289c-4737-481e-9bb3-2b86f38a6902"> 

+ Commands used to perform synthesis:
  - To read the design :  `read_verilog` 
  - To read the .lib file : `read_liberty` 
  - To write out the netlist file : `write_verilog` 
 
- Verify the synthesis
 
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/63bd1f15-ec42-47e3-b2d6-e76ee3ebe6d9"> 

   - The output on the simulator must be same as the output observed during RTL simulation.
   - Same RTL testbench can be used because the primary inputs and primary outputs remain same between the RTL design and synthesised netlist.

## Introduction to Logic synthesis

- **RTL design**
  + Behavioral representation of the required specification
  + RTL (Register-Transfer Level) forms a bridge between behavioral descriptions and gate-level implementation.

- **Synthesis**
  + RTL to gate level translation
  + The design is coverted into dates and the connections are made between the gates
  + This is given out as a file called netlist
    
<img width="350" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/dd91792a-9e4b-4c6e-ac62-55cd19486580)"> 

- **.lib**
   + Collection of logical modules
   + Includes basic logic gates like AND, OR, NOT, etc
   + Different flavors of same gate , **WHY ??**
       + These variations are designed to accommodate specific design requirements, process technologies, and performance goals
       + Clock frquency should be high, Hence time period of the clock should be  as low as possible
         
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/5030de94-2f5a-4ea4-952d-2d3ffb04c9f5"> 

- What is maximum clock rate ? tclk ?
	+ Propogation delay of Flop A
	+ Propogational delay of combinational circuit
	+ Time before clock edge, setup time
- So we need cells that work fast to make Tcombi samall
- Are faster cells sufficient ??
   + NO
- Why do we need slow cells ?
  
<img width="150" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/2c4cf856-de06-4d1d-96e3-c7f072b448f2"> 

   + To ensure that there are no "HOLD" issues at DFF_B, we need slow cells
   + Hence we need cells that work fast to meet the required performance and we need cells that work slow to meet HOLD
   **Hence the collection forms the .lib!!!**
     
**Faster cells vs Slower cells**
- Load in degital circuit -> Capacitance
- Faster the charging/discharging of capacitance -> Lesser the cell delay
    + To charge/discharge the capacitance fast, we need transistors capable of sourcing more current ( Wide Transistors)
    + Wider transistors -> Low Delay -> More area and power as well
    + Narrow transistors -> More Delay -> Less area and power
-Faster cells come at the penalty of area and power

**Selction of cells**
Synthesizer should be guided to select the flavour of cells that is optimum for the implementation of logic circuit. Guidance offered -> "Constaints"


<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/b4119c84-db5f-4751-acfd-72c81fe4b3d6">

 </details>

 
<details>
<summary> Labs using Yosys and Sky130 PDKs</summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)
## Labs using Yosys and Sky130 PDKs 
-[Yosys good mux (Lab3)](#yosys-good-mux-lab3)

 The SkyWater Technology Foundry's **SKY130 Process Design Kit (PDK)** is a collection of files, data, and models that enable the design and layout of integrated circuits using the SkyWater 130 nm technology node. PDKs provide designers with the necessary tools and information to create, simulate, and verify custom and digital designs that can be manufactured using the specific technology offered by the foundry. 
 
## Yosys good mux (Lab3)
- To invoke the Yosys : `yosys`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/eaa3287e-b5b6-4597-b29a-d8651c4839f6">

- To read the library : ` read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
- To read the design : `read_verilog good_mux.v`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/3953ff06-69ed-48b0-a966-39ff5fa2b560">

- To synthesis the mosule : `synth -top good_mux`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/6309e60b-1c8c-467b-ad52-e550bc305daf">

- To generate the netlist : `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/c948cd72-9e64-4bd9-a102-4f98112eab3b">

- To see the logic it has realised `show`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/30e2335a-7f17-4eef-b203-804640eb62d5">

- To write the netlist : 'write_verilog good_mux_netlist.v`
- ` !gvim good_mux_netlist.v`
-  To view a simplified code : ` write_verilog -noattr good_mux_netlist.v`
-  `!gvim good_mux_netlist.v`
  
</details>
</details>  

## Day 2
<details>
<summary> Timing libs, hierarchical vs flat synthesis and efficient flop coding styles</summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)

<details>
<summary> Introduction to timing.libs </summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)

## Introduction to timing.libs (Lab4)
**Introduction to dot Lib**
+ To view the contents in the .lib
`gvim ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`


<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/bcdd2944-4944-499b-99c8-9400c084a9b2">


- To have a pleasant color : `:syn off` (syntax off)
    - NOTE: Don't edit this file
- **sky130** : Name of the library
- **tt**     : Typical process
- **025C**   : Temperature variation
- **P V T**  : Operating conditions (Process Voltage Temperature)
    - Together determines how the silicon works
- **1v80**   : Voltage levels variation

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/f49ac9c0-7677-40e3-9456-46bd9c75c756">

- Displays the units of parameters
- Contains area and power consumpution
- .lib is a Bucket of all the standard cells
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/267ed2ae-d9e9-49dc-9039-7c02215dfb99">


- To enable line number `:se nu`
- To view all the cells `:g//`
- To view any instance `:/instance`
- Can compare and analyse the parameters

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/47cabe0a-eee7-40e9-9357-b1871e47fa46">


 </details>     


<details>
<summary> Hierarchical vs Flat synthesis </summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)
## Hierarchical vs Flat synthesis (Lab5)

## Hierarchical Synthesis
**Hierarchical synthesis involves breaking down a complex design into smaller modules for separate synthesis and integration. This approach enhances modularity, enables parallel development, and simplifies verification, making it ideal for large designs.**

- File used : 'multiple_modules.v`
- To view : `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
- and `gvim multiple_modules.v`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/d6816017-c0f4-48e9-8c92-1bf8c99ddeb6">


- It contains 2 submodules : `sub_module1` -> AND gate and `sub_module2`->OR gate
- `mutiple_module` instantiates them as `u1` and `u2` respectively
  
+  Frist Launch Yosys     : `yosys`
+  Read the library file  : `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+  Read the verilog file  : `read_verilog multiple_modules.v`
+  To set it as top module: `synth -top multiple_modules`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/cc297050-dc6e-4469-90d8-3ac600194370">

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/a9495611-658d-489f-bf39-b9e6546a524e">


+  `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ To view the netlist    :`show multiple_modules`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/8740c0be-8439-4b75-9c4f-a81cc0a8a26c">

+ `sub_module1` and `sub_module2` are shown instead of AND gate and OR gate.
+ To view : `write_verilog -noattr multiple_modules_hier.v`
+ `!gvim multiple_modules_hier.v`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/fd066807-4c8b-4bc6-95fb-6b8976185214">

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/e1c470a9-0747-4c7d-a4ca-47f405231908">



## Flat Synthesis
**Flat synthesis treats the entire design as a single unit, synthesizing it as one entity. While simpler for smaller designs, it can become unwieldy for larger projects, leading to longer synthesis times and reduced reusability of modules.**

+  Launch  : `yosys`
+  Read the library file :   `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+  Read the verilog file : ` read_verilog multiple_modules.v`
+  To set it as top module: `synth -top multiple_modules` 
+  `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `flatten` to write out a flattened netlist
+ `show` to view the netlist

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/7dffcc47-5ed6-40d6-b48e-08d156f95f34">

+ `write_verilog -noattr multiple_modules_flat.v`
+ `!gvim multiple_modules_flat.v`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/1e708f33-455c-40bf-a7d0-710e6ac6b174">

**Why sub module level synthesis**
- U seful when we have multiple instances of same module
- Divide and Conquer
- Helpful when circuits are massive
-`synth -top module_name` controls which module to synthesis
 </details>     


<details>
<summary>Various Flop Coding Styles and optimization</summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)
   
## Various Flop Coding Styles and optimization
- [Why flops and Flop coding styles](#why-flops-and-flop-coding-styles)
- [Lab flop synthesis simulations](#lab-flop-synthesis-simulations)
- [Interesting Optimisations](#interesting-optimisations)
  
## Why flops and Flop coding styles


## Lab flop synthesis simulations
## Interesting Optimisations
 
</details> 
</details>   

## Day 3
<details>
<summary> Combinational and sequential optmizations </summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)


<details>
<summary> Introduction to optimisations</summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)
+ Introduction to optimisations

</details> 
<details>
<summary> Combinational logic optimizations </summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)
## Combinational logic optimizations (Lab6)


</details> 
<details>
<summary> Sequential logic optimizations </summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)

## Sequential logic optimizations (Lab7)
 
</details> 
<details>
<summary>  Sequential optimizations for unused outputs  </summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)

## Sequential optimizations for unused outputs    

</details> 
</details>  

## Day 4
<details>
<summary> GLS, blocking vs non-blocking and Synthesis-Simulation mismatch</summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)

+ GLS, synthesis-Simulation mismatch and Blocking/Non-blocking statements
   + GLS concepts and flow using iverilog
   + synthesis-Simulation mismatch
   + Blocking and Non-blocking statements in verilog
   + Caveats with blocking statements
+ Labs on GLS and Synthesis-Simulation Mismatch
   + part1
   + part2
+ Labs on synth-sim mismatch for blocking statement
   + part1
   + part2

  
</details>   
  
</details>                    





  
