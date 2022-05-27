DAY1:

INTRODUCTION TO RISC-V ISA AND GNU COMPILER TOOLCHAIN

How do apps run on a hardware?
Apps flow through the system software which then run on hardware.
The system software consists of operating system-handles i/o operation,memories and to convert the input or the application software to its corresponding assembly language.
The compiler converts the high level language to a machine or assembly level language or instructions. The instructions will be in the format of which the hardware belongs to.
Thye assembler's job is to convert the machine level language or insturctions to the binary level language which is then fed to the hardware.


Psuedo instructions:

![image](https://user-images.githubusercontent.com/92938137/170606284-edeeabd2-8eb6-4663-967f-d6902fe7cfcd.png)

Base integer instruction set:

![image](https://user-images.githubusercontent.com/92938137/170606167-1da353bc-25db-4724-b4cc-ec9ca105067d.png)

Integer Multiply and divide Instruction set:

![image](https://user-images.githubusercontent.com/92938137/170606248-bd189369-b0e2-4535-82c9-b48bf8ee35dc.png)
![image](https://user-images.githubusercontent.com/92938137/170606266-1946da05-aa40-4fce-9cfb-f7cb21f841a0.png)


LABWORK:
![image](https://user-images.githubusercontent.com/92938137/170606485-c770cd7c-cf83-4c9c-b113-d3662bf53f83.png)

![image](https://user-images.githubusercontent.com/92938137/170605834-6c33a3bc-178c-4d5a-b171-0b915462d3ca.png)
DAY2:

INTRODUCTION TO ABI AND BASIC VERIFICATION FLOW

Application binary interface is also called as system call interface that enables the application program to access the registers of RICSV or ARM x28 so on.

There are two ways to load data into the registers- either directly or through memories.
RICSV uses little-endian method of memory addressing.

Using memories,we can load data through various set of instruction,all of 32 bits.

Some commands:

ld x8, 16(x23)//to load a double word into the destination register x8 with offset 16 from the source register x23.
This command uses immediate and registers,therefore is an I Type instruction.
![image](https://user-images.githubusercontent.com/92938137/170602752-eea528aa-d5a7-4fda-83ef-910a8c912af1.png)

add x8, x24,x8//to add the contents in the source registers x28 and x8 and store the result in the destination register x8.
This command uses only registers,therefore is a R Type instruction.
![image](https://user-images.githubusercontent.com/92938137/170602691-3e587f9c-c330-4d68-98f7-ea73f8cf33b0.png)

sd x8, 8(x23)//to store the content in source register x23 to the destination register x8
This command uses source registers ,immediate and also performs store operation,therefore is of S Type instruction.
![image](https://user-images.githubusercontent.com/92938137/170602814-c1e5ab23-6457-4728-8038-2e940ab2d886.png)


//Program to calculate sum of 1 to 9 using ASM

![image](https://user-images.githubusercontent.com/92938137/170595215-fc64d542-5cd1-4bc3-9ef7-b733f43ade81.png)
![image](https://user-images.githubusercontent.com/92938137/170595353-a185e77a-0100-4e13-bc5e-24632cf53ef0.png)

//Assembly Language Code of the function load
![image](https://user-images.githubusercontent.com/92938137/170595365-fc7bab82-c198-49f7-aaa0-cc3f1c73bb20.png)
![image](https://user-images.githubusercontent.com/92938137/170595378-f89719ea-2dfa-4a44-b365-2437dccfb208.png)


//Output
![image](https://user-images.githubusercontent.com/92938137/170595390-7f8d1712-889e-465c-b208-698bb64bda8b.png)
![image](https://user-images.githubusercontent.com/92938137/170595412-35d20e3a-cf0f-4fab-b75f-e42d70154ff0.png)


//Basic Verification flow using iverilog
![image](https://user-images.githubusercontent.com/92938137/170595399-ba0c1275-9a1a-43d8-99c7-8933875cf97b.png)
![image](https://user-images.githubusercontent.com/92938137/170595424-71c58cd9-1a3a-4b78-9aeb-afaa7d247fbd.png)

