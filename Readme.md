# This is my first repository

## Table of content

[Day 0](https://github.com/ariefsulaiman/sd-training/blob/main/Day0.md#day-0)


## Day 0
### Topic - System/Tool Setup Check. GitHub ID creation
The term **"IC packaging"** describes the material that holds a semiconductor device. The circuit material is enclosed in a package to prevent rust or physical damage and to enable attachment of the electrical contacts linking it to the printed circuit board (PCB). There are many different types of integrated circuits, and as a result, there are many IC packaging system designs to take into account. This is because various circuit designs will require various requirements for their exterior casing.\
Example of package - Quadruple in-line package (QIP) and Dual in-line package (DIP).

![image](https://user-images.githubusercontent.com/118953928/203929575-c1a4f6b4-530c-4778-bda4-69649a140961.png)
![image](https://user-images.githubusercontent.com/118953928/203929823-5436c544-0933-4c5f-b9b6-09d5637fb1ab.png)

**Pad** - used to connect inside (core) to outside (I/O), good at ESD protection to prevent charge coming from outside damage the core inside.\
**Core** - consists of all the main logic gate (NMOS/PMOS) and cell block such as macro cell and foundry IP's.\
**I/O** - help in communication between die with external and will be connected to die by using wire bonding.\
**Wire Bonding** - method of making interconnections between an integrated circuit (IC) or other semiconductor device and its packaging during semiconductor device fabrication.\
**Macro** - a simple core/cell with simple functionality and can be easily found online.\
**Foundry IP's** - cell with more specific functionality and the design was patent/owned by a company. Has higher value compared to macro.\


**Synthesis Flow**\
Convert software's instructions which is written in high level language to gate level language/machine language which is normally in binary format.
![image](https://user-images.githubusercontent.com/118953928/203932543-03c7cf3e-1d1c-4771-98bd-f1b03b06856e.png)
Specification/instructions written in RTL (high-level language such as C, C++ or Java) as inputs.
Compiler will compile the instruction into assembly language (.exe).
Assembler will then convert assembly language into gate level language (low-level language.machine language) which is in binary format (operands), and it is the language understood by a computer.


### Lab
![](Day0.jpg)

