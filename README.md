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
## Day 3
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

## Day 4
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
**What are flops??**
- Flip-flops, often referred to as "flops," are fundamental building blocks in digital circuits
- Flip-flops are fundamental to sequential logic circuits and play a vital role in memory storage and synchronization of signals with clock edges.
-  Flip-flops are used to store state information in sequential circuits, enabling the creation of memory elements, registers, and other essential components in digital designs.
 
**Why flops??**
- In a combinational circuit, when a input is given to a flop, output changes after the propagation delay
- Output glitches occur due to this propagation delay
- **Glitch** occurs when the intermediate signals reach the next set of gates while they are still transitioning. This can lead to temporary, unwanted changes in the output until all paths stabilize and reach a consistent logic state
- More the number of combinational circuit, more the glitches (output will never settle down)
- To avoid this we want a element to store that value, that is **flop**
- Basically Flops are like storage elements present between the combinational circuits
- output of the flop will change only at the edge of the clock ,therefore even if the input is changing output will be stable
- Hence aviods the transfer of gitch to the subsequent combinational circuits
- Controls pin called **Reset** and **set** are used to initialize the flop
- They can be synchronous or asynchronous

## D Flip-Flop with Asynchronous and synchronous Reset

- asynchronous->irrespective of clock
- synchronous->with respecte to clock
- when both asynchronous and synchronous reset is present, should take care of race
  
  - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
  - `gvim dff_asyncres_syncres.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/b61d78a3-36c0-44d5-83ce-1fc0460c0259">

- **Simulation**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `iverilog dff_asyncres_syncres.v tb_dff_asyncres_syncres.v`
   - `./a.out`
   - `gtkwave tb_dff_asyncres_syncres.vcd`
     
- OUTPUT

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/9af4f145-6e3c-41c1-be66-91236c6726c7">


## Lab flop synthesis simulations

## D Flip-Flop with Asynchronous Reset
- When the asynchronous reset input is asserted (set to 1), the flip-flop's output is immediately forced to 0, regardless of the clock signal's state.
- When the clock rises from 0 to 1, the flip-flop samples the value at its Data (D) input and updates its stored state accordingly.

  - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
  - `gvim dff_asyncres.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/8040e97b-d2f0-4074-b749-b7ccb41b1e96">

- **Simulation**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `iverilog dff_asyncres.v tb_dff_asyncres.v`
   - `./a.out`
   - `gtkwave tb_dff_asyncres.vcd`
     
- OUTPUT
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/7f27ad28-faf1-4cee-8e52-0c969dc71aa6">

- **Synthesis**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog dff_asyncres.v`
   - `synth -top dff_asyncres`
   - `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/febe071c-9064-4fa9-8b30-791b20d73ab8">


## D Flip_Flop with Asynchronous Set
- When the clock rises from 0 to 1, the flip-flop samples the value at its Data (D) input and updates its stored state accordingly.
- When the asynchronous set input (S) is asserted (set to 1), the flip-flop's output (Q) is immediately forced to 1, regardless of the clock signal's state.

  - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
  - `gvim dff_async_set.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/46903c4d-d823-4728-addd-b529b8e5d204">

- **Simulation**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `iverilog dff_async_set.v tb_dff_async_set.v`
   - `./a.out`
   - `gtkwave tb_dff_async_set.vcd`
     
- OUTPUT
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/a6b5ce19-5000-4ba3-9417-2daffcb40554">

- **Synthesis**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog dff_async_set.v`
   - `synth -top dff_async_set`
   - `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/ceb182bc-e9b3-4117-a70f-79d3473b0edc">

## D Flip-Flop with Synchronous Reset 
- When the clock rises from 0 to 1, the flip-flop samples the value at its Data (D) input and updates its stored state accordingly.
- The synchronous reset input (R) allows you to reset the flip-flop's stored state when the clock rises. If the reset input (R) is asserted (set to 1) simultaneously with a rising clock edge, the flip-flop's output (Q) is forced to the reset state (typically 0).

- `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
- `gvim dff_syncres.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/81efabae-3eff-4e71-b1ca-c4e11f69d096">

- **Simulation**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `iverilog dff_syncres.v tb_dff_syncres.v`
   - `./a.out`
   - `gtkwave tb_dff_syncres.vcd`
     
- OUTPUT
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/eb72d454-0ed6-44de-aa3b-afb742966611">

- **Synthesis**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog dff_syncres.v`
   - `synth -top dff_syncres`
   - `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib `
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/7f07809f-825b-4185-864d-75c9ed1de71e">


