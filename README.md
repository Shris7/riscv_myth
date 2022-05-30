
# Pipelined RISC-V CPU Core

The following repository contains all the information and codes that's needed to a build a 4-stage Pipelined RISC-V Core which is designed during the RISC-V MYTH Workshop. The core supports the RV32I Base Integer Instruction Set. It is developed and implemented in TL-Verilog on Makerchip platform.


## Index
- Introduction to RISC-V ISA
- GNU Compliler Toolchain
- Introduction to ABI
- Digital Logic with TL-Verilog and Makerchip
     - Combinational Logic Calculator
     - Sequential Logic
       - Fibonacci Sequence
       - Sequential Calculator
     - Pipelined Logic
       - Calculator and counter in pipeline
       - 2-cycle calculator
    - Validity
       - To Compute Total Distance
       - 2-cycle calculator with validity
    - Calculator with memory
- Basic RISC-V CPU Micro-architecture
    - Instruction Fetch Logic
    - Instruction Decode Logic
    - Register File Read and Write
    - Execute ALU Operations
    - Control Branch Instruction Logic
- Pipelined RISC-V CPU Micro-architrcture
    - Pipelinig the CPU
    - Load and Store Instructions and Memory
    - Completing the RISC-V Core
- Acknowledgements
## INTODUCTION TO RISC-V ISA

- RISC-V is an open standard instruction set architecture (ISA) based on established reduced instruction set computer (RISC) principles. Unlike most other ISA designs, the RISC-V ISA is provided under open source licenses that do not require fees to use.
- A RISC-V hart has a single byte-addressable address space of 2XLEN bytes for all memory accesses. A word of memory is defined as 32 bits (4 bytes). Correspondingly, a halfword is 16 bits (2 bytes), a doubleword is 64 bits (8 bytes), and a quadword is 128 bits (16 bytes)

