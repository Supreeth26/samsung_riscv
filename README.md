# samsung_riscv

RISC-V is an open standard instruction set architecture (ISA) based on the principles of reduced instruction set computing (RISC). It is designed to be simple, efficient, and extensible, making it suitable for a wide range of computing systems, from embedded devices to supercomputers.

TASK1:  Task is to install required tools for this internship such as ubantu on VMBox,Openlane,RISCV toolchain and to refer to C based and RISCV based lab videos and execute the task of compiling the C code using gcc and riscv compiler
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


![openlane](https://github.com/user-attachments/assets/53255d29-317b-49b8-a1c4-0a0d399b11ee)


3. simple C code

open the bash terminal and locate to the diretory where you want to create your file. Then run following command.

$ leafpad sum1ton.c

if leafpad is not downloaded follow the below command in bash.

$ sudo apt install leafpad


![simple c code](https://github.com/user-attachments/assets/109b9bbf-a06d-4538-b880-f6c8531cc757)


Once after saving the code run the following command in bash to get output for the specific code

$ gcc sum1ton.c

$./a.out


![output of c code](https://github.com/user-attachments/assets/51434019-4484-4e07-be8c-6b8281f1e42a)

4. After executing the C code now to convert it into Assembly level language follow the below commands in bash.

 $ cat sum1ton.c

 $ riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rc64i -o sum1ton.o sum1ton.c

 $ ls -ltr

  After typing above commands open the new bash terminal and type the following command.

 $ riscv64-unknown-elf-objdump -d sum1ton.o
 
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

![Screenshot 2024-06-13 002342](https://github.com/user-attachments/assets/d6ee2814-c86b-49b1-93ba-27cc9fce2b60)