## Interesting Optimisations
- To look at the RTL code
	- `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
	- `gvim mult_2.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/b5417497-2bdc-4727-a27d-a7e4f45fc286">

- Here input **a** is 3-bit , output **y** is 4-bit and relation is **y=2*a**
- observation
	- A Number **a** multiplied by 2 is a number appended by 0 **{a,0}**
 	- No extra hardware is required for multiplying a number with 2 or powers of 2
    	- ground the LSB , interconnect other bits in order

- Lets see what we get when we synthesis
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog mult_2.v`
   - `synth -top mul2`
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/fbd7454f-fee3-462d-9c73-5c21df1a9aa1">

- **netlist**
    - `write_verilog -noattr mul2_netlist.v`
    - `!gvim mul2_netlist.v`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/bbcc5f98-1592-467e-b251-8748a8386b04">

- Another special case
   - Here input **a** is 3-bit , output **y** is 6-bit and relation is **y=9*a**
- To look at the RTL code
	- `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
	- `gvim mult_8.v`
   
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/a595cde8-95c0-4563-ba6e-07559c2120ba">

- Lets see what we get when we synthesis
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog mult_8.v`
   - `synth -top mult8`
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/218caf9a-2e48-4039-9ad3-524cae3f1efd">

- **netlist**
    - `write_verilog -noattr mul8_netlist.v`
    - `!gvim mult8_netlist.v`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/fd91fb9e-3da0-4fb4-987d-af40b1ccda6f">
   
</details> 
</details>   

## Day 5
<details>
<summary> Combinational and sequential optmizations </summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)


<details>
<summary> Introduction to optimisations</summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)
## Introduction to Logic optimisations

**Combinational Logic optimisations**
- **Combinational logic??** refers to a type of digital logic design where the output is solely determined by the current input values, and there are no memory elements involved. Examples of combinational circuits include adders, multiplexers, demultiplexers, comparators, and more.
- Squeezing the logic to get the most optimised design (Area and power savings)

**Optimisation techniques**
- **Constant Propogation** (Direct Optimisation)
	- dentify signals that are derived from constant inputs or other signals with constant values.
	- Replace these signals with their constant values throughout the logic.
	- Update downstream logic accordingly, simplifying the circuit.
	- This optimization eliminates unnecessary logic and reduces gate count, improving circuit efficiency and performance.
- **Boolean logic optimization** (using K-map or Quine McKluskey)
	- Apply Boolean algebra rules to simplify logic expressions, using techniques like factorization, distribution, and absorption.
   	-  Use Karnaugh Maps (K-Maps) to identify patterns and group terms for simplification.
        - Eliminate redundant terms and simplify expressions further.
	- This optimization reduces the number of gates, improves circuit performance, and enhances overall efficiency.

**Sequential Logic Optimizations**
- **Sequential Logic??** is a fundamental concept in digital circuit design that involves elements capable of storing information (memory elements like flip-flops and latches) and producing outputs based not only on current inputs but also on past inputs and internal states.It forms the basis for many digital devices, including microcontrollers, processors, and communication systems.
- Designers must carefully evaluate the trade-offs between speed, power, and complexity to create effective and optimized sequential logic designs.

**Optimisation techniques**
- Basic
   - **Sequential constant propagation**
	- Sequential constant propagation is an optimization technique that involves identifying and replacing intermediate signals within a sequential circuit with their constant values. This technique aims to eliminate unnecessary calculations and logic, reducing the complexity of the circuit.
- Advanced
   - **State optimization**
     	- State optimization focuses on reducing the number of states in a finite state machine (FSM) or reducing the complexity of state transitions. By eliminating redundant or unreachable states and simplifying the transition logic, designers can create more efficient and streamlined state machines.
   - **Retiming**
     	- Retiming is a technique used to balance the delay of a sequential circuit by moving flip-flops within the design. By strategically relocating flip-flops along the critical path, designers can minimize propagation delays and improve the overall performance of the circuit.
   - **Sequential logic cloning** (Floor Plan Aware Synthesis)
	- Sequential logic cloning involves duplicating a portion of a sequential circuit to optimize its performance. This technique is particularly useful for critical paths where excessive delays are present. By replicating a section of the circuit and introducing additional registers, designers can reduce the delay along the path.
   
</details> 
<details>
<summary> Combinational logic optimizations </summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)
## Combinational logic optimizations (Lab6)
- [opt_check](#opt_check)
- [opt_check2](#opt_check2)
- [opt_check3](#opt_check3)
- [opt_check4](#opt_check4)
- [multiple_module_opt](#multiple_module_opt)
  
## opt_check
- To look at the RTL code
	- `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
	- `gvim opt_check.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/43a315f8-0d96-4b05-adb1-a1e5c980fed8">

- synthesis
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog opt_check.v`
   - `synth -top opt_check`
   - `opt_clean -purge` : For constant Propogation optimisation
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/0e1358d8-9657-4de5-b107-4db795b9a916">

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/6b2571dc-e221-4981-b0ae-5770489b55e5">