## GNU COMPILER TOOLCHAIN
- Similar to other ISA's RISC-V has its own tool chain.Toolchain is simply a set of tools used to compile a piece of code to produce an executable program.
- Preprocessor - Processes source code before compilation.
- Compiler - Takes the input provided by preprocessor and converts to assembly code.
- Assembler - Takes the input provided by compiler and converts to relocatable machine code.
- Linker - Takes the input provided by Assembler and converts to Absolute machine code.
- Steps to use RISC_V Toolchain:
   - Command to use the risc-v gcc compiler:
     ```bash
     riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o <object filename> <C filename>
     ```
  - Command to view the assembly code:
   ```bash
        riscv64-unknown-elf-objdump -d <object filename>
   ```
  - Command to use SPIKE simualtor to run risc-v obj file:
     ```bash
        spike pk <object filename>
    ```
  - Command to use SPIKE as debugger:
     ```bash
      spike -d pk <object Filename> with degub command as until pc 0 <pc of your choice>
    ```

 - Compute sum 1 to 9 
 ![image](https://user-images.githubusercontent.com/92938137/170606485-c770cd7c-cf83-4c9c-b113-d3662bf53f83.png)
 ![image](https://user-images.githubusercontent.com/92938137/170605834-6c33a3bc-178c-4d5a-b171-0b915462d3ca.png)
 ![image](https://user-images.githubusercontent.com/92938137/170606766-5ce2cfbc-d418-4225-ba41-052d987005cd.png)
 
 ![image](https://user-images.githubusercontent.com/92938137/170607112-f49cc9e7-d74a-41e3-9d95-60db42a00797.png)
 ![image](https://user-images.githubusercontent.com/92938137/170607263-1c1bfcb9-f347-4551-8ccc-08560be8311b.png)
 
 - No of instructions used with O1 is 15

 ![image](https://user-images.githubusercontent.com/92938137/170607438-609fe2ad-1c6f-4048-99b6-a4770c398a3b.png)
 ![image](https://user-images.githubusercontent.com/92938137/170607495-3a5806ea-6bb5-4bbb-9daa-f8d7fc7ad355.png)

- No of instructions with Ofast is 12

- UNSIGNED AND SIGNED INTEGERS

   - Range of unsigned numbers for a double word: 0 to (2^64-1)

![image](https://user-images.githubusercontent.com/92938137/170608156-6dffbcb2-c5cd-4c8b-9c71-f386815d6d59.png)
![image](https://user-images.githubusercontent.com/92938137/170607954-9d248c33-e514-4f03-8403-a2fc5d9a0d5b.png)
![image](https://user-images.githubusercontent.com/92938137/170608302-a9c9ecd0-4f01-4f32-9b65-27b25c99cedf.png)

![image](https://user-images.githubusercontent.com/92938137/170608381-c6967e1f-f22a-4448-979a-0780e777e7bf.png)
![image](https://user-images.githubusercontent.com/92938137/170608423-8d15aa3b-41b3-462f-8c9d-537e02e11ead.png)

![image](https://user-images.githubusercontent.com/92938137/170608590-4c70ceb4-9eb9-4244-85b9-226ffeb3abb2.png)
![image](https://user-images.githubusercontent.com/92938137/170608656-d0b8d1b2-33cb-423e-85a9-aca9b2d4c4d0.png)

![image](https://user-images.githubusercontent.com/92938137/170612733-10506461-5adb-4f33-addf-05d5adfca74e.png)
![image](https://user-images.githubusercontent.com/92938137/170612842-c92f81cd-3da4-4824-a3f7-d735c46de1e6.png)

![image](https://user-images.githubusercontent.com/92938137/170609052-4741ad2d-8fd5-49e5-a32e-11fd67998fd0.png)
![image](https://user-images.githubusercontent.com/92938137/170609127-9bc398e8-4ef4-41cd-8166-d502d7a64081.png)

    - Range of signed integers: 0 to 2^63-1 for positive numbers and -1 to 2^63-1 for negative numbers

![image](https://user-images.githubusercontent.com/92938137/170612370-9d19e764-de8a-43c0-a889-979521144c41.png)
![image](https://user-images.githubusercontent.com/92938137/170612424-3b960718-f9f6-41b8-9d64-2fa5c3557215.png)

## INTRODUCTION TO ABI
 - Application binary interface is also called as system call interface that enables the application program to access the registers of RICSV or ARM x28 so on.

- There are two ways to load data into the registers- either directly or through memories.
- RICSV uses little-endian method of memory addressing.

- Using memories,we can load data through various set of instruction,all of 32 bits.

- Some commands:

   -ld x8, 16(x23)//to load a double word into the destination register x8 with offset 16 from the source register x23.
     -This command uses immediate and registers,therefore is an I Type instruction.
![image](https://user-images.githubusercontent.com/92938137/170602752-eea528aa-d5a7-4fda-83ef-910a8c912af1.png)

   - add x8, x24,x8//to add the contents in the source registers x28 and x8 and store the result in the destination register x8.
     - This command uses only registers,therefore is a R Type instruction.
![image](https://user-images.githubusercontent.com/92938137/170602691-3e587f9c-c330-4d68-98f7-ea73f8cf33b0.png)

   - sd x8, 8(x23)//to store the content in source register x23 to the destination register x8
     - This command uses source registers ,immediate and also performs store operation,therefore is of S Type instruction.
![image](https://user-images.githubusercontent.com/92938137/170602814-c1e5ab23-6457-4728-8038-2e940ab2d886.png)


- Program to calculate sum of 1 to 9 using ASM

![image](https://user-images.githubusercontent.com/92938137/170595215-fc64d542-5cd1-4bc3-9ef7-b733f43ade81.png)
![image](https://user-images.githubusercontent.com/92938137/170595353-a185e77a-0100-4e13-bc5e-24632cf53ef0.png)

- Assembly Language Code of the function load
![image](https://user-images.githubusercontent.com/92938137/170595365-fc7bab82-c198-49f7-aaa0-cc3f1c73bb20.png)
![image](https://user-images.githubusercontent.com/92938137/170595378-f89719ea-2dfa-4a44-b365-2437dccfb208.png)


- Output
![image](https://user-images.githubusercontent.com/92938137/170595390-7f8d1712-889e-465c-b208-698bb64bda8b.png)
![image](https://user-images.githubusercontent.com/92938137/170595412-35d20e3a-cf0f-4fab-b75f-e42d70154ff0.png)


- Basic Verification flow using iverilog
![image](https://user-images.githubusercontent.com/92938137/170595399-ba0c1275-9a1a-43d8-99c7-8933875cf97b.png)
![image](https://user-images.githubusercontent.com/92938137/170595424-71c58cd9-1a3a-4b78-9aeb-afaa7d247fbd.png)



## Acknowledgements

 - [Kunal Ghosh](https://github.com/kunalg123)
 - [Steve Hover](https://github.com/stevehoover)
 - [Shivam Potdar](https://github.com/shivampotdar)
 - [Shivani Shah ](https://github.com/shivanishah269)
 - [Vineet Jain](https://github.com/vineetjain07)





