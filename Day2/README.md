DAY2:

INTRODUCTION TO ABI AND BASIC VERIFICATION FLOW

Application binary interface is also called as system call interface that enables the application program to access the registers of RICSV or ARM x28 so on.

There are two ways to load data into the registers- either directly or through memories.
RICSV uses little-endian method of memory addressing.

Using memories,we can load data through various set of instruction,all of 32 bits.

Some commands:

ld x8, 16(x23)//to load a double word into the destination register x8 with offset 16 from the source register x23.
This command uses immediate and registers,therefore is an I Type instruction.

add x8, x24,x8//to add the contents in the source registers x28 and x8 and store the result in the destination register x8.
This command uses only registers,therefore is a I Type instruction.

sd x8, 8(x23)//to store the content in source register x23 to the destination register x8
This command uses source registers ,immediate and also performs store operation,therefore is of S Type instruction.


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