## opt_check2
- To look at the RTL code
	- `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
	- `gvim opt_check2.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/b2592f4e-ef1a-4568-8303-5e7e5aa62700">

- synthesis
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog opt_check2.v`
   - `synth -top opt_check2`
   - `opt_clean -purge` 
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/5f309b47-7665-4508-b927-4080c6190296">

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/f5c93b1d-3003-4516-a4f6-6ccf9f841d26">


## opt_check3
- To look at the RTL code
	- `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
	- `gvim opt_check3.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/f62eeed3-3728-4307-9219-06ff4e7ad148">

- synthesis
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog opt_check3.v`
   - `synth -top opt_check3`
   - `opt_clean -purge`
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/af41291a-96e0-41a7-ac5b-a9f9957af8a2">

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/b0fc25c4-ad70-4f55-a896-9bc94c20423b">


## opt_check4
- To look at the RTL code
	- `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
	- `gvim opt_check4.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/4b08507e-1687-42a8-9b30-7e47c5860378">

- synthesis
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog opt_check4.v`
   - `synth -top opt_check4`
   - `opt_clean -purge`
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/310a5ca1-f592-44a5-a150-e8b078bdf693">

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/9c7a8966-12b6-49e0-86d5-8201bfc09d5e">



## multiple_module_opt
- To look at the RTL code
	- `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
	- `gvim multiple_module_opt.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/db948604-3af1-4ad8-a6e0-c80574baf752">

- synthesis
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog multiple_module_opt.v`
   - `synth -top multiple_module_opt`
   - `opt_clean -purge`
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show multiple_module_opt `
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/e4ace4b9-44a4-437f-8734-6df63eeb2b4f">

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/7b4426ed-6f89-4f51-a9b5-f746866829d4">


</details> 
<details>
<summary> Sequential logic optimizations </summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)

## Sequential logic optimizations (Lab7)
- [dff_const1](#dff_const1)
- [dff_const2](#dff_const2)
- [dff_const3](#dff_const3)
- [dff_const4](#dff_const4)
- [dff_const5](#dff_const5)

## dff_const1
- `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
- `gvim dff_const1.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/d280b206-0bd3-407e-8398-fe74eceeba76">

- **Simulation**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `iverilog dff_const1.v tb_dff_const1.v`
   - `./a.out`
   - `gtkwave tb_dff_const1.vcd`
     
- OUTPUT
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/a599e34b-db12-4228-ba8f-2c5f155a0e8d">

- **Synthesis**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog dff_const1.v`
   - `synth -top dff_const1`
   - `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib `
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/410e4642-01a4-4dd3-8f19-c0c8a8b46ba0">

