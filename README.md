# Samsung_RISC V

RISC-V is an open standard instruction set architecture (ISA) based on the principles of reduced instruction set computing (RISC). It is designed to be simple, efficient, and extensible, making it suitable for a wide range of computing systems, from embedded devices to supercomputers.

# TASK1

Task is to install required tools for this internship such as ubantu on VMBox,Openlane,RISCV toolchain and to refer to C based and RISCV based lab videos and execute the task of compiling the C code using gcc and riscv compiler
<details>
<summary>Click to expand</summary>


1. Install ubuntu on Oracle Virtual Machine Box

2. Install Openlane

OpenLane is an open-source flow for digital ASIC design, specifically developed to assist in the creation of integrated circuits (ICs) using open-source tools. It provides a complete automated RTL-to-GDSII (Register Transfer Level to GDSII) design flow, integrating multiple open-source tools and frameworks to facilitate chip design.

Follow the below instructions in terminal to install openlane

$ cd Desktop

$ ls -ltr

$ cd work/tools/openlane_working_dir/openlane

$ docker

$ ./flow.tcl -interactive

![openlane](https://github.com/user-attachments/assets/53255d29-317b-49b8-a1c4-0a0d399b11ee)


3. simple C code

open the bash terminal and locate to the diretory where you want to create your file. Then run following command.

$ leafpad sum1ton.c

if leafpad is not downloaded follow the below command in bash.

$ sudo apt install leafpad

click the link for C based lab video https://clicks.aweber.com/y/ct/?l=JDD53n&m=3Y8O_TCXOzMXw_6&b=vLXihi9JLQ3sNdpeivsmdw

![simple c code](https://github.com/user-attachments/assets/109b9bbf-a06d-4538-b880-f6c8531cc757)


Once after saving the code run the following command in bash to get output for the specific code

$ gcc sum1ton.c

$./a.out


![output of c code](https://github.com/user-attachments/assets/51434019-4484-4e07-be8c-6b8281f1e42a)

4. After executing the C code now to convert it into Assembly level language(Object term) follow the below commands in bash.

 $ cat sum1ton.c

 $ riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rc64i -o sum1ton.o sum1ton.c

 $ ls -ltr

  After typing above commands open the new bash terminal and type the following command.

 $ riscv64-unknown-elf-objdump -d sum1ton.o

 Click the link for RISC V based lab video https://clicks.aweber.com/y/ct/?l=JDD53n&m=3Y8O_TCXOzMXw_6&b=lcustSdrnDBWGkNmvZMx5Q
 
![c to assembly11](https://github.com/user-attachments/assets/a2dcb682-fea1-452d-bbe2-7aa641a3cc60)

To see the main program follow the below command

 $ riscv64-unknown-elf-objdump -d sum1ton.o | less

![less](https://github.com/user-attachments/assets/a08ce967-cf32-42c3-9ffd-08605fea206b)

To calculate the number of instructions in main program using calculator 

: /main

We can see the memory address and can calculate number of instructions using calculator.

![15inst](https://github.com/user-attachments/assets/5aa28450-c5ed-4b01-a8a5-17ad27f9cf7e)

5. In step 4 instead of this command  ($ riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rc64i -o sum1ton.o sum1ton.c) if we write the below command we can see that the number of instructions will be reduced.

$ $ riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rc64i -o sum1ton.o sum1ton.c

After this follow same as above steps (step 4).

![12inst](https://github.com/user-attachments/assets/e71fe958-2b2d-4c00-bd67-edaa998d540f)

</details>

# TASK2

Performing SPIKE Simulation and Debugging the C code with Interactive Debugging Mode using Spike

<details>
<summary>Click to expand</summary>


Spike is the official RISC-V Instruction Set Simulator (ISS). It is also referred to as the RISC-V ISA Simulator or RISCV-ISA-Sim. Spike serves as a reference implementation for RISC-V processor functionality, providing a platform to simulate and test RISC-V software and hardware designs.

Key Features of Spike:

1. Instruction Set Simulation:
Spike simulates the execution of programs on RISC-V processors. It supports different RISC-V base ISAs (e.g., RV32I, RV64I) as well as extensions like M (multiplication), A (atomic), F (single-precision floating point), and D (double-precision floating point).

2. Reference Implementation:
As the official simulator, Spike adheres to the RISC-V specifications, making it a reliable tool for verification and debugging.

3. Debugging and Testing:
Spike can be used to test RISC-V programs and verify that the software executes correctly on a simulated RISC-V architecture.

4. Hardware Verification:
Developers can compare the behavior of their custom hardware implementation with the behavior of Spike to ensure compliance with the RISC-V ISA.

Installing Spike:
Spike will be pre installed if you are using riscv.vdi file

Click the below link to get riscv.vdi file

https://forgefunder.com/~kunal/riscv_workshop.vdi

Start of Spike Simulation:

The target is to run the sum1ton file using both gcc compiler and riscv compiler(spike) and both should execute and display same output.
The instructions to run using gcc complier.

$ gcc sum1ton.c

$ ./a.out

The instruction to run using riscv(spike) compiler:

$ spike pk sum_1ton.o

## What is pk(Proxy Kernel) ?:

The pk (Proxy Kernel) is a lightweight runtime environment used with RISC-V simulators and emulators, such as Spike (the RISC-V ISA Simulator), to provide minimal operating system functionality. It is not a full-fledged kernel but acts as a bridge to allow user-level programs to run on simulated or bare-metal RISC-V systems.

### Key Features of the Proxy Kernel

1. Basic Input/Output: Implements simple I/O functions like printf and scanf.

2. Memory Management: Provides minimal memory management for program execution.

3. System Call Handling: Supports a subset of Linux-like system calls for convenience.

4. Compatibility: Works seamlessly with user programs compiled using the RISC-V toolchain.

The below image is the reference to see that output is same for both usimg  gcc compiler and riscv compliler(spike).

![same op using gcc and spike](https://github.com/user-attachments/assets/528b2bd2-d949-4583-94bd-0419dec8d90f)

Following is the snapshot of RISCV Objdump with -Ofast

Open the Objdump of code by using the following command

$ riscv64-unknown-elf-objdump -d sum_1ton.o | less

![main](https://github.com/user-attachments/assets/d5227032-7a06-4095-9086-d9a113059352)

## Debugging the Assembly Language Program of sum_1ton.c

  Open the debugger in another terminal by using the following command

$ spike -d pk sum_1ton.o

The debugger will be opened in the terminal. Now, debugging operations can be performed as shown in the following snapshot.

$ until pc 0 100b0 : This command says that pc starts debugging from 100b0

![spike debugger](https://github.com/user-attachments/assets/2e4e4848-0514-43c9-bd6a-bb0be59cac8d)

Press enter to move into the next instruction.

![instructions](https://github.com/user-attachments/assets/f83be108-9be3-4fad-be00-bed4ab6f6e13)

Debugging operations can be performed as shown in the following snapshot.

Calculation of sp value before and after the instruction 

$ addi sp,sp,-16

addi: This is the "add immediate" instruction. It performs an addition of a register and an immediate value (a constant) and stores the result in a destination register.

lui: This instruction stands for Load Upper Immediate in the RISC-V assembly language.

![address calculation](https://github.com/user-attachments/assets/33ee66ee-7473-4412-922e-9650032314c6)

</details>

# TASK3

Task is to identify instruction type of all the given instructions with its exact 32 bits instruction code in the desired instruction type format


<details> 
<summary>click to expand</summary>


RISC-V uses a fixed 32-bit instruction length and defines six primary instruction formats: R, I, S, B, U, and J. These formats describe how various fields within the 32-bit instruction word are used.

There are 6 instruction formats in RISC-V:

1. R-format
2. I-format
3. S-format
4. B-format
5. U-format
6. J-format

![Image](https://github.com/user-attachments/assets/ba8c652d-c1c0-4521-bce6-a70cc8592005)

## 1. R Type instruction

 The R-Type instruction is used for operations that involve registers and not memory locations. This format is typically used for arithmetic and logical operations. The instruction is divided into six fields:

 ![Image](https://github.com/user-attachments/assets/5a2c6900-b832-4464-96bf-c55f18bf728c)

- opcode(7bits)  ->   Specifies the operation (e.g., ADD, SUB).
- rd(5bits)      ->   Destination register where the result is stored.
- func3(3bits)   ->   Defines the specific type of operation.
- rs1(5bits)     ->   Source register 1.
- rs2(5bits)	    ->   Source register 2.
- func7(7bits)	  ->   Further distinguishes the operation (e.g., difference between ADD and SUB).

## 2. I Type instruction

I-type instruction format in RISC-V is a 32-bit instruction word that specifies one source operand as a 12-bit constant. This constant is a signed 2's complement number that is sign extended to form a 32-bit operand.

![Image](https://github.com/user-attachments/assets/990ba914-5c26-469c-a5f7-d9ee87593697)

- They can be used for load/store operations, branch operations, or immediate ALU operations. 
- The sign-bit for the immediate is always in bit 31 of the instruction. 
- RISC-V has an asymmetric immediate encoding, which means that the immediates are formed by concatenating different bits in an asymmetric order.


opcode	(0–6bits) -> 	Specifies the type of operation (e.g., LOAD, ADDI).
rd	(7–11bits) -> 	Destination register.
funct3	(12–14bits) -> 	Specifies the operation within the opcode.
rs1	(15–19bits) -> 	Source register 1.
imm[11:0]	(20–31bits) -> 	12-bit immediate value (sign-extended).

## 3. S Type instruction

The S-type instruction format in RISC-V is used to store data from a register into memory.S-type instructions are also known as store instructions.

- The S-type instruction format uses an immediate value to store the address where the data is to be stored. 
- The S-type instruction format uses the upper seven bits of the instruction to store the immediate value.

![Image](https://github.com/user-attachments/assets/50466dca-ca91-4a71-bf0e-862edfba3472)

- imm[11:5]	(31-25bits) -> 	Upper 7 bits of the immediate value
- rs2	(24-20bits) -> 	Source register 2 (contains data to be stored)
- rs1	(19-15bits) -> 	Source register 1 (base address register)
- funct3	(14-12bits) -> 	Function code (determines the store operation)
- imm[4:0]	(11-7bits) -> 	Lower 5 bits of the immediate value
- opcode	(6-0bits) -> 	Operation code (e.g., 0100011 for store)

## 4. B type instruction

RISC-VThe B-type instruction format in RISC-V is used for branch instructions that transfer control to a new instruction address. B-type instructions are a variation of the S-type format and are sometimes called SB.

![Image](https://github.com/user-attachments/assets/80c6b790-7a5c-4523-8d0a-8020f7e71bae)

- The first 7 bits are reserved for the opcode 
- The instruction includes at least one register operand, such as rs1, rs2, or rd 
- The instruction encodes branch offsets that are multiples of 2 
- The target address for the instruction is calculated by adding the branch offset to the PC address 
- There are two source registers rs1 and rs2 on which various operations are performed based on certain conditions, and those conditions are defined by func3 field.
- After performing operations on the source register based on the conditions, it is evaluated that if the condition is true, Program Counter value gets updated by PC = Present PC Value + Immediate Value, and if the condition is false then PC will be given as PC = Present PC value + 4 bytes, which states that PC will move to next instruction set.

- imm[12]	(31bit) -> 	Most significant bit of the immediate value
- imm[10:5]	(30-25bits) -> 	Bits 10 to 5 of the immediate value
- rs2	(24-20bits) ->	Source register 2 (used for comparison)
- rs1	(19-15bits) ->	Source register 1 (used for comparison)
- funct3	(14-12bits) ->	Function code (determines the branch condition)
- imm[4:1]	(11-8bits) -> 	Bits 4 to 1 of the immediate value
- imm[11]	(7bit) -> 	Bit 11 of the immediate value
- opcode	(6-0bits) -> 	Operation code (e.g., 1100011 for branch)

## 5. U Type instruction

In RISC-V, the U-type instruction format is used for instructions involving immediate values that occupy the upper 20 bits of a 32-bit word. The two primary U-type instructions are:

- LUI (Load Upper Immediate): Used to load a 20-bit immediate into the upper 20 bits of a register.
- AUIPC (Add Upper Immediate to PC): Computes a target address by adding a 20-bit immediate to the current program counter (PC).

![Image](https://github.com/user-attachments/assets/1aafbf66-05c9-4471-8fc0-8e12ad355115)

- imm[31:12]	(31-12bits) -> 	The 20-bit immediate value (upper bits)
rd	(11-7bits) -> 	Destination register
opcode	(6-0bits) -> 	Operation code (e.g., 0110111 for LUI)

## 6. J Type instruction

The J-type instruction format is used for jump instructions, which involve an immediate value specifying a target address relative to the current program counter (PC). The primary J-type instruction is:

- JAL (Jump and Link): Used to jump to a target address and save the return address in a register.
- The J-type instruction format is a variation of the U-type format, and is sometimes called UJ. 
- The J-type instruction format is used for PC updating instructions, such as jumps and branches. 
- The J-type instruction format uses a 20-bit immediate value, which is larger than the immediate values used in other instruction formats.

![Image](https://github.com/user-attachments/assets/82a1711c-4776-4896-8906-bb53bfba1b0e)

- imm[20]	(31bit) -> 	Most significant bit of the immediate value
- imm[10:1]	(30-21bits) -> 	Bits 10 to 1 of the immediate value
- imm[11]	(20bit) -> 	Bit 11 of the immediate value
- imm[19:12]	(19-12bits) -> 	Bits 19 to 12 of the immediate value
- rd	(11-7bits) -> 	Destination register (to store return address)
- opcode	(6-0bits) -> 	Operation code (e.g., 1101111 for JAL)

### Now let us analyse the instructions of riscv -objdump application code:

## 1. lui a0,0x21

- The instruction LUI a0, 0x21 is a U-type instruction in RISC-V.
- Type: U-type (Load Upper Immediate)
- Opcode: 0110111 (for LUI)
- a0 is the destination register.
- 0x21 is the 20-bit immediate value (decimal 33).

### 32 bit instruction is: 00000000000000100001_01010_0110111

## 2. addi  sp,sp,-16

- The instruction addi sp, sp, -16 is an I-type instruction in RISC-V
- Opcode: 0010011 (for ADDI - Add Immediate).
- sp is both the source (rs1) and destination (rd) register.
- -16 is the signed immediate value.

### 32 bit instruction is: 111111111000 00010 000 00010 0010011

## 3. li a5 55

- The instruction li a2, 55 is a pseudo-instruction in RISC-V. It expands to a real instruction depending on the immediate value. Since 55 fits within 12 bits, it translates to an I-type ADDI instruction.
- a2 corresponds to register x12.
- Immediate value: 55.
- Opcode: 0010011

 ### 32 bit instruction is:000000110111 00000 000 01100 0010011

## 4. li a1,10

- The instruction li a1, 10 is a pseudo-instruction in RISC-V. Since the immediate value 10 fits within 12 bits, it translates to an I-type ADDI instruction.
- Destination Register (a1): Register x11.
- Immediate: 10.
- Opcode: 0010011

 ### 32 bit instruction i:000000001010 00000 000 01011 0010011

## 5. 
  
