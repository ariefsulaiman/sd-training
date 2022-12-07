# This is my first repository

## Table of content

[Day 0 - System/Tool Setup Check. GitHub ID creation](https://github.com/ariefsulaiman/sd-training/blob/main/Readme.md#day-0)\
[Day 1 - Introduction to Verilog RTL design and Synthesis](https://github.com/ariefsulaiman/sd-training/edit/main/Readme.md#day-1)

## Day 0
### Topic - System/Tool Setup Check. GitHub ID creation
### Theory
The term **"IC packaging"** describes the material that holds a semiconductor device. The circuit material is enclosed in a package to prevent rust or physical damage and to enable attachment of the electrical contacts linking it to the printed circuit board (PCB). There are many different types of integrated circuits, and as a result, there are many IC packaging system designs to take into account. This is because various circuit designs will require various requirements for their exterior casing.\
Example of package - Quadruple in-line package (QIP) and Dual in-line package (DIP).

![image](https://user-images.githubusercontent.com/118953928/203929575-c1a4f6b4-530c-4778-bda4-69649a140961.png)
![image](https://user-images.githubusercontent.com/118953928/203929823-5436c544-0933-4c5f-b9b6-09d5637fb1ab.png)

**Pad** - used to connect inside (core) to outside (I/O), good at ESD protection to prevent charge coming from outside damage the core inside.\
**Core** - consists of all the main logic gate (NMOS/PMOS) and cell block such as macro cell and foundry IP's.\
**I/O** - help in communication between die with external and will be connected to die by using wire bonding.\
**Wire Bonding** - method of making interconnections between an integrated circuit (IC) or other semiconductor device and its packaging during semiconductor device fabrication.\
**Macro** - a simple core/cell with simple functionality and can be easily found online.\
**Foundry IP's** - cell with more specific functionality and the design was patent/owned by a company. Has higher value compared to macro.


**Synthesis Flow**\
Convert software's instructions which is written in high level language to gate level language/machine language which is normally in binary format.
![image](https://user-images.githubusercontent.com/118953928/203932543-03c7cf3e-1d1c-4771-98bd-f1b03b06856e.png)
Specification/instructions written in RTL (high-level language such as C, C++ or Java) as inputs.
Compiler will compile the instruction into assembly language (.exe).
Assembler will then convert assembly language into gate level language (low-level language.machine language) which is in binary format (operands), and it is the language understood by a computer.


### Lab
![Day0](https://user-images.githubusercontent.com/118953928/205473351-53f8d06d-b517-41cb-832d-c3b92b0b8233.jpg)

## Day 1 
### Topic - Introduction to Verilog RTL design and Synthesis
### Theory
* **Design** is a set of Verilog code for the design work as intended.
* **RTL Design** is the behavioural representation of the required specification.
* **Simulator** is a method to check design and simulate the design. In this topic, the tool used is iverilog.
* **Testbench** is the setup of test vector to check it output match with the specs to test the functionality.
* **IVerilog** is a Verilog simulation and synthesis tool that is available for free. it take a design and a testbench as a input and it converts Verilog source code into a value change dump format (VCD file).
* **GTKWave** is a fully featured GTK+ wave reader for Unix, Win32, and Mac OSX that reads and displays LXT, LXT2, VZT, FST, and GHW and Verilog VCD/EVCD files. GTKWave is the best open source free wave viewer and the IVerilog developer recommends to use it.
* **Synthesizer** is a tool used for converting RTL to Netlist. In this topic, the synthesizer used is Yosys.
* **Yosys** is a framework for Verilog RTL synthesis. it takes a design and a .lib and it converts it into a netlist file.

* **Synthesis** is the process to converting RTL to gate level translation. The design is converted into gate. The connections are made between gates. The output of this process is called netlist.

What is .lib?
* A LIB file is a documentation of timing and power parameters related with cells in a technology node's standard cell library. A lib file is mainly a timing model file that comprises the cell delay, cell transition time, setup and hold time requirements. It may contain variation of a single cell. For example, slow medium and fast cell.

Why do we need variation of cell?
* Slow, fast and medium synthesis libraries are provided for timing-based synthesis. The slow lib is used for Hold time and the fast lib is used for Setup time checks. Achieve a maximum clock speed (minimum clock period), means better performance.  But that not always true because it should not too fast because hold violation might happen. So sometimes we need cell that can work slowly. 

How to get a faster/slower cells
* In digital logic circuit, to get a faster cell the charge-discharge of a capacitance need to be fast. To get a faster charge-discharge of a capacitance the transistor needs to be bigger to be able of sourcing more current. The wider transistor means more area and power it gets. There will always be a trade of between speed, area and power.

| Faster cell  | Slower cells |
| ------------- | ------------- |
| Low Delay  | More Delay  |
| Wider Transistor  | Narrow Transistor  |
| More Area  | Less Area  |
| More Power  | Less Power |


### Lab using Iverilog and Gtkwave
**Lab 1: Introduction to lab** 

Task --> Cloning the directory from Github into machine
![image](https://user-images.githubusercontent.com/118953928/205473699-d51db95c-31fe-4583-b6fd-bfe48b1a1c62.png)

**Lab 2: Introduction iverilog gtkwave part 1** 

Task --> Setting up and opening the GTKwave\
The verilog file and testbench need to be compile by iverilog to create a a.out. Executing a.out to create vcd file for the GTKwave to read the file.
![image](https://user-images.githubusercontent.com/118953928/205474522-5ff4bd08-2950-4745-ab93-f5dc98cf919b.png)
![image](https://user-images.githubusercontent.com/118953928/205474452-7bdd8af4-8a20-4549-a897-1267c5663269.png)

**Lab 2: Introduction iverilog gtkwave part 2** 

Task --> Open the design file and the testbench file\
![image](https://user-images.githubusercontent.com/118953928/205474955-6169a528-89d9-4842-bb40-f536162e729d.png)
![image](https://user-images.githubusercontent.com/118953928/205474904-bd3460b3-f911-42e9-92f5-3492da540a15.png)

**Summary of command used**
| Command  | Detail |
| ------------- | ------------- |
| git clone \<linkfromgithub> | Copying the directory from Github into the machine  |
| iverilog good_mux.v tb_good_mux.v  |  Compile verilog design and testbench and create a.out file |
| ./a.out  | Run the simulation. vcd file is created  |
| gtkwave tb_good_mux.vcd  | View the simulation results graphically |

### Lab using Yosys and Sky130 PDKs
**Lab 3: Good mux Part 1** 
Task --> Opening up Yosys\
![yosys](https://user-images.githubusercontent.com/118953928/205495328-f2b7ee41-6f4a-41a3-88e5-bbb2715046c8.JPG)

Task --> Read library, Read design, Synthesis, Generate netlists for the specified cell library, Display logic circuit 
![image](https://user-images.githubusercontent.com/118953928/205495758-f4c95477-6352-468f-afba-ff9bfdb3eab0.png)
![show](https://user-images.githubusercontent.com/118953928/205496208-f9e15299-ce6c-4de1-a3cf-1a6ccbc28eed.JPG)


**Command used**
| Command  | Detail |
| ------------- | ------------- |
| read_liberty -lib ../my_lib/lib/sky*.lib | Read library  |
| read_verilog good_mux.v  |  Read design |
| synth -top good_mux  | Synthesis  |
| abc -liberty ../lib/sky*.lib  | Generate netlists for the specified cell library |
| show  | Display logic circuit |

**Lab 3: Good mux Part 2** \
Task --> Understanding the logic circuit\
The circuit from the video is different from my result when showing the logic circuit. The logic circuit on the video show there is 1 nand, 1 clk inverter and and 1 02ai gate. My logic just show a whole block of mux. I think because there a Mux2x1 in the standard cell library so, there is no need divide for each logic gate for the same function.

**Lab 3: Good mux Part 3** \
Task --> write netlist, open netlist in vim\
![image](https://user-images.githubusercontent.com/118953928/205530077-76f2415f-9395-4382-bcde-d8bcaf1702ea.png)
![image](https://user-images.githubusercontent.com/118953928/205529961-5039b4ae-e1f4-4f02-91d2-c3223c1b8ae5.png)

Task --> Simplify netlist, open simplify netlist in vim\
![image](https://user-images.githubusercontent.com/118953928/205530977-bbb4cc7c-29dd-46f0-98f6-13f33b9e53ee.png)
![image](https://user-images.githubusercontent.com/118953928/205530696-f1c08a2f-260d-4edd-9a51-ab765747d951.png)

**Command used**
| Command  | Detail |
| ------------- | ------------- |
| write_verilog good_mux_netlist.v | Generate the netlist.v  |
| !vim good_mux_netlist.v  |  Open the generated netlist |
| write_verilog -noattr good_mux_netlist.v  | Simplify the netlist  |

## Day 2 
### Topic - Timing libs(QTMs/ETMs), hierarchical vs flat synthesis and efficient flop coding styles
### Theory & Lab
#### Lab Topic: Introduction to timing.lib
> 1. Structure of .lib
![Slide1](https://user-images.githubusercontent.com/118953928/206137095-3ebec90c-93ce-4fb5-8d1f-ebb0b9caaf7c.JPG) 

> 2. Variation of cells in .lib
![Slide2](https://user-images.githubusercontent.com/118953928/206137566-7766f8be-4773-4639-8baf-4edb2ca412c0.JPG)

> 3. Behavioral code of the cell inside .lib
![Slide3](https://user-images.githubusercontent.com/118953928/206137854-c5bd555f-6603-466e-9dbb-7d64a9ff66f1.JPG)

> 4. Cell information from the verilog model structure
![Slide4](https://user-images.githubusercontent.com/118953928/206138828-932f5ec7-f87c-4fb1-af37-9bcc2cef0868.JPG)
![Slide5](https://user-images.githubusercontent.com/118953928/206138884-1624071d-fcc1-4a0f-8fc2-8472a2f5c5fe.JPG)
![Slide6](https://user-images.githubusercontent.com/118953928/206138911-3ba7e73a-696d-4b1e-a756-2e8bd64a6a93.JPG)
![Slide7](https://user-images.githubusercontent.com/118953928/206138953-0ef3b587-f741-40e8-ad79-44fa546504dc.JPG)

> 5. 
![Slide8](https://user-images.githubusercontent.com/118953928/206139251-5d402e51-e8af-4fef-a9dd-b491e2e00f9b.JPG)

#### Lab Topic: Hierarchy vs flat synthesis
> 1. Opening & understanding multiple module
![Slide10](https://user-images.githubusercontent.com/118953928/206141163-bf473bc1-6ec1-422c-8144-b2c653956b0e.JPG)

> 2. Synthesis of the mutiples_module  
![Slide11](https://user-images.githubusercontent.com/118953928/206141431-fd95d8c1-d75d-4858-9e36-25d6fa5f3d80.JPG)
![Slide12](https://user-images.githubusercontent.com/118953928/206141606-5eb3b4ca-c44f-4c24-aabc-651399d64f21.JPG)
![Slide13](https://user-images.githubusercontent.com/118953928/206141624-3be9de33-6b54-4c8c-9c4d-66fe5fb32fcc.JPG)


> 3. 



#### Lab Topic: -