## dff_const2
- `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
- `gvim dff_const2.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/2484b140-e115-4a04-994f-484ab86072b8">

- **Simulation**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `iverilog dff_const2.v tb_dff_const2.v`
   - `./a.out`
   - `gtkwave tb_dff_const2.vcd`
     
- OUTPUT
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/4c5f73bc-d98b-4126-8997-10fee42fcc2c">


- **Synthesis**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog dff_const2.v`
   - `synth -top dff_const2`
   - `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib `
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/3cf456ac-56f4-4462-8c64-495df3147e80">


## dff_const3
- `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
- `gvim dff_const3.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/aa085a87-d270-407c-995b-abee10ff93a0">

- **Simulation**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `iverilog dff_const3.v tb_dff_const3.v`
   - `./a.out`
   - `gtkwave tb_dff_const3.vcd`
     
- OUTPUT
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/7ddc0cd0-fdfb-4b24-a1f6-d684f66eac7f">

- **Synthesis**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog dff_const3.v`
   - `synth -top dff_const3`
   - `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib `
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/499f4930-bf45-4930-b81e-6471172cdbef">

## dff_const4
- `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
- `gvim dff_const4.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/f93252e5-5f97-46ae-b9fb-0291ecb463b2">

- **Simulation**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `iverilog dff_const4.v tb_dff_const4.v`
   - `./a.out`
   - `gtkwave tb_dff_const4.vcd`
     
- OUTPUT
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/953f2daf-4a80-4dcd-974d-6da7183106ba">

- **Synthesis**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog dff_const4.v`
   - `synth -top dff_const4`
   - `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib `
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/71d67c55-a813-45c5-b2a9-a0ba32aeba91">

## dff_const5
- `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
- `gvim dff_const5.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/74c6a764-2115-4bd8-8cb9-6bbe0cfe5063">

- **Simulation**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `iverilog dff_const5.v tb_dff_const5.v`
   - `./a.out`
   - `gtkwave tb_dff_const5.vcd`
     
- OUTPUT
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/f21e94a6-72eb-4cb7-b893-59fa99829cfb">

- **Synthesis**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog dff_const5.v`
   - `synth -top dff_const5`
   - `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib `
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/cdadc96a-5a53-4b12-946d-51a40634c924">

</details> 
<details>
<summary>  Sequential optimizations for unused outputs  </summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)

## Sequential optimizations for unused outputs 
- [counter_opt](#counter_opt)
- [counter_opt2](#counter_opt2)

## counter_opt
- `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
- `gvim counter_opt.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/304f06b8-ebff-4ef8-8cc4-042c2430a350">

- **Synthesis**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog counter_opt.v`
   - `synth -top counter_opt`
   - `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib `
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`

<img width="750" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/ef4f0f85-9e00-4e25-a43c-5dc609c8a5cb">

## counter_opt2
- `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
- `gvim counter_opt2.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/d788dc1d-8c0c-4c86-878c-009c870022f7">

- **Synthesis**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog counter_opt2.v`
   - `synth -top counter_opt`
   - `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib `
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`

<img width="750" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/3562b15a-b362-4977-ae86-71d293ab2684">


</details> 
</details>  

## Day 6
<details>
<summary> GLS, blocking vs non-blocking and Synthesis-Simulation mismatch</summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)

<details>
<summary>GLS, synthesis-Simulation mismatch and Blocking/Non-blocking statements</summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)

