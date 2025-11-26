# RISK-V-a-Learning-Journey-for-High-Schoolers
This repository explores how a C program transforms into hardware through RISC-V, ISA, RTL, and related concepts. We start from the basics and gradually dive deeper to understand every layer of the RISC-V ecosystem, from software instructions to actual processor execution.
## Introduction to RISC-V
RISC-V RISC-V stands for Reduced Instruction Set Computer, it has small and simple instructions which makes hardware design easier to implement it is an Open source Instruction Set Architecutre (ISA) used for designing the computers.
ISA ISA as we previously saw stands for Instruction Set Architecture it defines the instructions the porcessor understands and how it manipulates the data. It is the language of the computer and they way we'll talk to the computer. ISA acts asa bridge between the software and the hardware and makes it easier to communicate between these two. It tells us -
• What Instructions Exist
• How to format them
• How a CPU should execute them


## How Apps run on Hardware
1. The Role of System Software All apps first enter a box called system software. This includes:
• Operating System (OS)
• Compiler
• Assembler The system software acts as a bridge between your app and the computer hardware, making sure your instructions are understood and executed correctly.
2. What the Operating System Does The OS is like the manager of the computer. It handles
• Input/Output (I/O) operation**s: Makes sure the app can interact with devices like the keyboard, mouse, or screen. Allocates memory: Gives space to the app to store and process data.
Prepares instructions: Converts app code into assembly language, a lower-level language that the computer hardware can work with.
3. What the Compiler Does After the OS processes the app, the compiler takes over. Its job is to: Convert the high-level code (C, C++, Java, etc.) into hardware-specific instructions. Makeing sure the program runs efficiently on the processor architecture. This is important because the same C code could work on different hardware, but the compiler ensures it is translated correctly for each one.
4. What the Assembler Does Next comes the assembler, which converts these instructions into binary code - the Os and 1s that the hardware can understand. These binary instructions control the processor, memory, and other components. As of now our app exists only as electrical signals inside the computer.
Let's look at this with an exampleof a Stopwatch App You write the code in C language. The app enters system software: The OS handles I/O and memory, and prepares the instructions. The compiler converts C into hardware instructions. The assembler converts instructions into binary. The binary instructions now run on the hardware, controlling the processor and displaying the stopwatch on your screen.
**Why is this called "architecture"?** These instructions form the big structure of the computer, guiding the hardware on how to execute the app.
