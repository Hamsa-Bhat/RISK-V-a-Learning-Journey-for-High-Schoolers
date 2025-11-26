# RISK-V-a-Learning-Journey-for-High-Schoolers
This repository explores how a C program transforms into hardware through RISC-V, ISA, RTL, and related concepts. We start from the basics and gradually dive deeper to understand every layer of the RISC-V ecosystem, from software instructions to actual processor execution.
## Introduction to RISC-V
RISC-V RISC-V stands for Reduced Instruction Set Computer, it has small and simple instructions which makes hardware design easier to implement it is an Open source Instruction Set Architecutre (ISA) used for designing the computers.
ISA ISA as we previously saw stands for Instruction Set Architecture it defines the instructions the porcessor understands and how it manipulates the data. It is the language of the computer and they way we'll talk to the computer. ISA acts asa bridge between the software and the hardware and makes it easier to communicate between these two. It tells us -
• What Instructions Exist
• How to format them
• How a CPU should execute them

## RISC - V Architecture
RISC stands for Reduced Instruction Set Computer. RISC-V is open-source. 
This means anyone can design a processor using RISC-V without paying licensing fees.
It has a small, simple base set of instructions, which makes hardware easier to design and implement.

## C Programs into RISC-V Instructions
When we implement a C program on hardware, it undergoes a series of transformations before it can be executed by the processor. The process can be summarized as follows:
**Step 1: Writing the C Code**
First, we write the program in C, which is easy for humans to understand.

**Step 2: Compiling to Assembly**
The compiler converts the C code into RISC-V assembly language.
Assembly is still readable, but it’s much closer to what the hardware can understand.

**Step 3: Assembling to Machine Code**
The assembler changes the assembly code into machine code, which is in binary (1s and 0s).
For convenience, we often write this in hexadecimal, but the processor only understands the binary version.

**Step 4: Running on Hardware**
Finally, this machine code is loaded onto the processor, which can now execute the program exactly and precisiely.


## How Apps run on Hardware
1. The Role of System Software All apps first enter a box called system software. This includes:
• Operating System (OS)
• Compiler
• Assembler The system software acts as a bridge between your app and the computer hardware, making sure your instructions are understood and executed correctly.
2. What the Operating System Does The OS is like the **manager of the computer. It handles
• Input/Output (I/O) operation**: Makes sure the app can interact with devices like the keyboard, mouse, or screen. Allocates memory: Gives space to the app to store and process data.
Prepares instructions: Converts app code into assembly language, a lower-level language that the computer hardware can work with.
3. What the Compiler Does After the OS processes the app, the compiler takes over. Its job is to: Convert the high-level code (C, C++, Java, etc.) into hardware-specific instructions. Makeing sure the program runs efficiently on the processor architecture. This is important because the same C code could work on different hardware, but the compiler ensures it is translated correctly for each one.
4. What the Assembler Does Next comes the assembler, which **converts these instructions into binary code** - the Os and 1s that the hardware can understand. These binary instructions control the processor, memory, and other components. As of now our app exists only as electrical signals inside the computer.
Let's look at this with an exampleof a **Stopwatch App** we write the code in C language. The app enters system software: The OS handles I/O and memory, and prepares the instructions. The compiler converts C into hardware instructions. The assembler converts instructions into binary. The binary instructions now run on the hardware, controlling the processor and displaying the stopwatch on your screen.
**Why is this called "architecture"?** These instructions form the big structure of the computer, guiding the hardware on how to execute the app.

When we write a program and it finally reaches the hardware, there’s an important step in between called RTL — Register Transfer Level. It acts as the bridge between the instructions defined by the architecture (like RISC-V) and the actual physical circuits in the processor.

**What is RTL?**
RTL **(Register Transfer Level)** is a way to describe how data moves inside the processor.
It defines:
- How registers (small storage units) store values.
- How operations like addition, subtraction, or multiplication are performed.
- How data flows between different parts of the CPU.

RTL is usually written in a Hardware Description Language (HDL) like Verilog.

When a program finally reaches the compiler, the compiler converts high-level code into RISC-V instructions.
**Pseudo Instructions**
The output of the compiler usually contains pseudo instructions.
These are:
- Helper instructions for the programmer
- But not understood by the CPU directly

**Base Integer Instructions (RV64I)**
These are:
- The real, fundamental instructions
- Part of RV64I (RISC-V 64-bit Integer Base ISA)
- Fully understood by the CPU

**ABI (Application Binary Interface)**
The ABI decides:

- How registers are used
- How functions work
- How arguments are passed
- How the program talks to the OS and hardware
The ABI ensures all programs, compilers, and hardware follow the same rules.
after following the ABI rules, each RISC-V instruction is converted into a bit pattern.

**Word, Doubleword, MSB, LSB**
In RISC-V:
32-bit value = word
64-bit value = doubleword

RISC-V RV64I supports 64-bit processors, so most operations use doubleword values.

Every binary value has two ends:
**LSB (Least Significant Bit)** - the rightmost bit, smallest value

**MSB (Most Significant Bit)** - the leftmost bit, largest value

## Two's Complement 
When programs run on hardware, the CPU has both positive and negative numbers.
RISC-V uses *Two’s Complement Representation*.

To convert a positive number into its negative equivalent, the processor follows these steps:
Let us start with the positive number’s binary form
**Invert all bits**
0 → 1
1 → 0
**Add 1 to the result**
This gives the two’s complement form of the number, which is the standard way to represent negatives inside the CPU.
Example idea:
Numbers like –1,152,991,877,645,991,936 would be converted by taking its binary, inverting, and adding 1.
Two’s complement uses the MSB (Most Significant Bit) as the sign bit:
**MSB = 0 → Positive number
MSB = 1 → Negative number**
This rule stays true for:
- 32-bit values (word)
- 64-bit values (doubleword)
This is why two’s complement integrates with binary representation.
- Adding two large positives overflows into the negative region
- Adding two negatives overflow into the positive region
Overflow happens because the result cannot fit in the fixed number of bits.

## How Numbers Are Loaded Into Registers
There are two ways to load values into registers:
- **Method 1:** Loading Directly
The instruction itself contains the data.
But the limitations are that -
- Works for small values only
- Cannot store full 64-bit numbers directly

-  **Method 2:** Loading Through Memory
Used when the data is too large for an immediate.
Large 64-bit Value → Stored in Memory → Register
This method handles very large constants, like full 64-bit values.

### **Little Endian Storage**

In little-endian, the Least Significant Byte (LSB) is stored at the lowest memory address, and the next bytes follow upward.
Example (Little Endian):
Suppose we store a 64-bit number at address m(0).
Memory layout:
Address	Contains
m(0)	LSB
m(1)	Next byte
m(2)	Next byte
m(3)	Next byte
m(4)	Next byte
m(5)	Next byte
m(6)	Next byte
m(7)	MSB

*This ordering—LSB first → MSB last—is called little endian.*
- **Middle Endian** 
Middle endian is the reverse:
- MSB at the lowest address
- LSB at the highest address
But this is not that iportant as this is not in RISC V 

### How Doublewords Are Arranged in Memory
Each doubleword is 8 bytes.
So they must start at memory locations spaced 8 bytes apart.
If the 1st doubleword starts at
m(0)
then the next ones are:
Doubleword	Starting Address
1st	m(0)
2nd	m(8)
3rd	m(16)
4th	m(24)
Since  each doubleword occupies 8 bytes.

