
# Pipelined RISC-V CPU Core

The following repository contains all the information and codes that's needed to a build a 4-stage Pipelined RISC-V Core which is designed during the RISC-V MYTH Workshop. The core supports the RV32I Base Integer Instruction Set. It is developed and implemented in TL-Verilog on Makerchip platform.


## Index
- Introduction to RISC-V ISA
- [GNU Compliler Toolchain](https://github.com/RISCV-MYTH-WORKSHOP/riscv_myth_workshop_may22-Shris7#gnu-compiler-toolchain)
- Introduction to ABI
- Digital Logic with TL-Verilog and Makerchip
     - Combinational Logic Calculator
     - Sequential Logic
       - Fibonacci Sequence
       - Counter
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
    - Test Bench
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

   - ld x8, 16(x23)//to load a double word into the destination register x8 with offset 16 from the source register x23.
     - This command uses immediate and registers,therefore is an I Type instruction.
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

## DIGITAL LOGIC WITH TL-VERILOG AND MAKERCHIP

- We can code, compile, simulate, and debug Verilog designs, all from our browser. Our code, block diagrams, waveforms, and novel visualization capabilities are          tightly integrated for a seamless design experience.
- Advantages:
  - Develop Verilog in your Browser
  - Easy Pipelining
  - Organized Waveforms
  - Organized Diagrams
  - Linked Design and Debug
## Combinational Logic Calculator
![image](https://user-images.githubusercontent.com/92938137/170912732-d39a4d03-20a7-46a7-8bd2-71f3474a2035.png)
![image](https://user-images.githubusercontent.com/92938137/170809678-7063cad8-4f61-400c-a99c-e3df91d2a141.png)

## Sequential Logic
- Fibbonaci Sequence

![image](https://user-images.githubusercontent.com/92938137/170912810-ff77bbc5-8d98-4173-8a91-28aa95c5ede0.png)
![image](https://user-images.githubusercontent.com/92938137/170808413-c62b72ac-b63e-494d-8f05-b5fdc1d6167d.png)
- Counter
![image](https://user-images.githubusercontent.com/92938137/170912972-8d1fa5ad-6697-4739-bfac-dd2f4a00984a.png)

- Sequential Calculator

![image](https://user-images.githubusercontent.com/92938137/170913068-c366609a-3678-44c6-bf02-969b82997fbc.png)

## Pipelined Logic
- Defined with a '|' symbol
- Within the Pipeline, multiple stages can be defined using '@'
- Calculator and Counter in pipeline

![image](https://user-images.githubusercontent.com/92938137/170815690-94e0049d-e676-417c-b18e-8bb4fa462c52.png)
- 2-cycle calculator

![image](https://user-images.githubusercontent.com/92938137/170913288-e9c9053a-84a2-4d1c-b312-210228aeb783.png)
![image](https://user-images.githubusercontent.com/92938137/170812865-8135f7b4-e183-4945-ba8a-c34e2d7886f6.png)
![image](https://user-images.githubusercontent.com/92938137/170812888-4ace255e-3d40-40f7-b73a-ee2c1d05cabf.png)

## Validity
- Validity can be understood by the word when?
- This functionality is not a part of other circuit design languages and is exclusive to TLV
- This will make no difference on the nature of the code.
- It  decides when a signal has significance, so it is only executed then.
- This keeps the Waveform clean and easy to debug
- You will see this operator being used '?' throughout the CPU Code.

- Total Distance Problem

![image](https://user-images.githubusercontent.com/92938137/170913564-41c96a38-4c66-4316-8a4d-9fb414a6ea61.png)
![image](https://user-images.githubusercontent.com/92938137/170814041-eab3b9a5-75ab-47c0-b43c-941d6d60d1ee.png)
- 2-cycle calculator with Validity

![image](https://user-images.githubusercontent.com/92938137/170913988-dcbe89c1-47df-4b26-bf01-2fd819f94b62.png)
![image](https://user-images.githubusercontent.com/92938137/170816685-cb5b0b2c-abbf-4279-a199-c26e4f2f3f84.png)
![image](https://user-images.githubusercontent.com/92938137/170816700-8f160ef6-88b0-4ff0-a0ea-981c1c9b8360.png)

## Calculator with memory
![image](https://user-images.githubusercontent.com/92938137/170914292-2d4ce84f-18fd-47cb-a1df-d98f6f7778e3.png)
![image](https://user-images.githubusercontent.com/92938137/170878578-e173df05-4b54-4585-97a2-53a85ab28299.png)
![image](https://user-images.githubusercontent.com/92938137/170878603-dd91531d-3e2d-4c67-b948-de07d8604c30.png)
![image](https://user-images.githubusercontent.com/92938137/170878655-daf62abd-506e-4bf0-8a72-4086604a0bb7.png)

## BASIC RISC-V CPU MICRO-ARCHITECTURE
- This section we will implement the risc-v cpu in three stages: Fetch, Decode, Excecute

## Fetch logic
- Program Counter(PC), also called as Instruction Pointer is a block which contains the address of the next instruction to be executed.
- It is feed to the instruction memory which gives out the instruction to be executed.
- PC is incremented by four after every valid iteration.
- The output of the program counter is used for fetching an instruction from the instruction memory.
- The instruction memory gives out a 32-bit instruction depending upon the input address.
- During Fetch Stage, processor fetches the instruction from the IM pointed by address given by PC.

![image](https://user-images.githubusercontent.com/92938137/170914453-6926c8af-05a8-4140-b5b3-a4109273562f.png)
![image](https://user-images.githubusercontent.com/92938137/170914489-6806a193-bc95-43d0-8e24-92e050b48bed.png)
![image](https://user-images.githubusercontent.com/92938137/170820048-4b62bc41-d4d3-4c6c-a0cb-5c222d9a6429.png)

## Instruction Decode
- In decode the CPU identifies which instruction has been read in by the processor
- There are 6 types of instructions we have implemented:
   - R-type : Register
   - I-type : Immediate
   - S-type : Store
   - B-type : Branch
   - U-type : Upper Immediate
   - J-type: Jump
- The register file used here allows 2 reads and 1 write.

![image](https://user-images.githubusercontent.com/92938137/170914924-ed45a140-cec0-4805-bb0f-a7b126bb9497.png)
![image](https://user-images.githubusercontent.com/92938137/170824067-5bce710c-d1cb-4d12-bcb6-3013c950a7de.png)
![image](https://user-images.githubusercontent.com/92938137/170824087-1f7f9d05-42ba-40a8-b09f-01f6fc9dce77.png)

- To Decode Instruction Field Based on Instr Type RV-ISBUJ
 
![image](https://user-images.githubusercontent.com/92938137/170915131-362575fe-3916-4ef1-a538-79f154ba7b82.png)
![image](https://user-images.githubusercontent.com/92938137/170825404-58384194-0911-4025-ac99-f79d825faee5.png)
![image](https://user-images.githubusercontent.com/92938137/170825416-513e433f-534f-448d-a750-4860b4bd60e4.png)

- Decode individual instruction

![image](https://user-images.githubusercontent.com/92938137/170915173-b85fcf80-7c98-4ad8-ba4c-35d2650ce665.png)
![image](https://user-images.githubusercontent.com/92938137/170826071-a408bdca-7289-4c23-afe1-e7d7fe82f4b5.png)
![image](https://user-images.githubusercontent.com/92938137/170826083-677518e2-b854-44bf-bc65-e362f19be7b5.png)

## Register File read and write
- Inputs:
   - Read_Enable - Enable signal to perform read operation
   - Read_Address1 - Address1 from where data has to be read
   - Read_Address2 - Address2 from where data has to be read
   - Write_Enable - Enable signal to perform write operation
   - Write_Address - Address where data has to be written
   - Write_Data - Data to be written at Write_Address
- Outputs:
   - Read_Data1 - Data from Read_Address1
   - Read_Data2 - Data from Read_Address2

![image](https://user-images.githubusercontent.com/92938137/170915410-52a8d909-010e-4f40-b4dd-c71257c4b838.png)
- Read Operation

![image](https://user-images.githubusercontent.com/92938137/170827535-8a329dda-bb65-4e32-9160-d5e5726d1989.png)
![image](https://user-images.githubusercontent.com/92938137/170827542-bb6aa84b-a922-4199-ad76-c18ee975242c.png)
![image](https://user-images.githubusercontent.com/92938137/170827546-daffaf0d-104c-4b97-978c-314f4026700e.png)

- Write Operation

![image](https://user-images.githubusercontent.com/92938137/170828336-f45793bd-a682-4251-b93a-633b3194ad5c.png)
![image](https://user-images.githubusercontent.com/92938137/170828324-4b345f15-d386-4feb-931e-b0c3988b1b81.png)

## Excecute ALU Operations
- Operands perform the opration based on the opcode
![image](https://user-images.githubusercontent.com/92938137/170827809-76f5288c-d27d-4df3-87df-b4a9f14ae9df.png)
![image](https://user-images.githubusercontent.com/92938137/170828360-218de152-e8c6-4c76-b106-05e120de27ab.png)

## Branch Instruction Implemenataion
- We control the logic or rather embed logic in our programs using control logic instructions i.e. Branch Instructions
![image](https://user-images.githubusercontent.com/92938137/170915713-0e9367da-04a4-45a6-a376-61b0af7ec2ad.png)
![image](https://user-images.githubusercontent.com/92938137/170831616-633043cc-4d56-421c-9765-c243fba67ac3.png)
![image](https://user-images.githubusercontent.com/92938137/170831641-e4c16ed9-1ae9-4b57-b17a-ac0321a61078.png)
![image](https://user-images.githubusercontent.com/92938137/170831679-61cd9ed8-12c1-4afa-be41-bca6be37f704.png)

## Test Bench
![image](https://user-images.githubusercontent.com/92938137/170915785-88ab0d70-666e-43d9-bad0-3a52035aef19.png)
![image](https://user-images.githubusercontent.com/92938137/170831933-eaefb266-f9ce-4220-8a5a-bb27452a5d3d.png)
![image](https://user-images.githubusercontent.com/92938137/170831954-30d03887-d407-4e6a-81be-3b380c3ef7ec.png)
![image](https://user-images.githubusercontent.com/92938137/170831959-ceb35c41-5b6f-45c0-b8c3-625922d6c8a2.png)
![image](https://user-images.githubusercontent.com/92938137/170831975-4978bb3c-28eb-4734-86e8-07ecbfcff1dd.png)
![image](https://user-images.githubusercontent.com/92938137/170831987-77d78be5-dfad-46f3-918c-021dcece3f67.png)

## PIPELINED RISC-V CPU MICROARCHITECTURE
- Pipelining the CPU with branches involves 3 cycle delay and the other instructions are pipelined 
- There are various hazards to be taken into consideration while implementing a pipelined design such as:
    - Control Flow
    - Read-before-Write Hazard issues.
- 3 cycle Validity:

![image](https://user-images.githubusercontent.com/92938137/170916143-c8b88bb5-a6cd-43bc-989f-0e0aac401917.png)
![image](https://user-images.githubusercontent.com/92938137/170850829-d3b4f1f9-2882-4035-a8a1-3aef7ca87e24.png)
![image](https://user-images.githubusercontent.com/92938137/170850838-06615c74-d6d1-4c9c-a5f2-b299624a7240.png)

## Load and store Instructions and Memory
- A Data memory can be added to the Core. The Load-Store operations will add up a new stage to the core.
- Thus, making it now a 4-Stage Core / CPU.
![image](https://user-images.githubusercontent.com/92938137/170916625-495e3c19-c600-4402-96a8-53af28bb522c.png)
![image](https://user-images.githubusercontent.com/92938137/170916691-2dc58720-2f97-4f7f-8974-38f35ce3ecc6.png)
![image](https://user-images.githubusercontent.com/92938137/170916710-0ddf6441-9b8d-4e63-93b6-293f8a8d6b2b.png)
![image](https://user-images.githubusercontent.com/92938137/170875215-a400eebb-92b6-47d8-bb1d-1295bf1bcd76.png)
![image](https://user-images.githubusercontent.com/92938137/170875231-783e3299-b4d6-4121-9de6-afabf22c7429.png)
![image](https://user-images.githubusercontent.com/92938137/170875586-0f78c489-9ea1-41a7-8eaf-604f262470fc.png)
![image](https://user-images.githubusercontent.com/92938137/170875607-1f3cf0ac-198b-4c77-b191-9b02d649460b.png)
![image](https://user-images.githubusercontent.com/92938137/170877732-c9a4f498-4e1f-4243-874e-48d8b8665e80.png)

## Completing the RISC-V Core
- Add the jump Instructions
- instructions to decode the ALU logic is also added.
![image](https://user-images.githubusercontent.com/92938137/170916876-b7d724e8-40ad-4089-a423-cc2be9301a73.png)
![image](https://user-images.githubusercontent.com/92938137/170916948-58c8ad49-295f-4ada-804d-6b557c51c234.png)
![image](https://user-images.githubusercontent.com/92938137/170878242-fdaeceaf-3029-43f8-998e-e03db4ba31fc.png)
![image](https://user-images.githubusercontent.com/92938137/170878288-ee7a2518-5771-4542-b733-9e2d4f574a3f.png)
![image](https://user-images.githubusercontent.com/92938137/170878311-21456611-e618-490c-a1e1-b2d05cd83f80.png)
![image](https://user-images.githubusercontent.com/92938137/170878327-c993ae1c-86be-4fd3-90bd-19c6be8ff948.png)
![image](https://user-images.githubusercontent.com/92938137/170878349-b5c7dd71-8c49-449a-9f48-eb558bbab25d.png)

## Acknowledgements

 - [Kunal Ghosh](https://github.com/kunalg123),Co-founder VSD Corp,Pvt Ltd.
 - [Steve Hover](https://github.com/stevehoover),Founder,Redwood EDA
 - [Shivam Potdar](https://github.com/shivampotdar),TA
 - [Shivani Shah ](https://github.com/shivanishah269),TA
 - [Vineet Jain](https://github.com/vineetjain07),TA