- [GLS concepts and flow using iverilog](#GLS-concepts-and-flow-using-iverilog)
- [Synthesis-Simulation mismatch](#Synthesis-Simulation-mismatch)
- [Blocking and Non-blocking statements in verilog](#Blocking-and-Non-blocking-statements-in-verilog)
- [Caveats with blocking statements](#Caveats-with-blocking-statements)
  
## GLS concepts and flow using iverilog
**Gate level simulation (GLS)**
- **What is GLS??**
	- It is a verification process in digital design where the gate-level netlist of a design is simulated to ensure that it behaves as expected after the synthesis process. In gate-level simulation, the design is represented using actual gate-level components (AND gates, OR gates, flip-flops, etc.) and their interconnections.
	- Run the testbench with netlist as the design under test
	- Netlist is logically same as RTL code (same TB will allign with the design)
- **Why GLS??**
	- To verify the logical correctness of design under synthesis
	- Ensuring the timing of the design is met
	- It helps designers catch post-synthesis errors, timing issues, and other potential design flaws.
- **GLS using iverilog**

<img width="750" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/cbeb0cf9-fb14-454b-ae9d-83b7c03a9e36">

## Synthesis-Simulation mismatch

Discrepancies or inconsistencies that can arise between the behavior of a digital design as simulated and its behavior after synthesis.
- **Reasons**
	- Missing sensitivity List
	- Blocking vs Non-blocking assignments
	- Non standard Verilog coding
   
Addressing and minimizing synthesis-simulation mismatch is crucial for ensuring the correctness and reliability of digital designs. Careful validation, consistency in constraints, and understanding the intricacies of the synthesis process are key steps in mitigating this type of issue.
     
## Blocking and Non-blocking statements in verilog
Blocking and non-blocking statements are two types of assignment statements used in Verilog, a hardware description language. They serve different purposes in describing how assignments are executed within a procedural block of code, such as an 'always' or 'initial' block.

- **Blocking Assignment**

    - Blocking assignments in Verilog use the `=` operator for assignment.
    - A blocking assignment is executed sequentially, meaning the next statement will not be executed until the current assignment is complete.
    - The value on the right side of the assignment is immediately assigned to the left-hand side, and the process waits for the assignment to complete before moving on.
    - It represents a procedural programming-style behavior.

```v
a = 1;    // Assign the value 1 to 'a'
b = a;    // Use the current value of 'a' to assign to 'b'
c = b;    // Use the current value of 'b' to assign to 'c'
```

- **Non-blocking Assignment**

    - Non-blocking assignments in Verilog use the <= operator for assignment.
    - A non-blocking assignment schedules the assignment to take place at the end of the current time step without affecting the order of execution of subsequent statements.
    - It is commonly used to model concurrent behavior, particularly in sequential logic circuits, by allowing multiple assignments to occur simultaneously within the same time step.
    - It represents hardware modeling and concurrent behavior more accurately.

```v
always @(posedge clk) begin
  a <= b;  // Schedule the assignment of 'b' to 'a'
  b <= c;  // Schedule the assignment of 'c' to 'b'
  c <= d;  // Schedule the assignment of 'd' to 'c'
end
```

## Caveats with blocking statements

Using blocking statements (`=`) in Verilog can introduce certain caveats and potential issues in your designs. Here are some important considerations to keep in mind:

1. **Sequential Execution:** Blocking assignments are executed sequentially, meaning that each assignment must complete before the next one starts. This can lead to unintended delays and might not accurately capture concurrent behavior.

2. **Race Conditions:** When multiple blocking assignments are used to update the same variable within a procedural block, the final value of the variable is determined by the order of execution. This can lead to race conditions where simulation results might not match hardware behavior.

3. **Combinational Logic:** In combinational logic circuits, using only blocking assignments might not accurately model concurrent behavior. Combinational logic should ideally use non-blocking assignments (`<=`) to capture concurrent signal updates within the same time step.

4. **Sensitivity Lists:** Procedural blocks using blocking assignments should have accurate sensitivity lists to ensure that the code executes when the appropriate events occur. Incorrect sensitivity lists can lead to unexpected simulation behavior.

5. **Simulation vs. Hardware Behavior:** The sequential execution of blocking assignments in simulation might not accurately represent the concurrent behavior of hardware circuits.

6. **Nested Blocking Blocks:** Nesting blocking assignment blocks within each other can lead to unintended delays and can complicate the design.

7. **Timing Analysis:** If used improperly, blocking assignments in synchronous logic (such as setting flip-flop inputs) can lead to incorrect timing analysis results.

8. **State Machines:** When describing state machines, using only blocking assignments might lead to incorrect state transitions if transitions are not carefully managed.

**Best Practices to Mitigate Caveats:**

1. **Use Non-Blocking Assignments:** For modeling concurrent behavior in sequential logic circuits, use non-blocking assignments (`<=`) to avoid race conditions and capture the expected hardware behavior.

2. **Reserve Blocking for Sequential Logic:** Use blocking assignments (`=`) for simple sequential operations where one operation must complete before the next one starts.

3. **Minimize Multiple Blocking Assignments:** Avoid multiple blocking assignments to the same variable within a single procedural block to prevent race conditions.

4. **Sensitivity List Integrity:** Ensure that sensitivity lists in your procedural blocks are accurate and capture the necessary triggers for execution.

5. **Separate Logic Types:** Clearly separate sequential logic (clocked processes) from combinational logic (non-blocking assignments) to maintain accurate modeling.

6. **Avoid Nesting Blocks:** Minimize nesting of blocking assignment blocks to avoid unintended timing effects.

7. **Consult Simulation Warnings:** Pay attention to simulation tool warnings or messages related to the usage of blocking assignments. They can offer insights into potential issues.

By understanding these caveats and applying best practices, you can use blocking assignments effectively while mitigating potential pitfalls and ensuring accurate modeling of your Verilog designs.

</details>     

<details>
<summary>Labs on GLS and Synthesis-Simulation Mismatch</summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)

- [Ternary operator mux](#Ternary-operator-mux)
- [Bad_mux](#Bad-mux)

## Ternary operator mux
- `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
- `gvim ternary_operator_mux.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/1778a50e-e9bd-4ba0-a62c-f6529f501149">

- **Simulation**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `iverilog ternary_operator_mux.v tb_ternary_operator_mux.v`
   - `./a.out`
   - `gtkwave tb_ternary_operator_mux.vcd`
     
- OUTPUT
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/75ddfb8c-c2ec-4f47-916b-6fca39a57df6">

- **Synthesis**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog ternary_operator_mux.v`
   - `synth -top ternary_operator_mux`
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/d788d4e2-217e-45a0-999c-2508e8e2f529">

- **GLS to Gate-Level Simulation**

    - `iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v ternary_operator_mux_net.v tb_ternary_operator_mux.v`
    - `./a.out`
    - `gtkwave tb_ternary_operator_mux.vcd`
      
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/5bc21f41-7d4b-4328-9a6d-addaf16c5225">
      
## Bad_mux
- `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
- `gvim bad_mux.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/ba70bbba-4674-40db-841a-f49f0a0f59cf">

- **Simulation**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `iverilog bad_mux.v tb_bad_mux.v`
   - `./a.out`
   - `gtkwave tb_bad_mux.vcd`
     
- OUTPUT
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/55334f40-31fe-477d-9837-750f4ac90426">

- **Synthesis**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog bad_mux.v`
   - `synth -top bad_mux`
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/0148e431-ffbf-4950-a7a5-18c31b770119">

- **GLS to Gate-Level Simulation**

    - `iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v bad_mux.v tb_bad_mux.v`
    - `./a.out`
    - `gtkwave tb_bad_mux.vcd`
      
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/218556de-de81-4927-82aa-bfa449e393e7">

</details> 

<details>
<summary>Labs on synth-sim mismatch for blocking statement</summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)

## blocking_caveat
- `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
- `gvim blocking_caveat.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/59c74996-fdac-4908-8cde-9d8e19c50dfa">

- **Simulation**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `iverilog blocking_caveat.v tb_blocking_caveat.v`
   - `./a.out`
   - `gtkwave tb_blocking_caveat.vcd`
     
- OUTPUT
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/9b4484ae-49ae-400c-bc2a-ab7d20efff33">

- **Synthesis**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog blocking_caveat.v`
   - `synth -top blocking_caveat`
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/8881c6be-5275-4922-b2e6-1a0ee64e93b0">

- **GLS to Gate-Level Simulation**

    - `iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v blocking_caveat.v tb_blocking_caveat.v`
    - `./a.out`
    - `gtkwave tb_blocking_caveat.vcd`
      
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/f3c28fca-c64b-4ced-96e3-f9d081789505">


</details>   
</details>   
  
</details>                    





  
