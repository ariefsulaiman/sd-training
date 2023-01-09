# This is my first repository

## Table of content

[Day 0 - System/Tool Setup Check. GitHub ID creation](https://github.com/ariefsulaiman/sd-training/blob/main/Readme.md#day-0---systemtool-setup-check-github-id-creation)\
[Day 1 - Introduction to Verilog RTL design and Synthesis](https://github.com/ariefsulaiman/sd-training/blob/main/Readme.md#day-1---introduction-to-verilog-rtl-design-and-synthesis)\
[Day 2 - Timing libs(QTMs/ETMs), hierarchical vs flat synthesis and efficient flop coding styles](https://github.com/ariefsulaiman/sd-training/blob/main/Readme.md#day-2---timing-libsqtmsetms-hierarchical-vs-flat-synthesis-and-efficient-flop-coding-styles)\
[Day 3 - Combinational and Sequential Optimizations](https://github.com/ariefsulaiman/sd-training/blob/main/Readme.md#day-3---combinational-and-sequential-optimizations)\
[Day 4 - GLS, blocking vs non-blocking and Synthesis-Simulation mismatch](https://github.com/ariefsulaiman/sd-training/blob/main/Readme.md#day-4---gls-blocking-vs-non-blocking-and-synthesis-simulation-mismatch)\
[Day 5 - DFT](https://github.com/ariefsulaiman/sd-training/blob/main/Readme.md#day-5---dft)\
[Day 6 - Introduction to Logic Synthesis](https://github.com/ariefsulaiman/sd-training#day-6---introduction-to-logic-synthesis)\
[Day 7 - Basics of STA](https://github.com/ariefsulaiman/sd-training#day-7---basics-of-sta)\
[Day 8 - Advanced constraints](https://github.com/ariefsulaiman/sd-training/blob/main/Readme.md#day-8---advanced-constraints)\
[Day 9 - Optimization](https://github.com/ariefsulaiman/sd-training/blob/main/Readme.md#day-9---optimization)\
[Day 10 - Timing Models](https://github.com/ariefsulaiman/sd-training/blob/main/Readme.md#day-10---quality-checks)\
[Day 11 - Introduction to the BabySoC](https://github.com/ariefsulaiman/sd-training/blob/main/Readme.md#day-11----introduction-to-the-babysoc)\
[Day 12 - Module 12: BabySoC Modelling ](https://github.com/ariefsulaiman/sd-training/blob/main/Readme.md#day-12----babysoc-modelling)\
[Day 13 - Post-synthesis simulation](https://github.com/ariefsulaiman/sd-training/blob/main/Readme.md#day-13----post-synthesis-simulation)


## Day 0 - System/Tool Setup Check. GitHub ID creation
<details>
  <summary>Theory</summary>
 

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
</details>

<details>
  <summary>Lab</summary>
 
### Lab
![Day0](https://user-images.githubusercontent.com/118953928/205473351-53f8d06d-b517-41cb-832d-c3b92b0b8233.jpg)
 
  </details>

## Day 1 - Introduction to Verilog RTL design and Synthesis
<details>
  <summary>Theory</summary>
 

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
</details>
 
<details>
  <summary>Lab using Iverilog and Gtkwave</summary>  

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
</details>
    
    
<details>
  <summary>Lab using Yosys and Sky130 PDKs</summary>  
  
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
</details>

 
 
## Day 2 - Timing libs(QTMs/ETMs), hierarchical vs flat synthesis and efficient flop coding styles
<details>
  <summary>Lab Topic: Introduction to timing.lib</summary>
  
#### Lab Topic: Introduction to timing.lib

> 1. Structure of .lib
- vim../my_lib/lib/sky130_fd_sc_hd_tt_025C_1v80.lib --> Open the .lib
- :syn off --->switch off the syntax --> Turn off syntax colour
![Slide1](https://user-images.githubusercontent.com/118953928/206137095-3ebec90c-93ce-4fb5-8d1f-ebb0b9caaf7c.JPG) 
> > Note\
Tt: typical(fast/slow/typical)\
C= temperature\
V= voltage

> 2. Variation of cells in .lib
- :vsp ../my_lib/verilog_model/sky130_fd_sc_hd.v --> Open the file that conatin all detail and behavioural 
![Slide2](https://user-images.githubusercontent.com/118953928/206137566-7766f8be-4773-4639-8baf-4edb2ca412c0.JPG)

> 3. Behavioral code of the cell inside .lib
![Slide3](https://user-images.githubusercontent.com/118953928/206137854-c5bd555f-6603-466e-9dbb-7d64a9ff66f1.JPG)

> 4. Cell information from the verilog model structure
![Slide4](https://user-images.githubusercontent.com/118953928/206138828-932f5ec7-f87c-4fb1-af37-9bcc2cef0868.JPG)
![Slide5](https://user-images.githubusercontent.com/118953928/206138884-1624071d-fcc1-4a0f-8fc2-8472a2f5c5fe.JPG)
![Slide6](https://user-images.githubusercontent.com/118953928/206138911-3ba7e73a-696d-4b1e-a756-2e8bd64a6a93.JPG)
![Slide7](https://user-images.githubusercontent.com/118953928/206138953-0ef3b587-f741-40e8-ad79-44fa546504dc.JPG)

> 5. Variation of cells 
![Slide8](https://user-images.githubusercontent.com/118953928/206139251-5d402e51-e8af-4fef-a9dd-b491e2e00f9b.JPG)
</details>
  
  <details>
  <summary>Lab Topic: Hierarchy vs flat synthesis</summary>

> 1. Opening & understanding multiple module
Command : Gvim multiple_module.v
![Slide10](https://user-images.githubusercontent.com/118953928/206141163-bf473bc1-6ec1-422c-8144-b2c653956b0e.JPG)

> 2. Synthesis of the mutiples_modules\
- Command:\
![image](https://user-images.githubusercontent.com/118953928/206324204-07a98b64-97ed-4249-b865-41c744635086.png)
- Result\
![Slide11](https://user-images.githubusercontent.com/118953928/206141431-fd95d8c1-d75d-4858-9e36-25d6fa5f3d80.JPG)
![Slide12](https://user-images.githubusercontent.com/118953928/206141606-5eb3b4ca-c44f-4c24-aabc-651399d64f21.JPG)
![Slide13](https://user-images.githubusercontent.com/118953928/206141624-3be9de33-6b54-4c8c-9c4d-66fe5fb32fcc.JPG)


> 3. Revision
![Slide14](https://user-images.githubusercontent.com/118953928/206142219-cd6ca58e-eba7-47de-b4b3-def8389733b7.JPG)
![Slide15](https://user-images.githubusercontent.com/118953928/206142232-04f06038-e6a3-4ebe-af71-7b0a8ba1d07c.JPG)

> 4. Flatten the multiple_modules
- Code
![image](https://user-images.githubusercontent.com/118953928/206327140-c5782660-28bd-4ce1-a816-c8745c15adcc.png)

- Result
![Slide17](https://user-images.githubusercontent.com/118953928/206142853-3fb1077f-66ec-4889-b5c1-30051c572806.JPG)

> 5. Synthesizing sub module from the multiple_modules.v
![Slide18](https://user-images.githubusercontent.com/118953928/206143146-e0457ba3-8d37-492d-a0c1-81cb3b61c974.JPG)
</details>
  
<details>
  <summary>Lab Topic: Various Flop Coding Styles and Optimization</summary>

> 1. Flip-flop
![Slide19](https://user-images.githubusercontent.com/118953928/206143268-69ceaa31-11a7-4247-a29a-d0207a38e90f.JPG)

> 2. Asynchronous D-flip-flop
![Slide20](https://user-images.githubusercontent.com/118953928/206143520-1255fd04-4a40-424c-a237-032e2c787a95.JPG)

> 3. Synchronous D-flip-flop 
 ![Slide21](https://user-images.githubusercontent.com/118953928/206143701-d312c8cc-ab25-45b7-82cc-1550dac40601.JPG)
 
> 4. Simulating asynchronous D-flip-flop (reset)
![Slide22](https://user-images.githubusercontent.com/118953928/206145248-1ae21d67-2b54-4b78-aec0-c8901a992726.JPG)

> 5. Simulating asynchronous D-flip-flop (set)
![Slide23](https://user-images.githubusercontent.com/118953928/206145497-e9dc8277-071a-4c43-ada1-ccc73f99ace2.JPG)

> 6. Simulating synchronous D-flip-flop (set)
![Slide24](https://user-images.githubusercontent.com/118953928/206146136-f453b94e-d04f-49cd-b48c-20b9dbcf3a2c.JPG)

> 7. Synthesis asynchronous D-flip-flop (reset)
- Coding
![image](https://user-images.githubusercontent.com/118953928/206331269-3758d609-38e0-4574-9a23-3107c91b9fbf.png)

- Result
![Slide25](https://user-images.githubusercontent.com/118953928/206146468-6dfa53aa-176d-453a-b616-eb564bcf1226.JPG)

> 8. Synthesis asynchronous D-flip-flop (set)
- Coding
![image](https://user-images.githubusercontent.com/118953928/206332007-7e17fbb5-0cc7-4706-8376-7241cc3a6c52.png)

- Result
![Slide26](https://user-images.githubusercontent.com/118953928/206146624-4c772154-6d39-4e27-94c3-672f8ed407f8.JPG)

> 9. Synthesis synchronous D-flip-flop (set)
- Coding
![image](https://user-images.githubusercontent.com/118953928/206332774-93ae20f7-76f0-4180-aee8-06aef2f28db5.png)

- Result
![Slide27](https://user-images.githubusercontent.com/118953928/206146881-9e14fce8-a6f1-4e8b-ada4-0e6893208aa2.JPG)

> 10. Interesting optimization of mult2 & mult8
![Slide29](https://user-images.githubusercontent.com/118953928/206148279-9ad0b948-e6a5-46d8-b144-59accbf662dd.JPG)

> 11. Synthesis of mult2
- Coding
![image](https://user-images.githubusercontent.com/118953928/206333632-ecda2517-5acc-4139-869c-d4282ebe9112.png)

- Result
![Slide30](https://user-images.githubusercontent.com/118953928/206148447-51663683-b8e6-4bbc-ac26-a01c7d6efec7.JPG)

> 12. Interesting optimization of mult8
![Slide31](https://user-images.githubusercontent.com/118953928/206148687-291127bd-d7db-4af5-9321-5e4588dd5dfd.JPG)

> 13. Synthesis of mult8
- Coding
![image](https://user-images.githubusercontent.com/118953928/206334190-689c0da2-029d-4be5-82ad-b495b0ede65d.png)

- Result
![Slide32](https://user-images.githubusercontent.com/118953928/206148944-64e5a680-2385-48f5-bf21-22e22dbad88c.JPG)
</details>
  
## Day 3 - Combinational and sequential optimizations

<details>
  <summary>Lab Topic: Introduction To Optimization</summary>  

> Combinational Logic Optimization
![Slide2](https://user-images.githubusercontent.com/118953928/206737731-3b98b2c1-5cc1-4d5c-8bea-f80e394e3f51.JPG)
![Slide3](https://user-images.githubusercontent.com/118953928/206737745-294ff8f0-c640-4aec-8b93-4d37092f7ad5.JPG)
![Slide4](https://user-images.githubusercontent.com/118953928/206737755-7fa69913-b322-4f3e-bb75-4271992ed91b.JPG)

> Sequential Constant Optimization (D-FF with reset signal)
![Slide5](https://user-images.githubusercontent.com/118953928/206738058-c1fa725f-dce3-4970-a66f-49a9ca483a24.JPG)

> Sequential Constant Optimization (D-FF with set signal)
![Slide6](https://user-images.githubusercontent.com/118953928/206738071-79327fe0-fe76-4c31-9efd-2b09197664a0.JPG)

> State Optimization 
![Slide7](https://user-images.githubusercontent.com/118953928/206738105-e6aa77a0-7cc5-4856-9814-5a200b8509d5.JPG)
</details>
  
<details>
  <summary>Lab Topic: Combinational Logic Optimization</summary>

> opt_check.v
![Slide9](https://user-images.githubusercontent.com/118953928/206738385-fe0c1beb-2bd2-46ef-885e-075936e0fa5b.JPG)
![Slide10](https://user-images.githubusercontent.com/118953928/206738396-00a40586-19a3-41f3-ae38-383a53e51700.JPG)
![Slide11](https://user-images.githubusercontent.com/118953928/206738406-be0f1c3f-0f63-4056-8571-b4638e577a6f.JPG)

> opt_check2.v
![Slide12](https://user-images.githubusercontent.com/118953928/206738487-c8037e3e-52b4-4c6c-9acd-17a501013462.JPG)
![Slide13](https://user-images.githubusercontent.com/118953928/206738495-62658e89-7acb-4710-9999-51dd3ba71f01.JPG)
![Slide14](https://user-images.githubusercontent.com/118953928/206738501-a1808382-252e-4d1d-8c2c-bf1940f752d0.JPG)

> opt_check3.v
![Slide15](https://user-images.githubusercontent.com/118953928/206738616-724c88cb-bf4d-4e1c-8f01-8485ddd501d6.JPG)
![Slide16](https://user-images.githubusercontent.com/118953928/206738623-560d219c-8645-4754-b856-20df1b5f0bc3.JPG)
![Slide17](https://user-images.githubusercontent.com/118953928/206738625-e743d7cd-c7e5-4664-94b9-edb0ef9d2bf6.JPG)

> opt_check4.v
![Slide18](https://user-images.githubusercontent.com/118953928/206738716-5a33c98b-a3cb-42ec-9a73-894f890fd7de.JPG)
![Slide19](https://user-images.githubusercontent.com/118953928/206738721-7e485eb5-85eb-4b43-b268-8c42733aa759.JPG)
![Slide20](https://user-images.githubusercontent.com/118953928/206738723-b9df76d0-df0c-44e1-9324-64d52d311177.JPG)

> Multiple_module_opt.v
![Slide21](https://user-images.githubusercontent.com/118953928/206738793-61878bc5-6e62-4c60-9bdb-dd964d30f5ee.JPG)
![Slide22](https://user-images.githubusercontent.com/118953928/206738805-27ffdd9f-7667-473f-83f2-32586e3b14c0.JPG)
![Slide23](https://user-images.githubusercontent.com/118953928/206738807-6eef66a0-5706-4f33-8634-1db9ea3965d5.JPG)

> Multiple_module_opt2.v
![Slide24](https://user-images.githubusercontent.com/118953928/206738858-625ddf05-3d48-420b-b706-66a3b369749c.JPG)
![Slide25](https://user-images.githubusercontent.com/118953928/206738866-207a2410-32a2-42c2-937f-9565fd0cb450.JPG)
![Slide26](https://user-images.githubusercontent.com/118953928/206738869-dc8c4cb0-e8eb-4589-9a16-0cf357d2ecde.JPG)
</details>
  
<details>
  <summary>Lab Topic: Sequential Logic Optimization</summary>

> dff_const1
![Slide28](https://user-images.githubusercontent.com/118953928/206739222-46dd648a-a549-448c-9f62-08f0a09203cb.JPG)
![Slide29](https://user-images.githubusercontent.com/118953928/206739228-108c3b09-4220-4af5-bc7e-33454160b2fe.JPG)
![Slide30](https://user-images.githubusercontent.com/118953928/206739233-c4dcb61f-9f2c-4803-9020-e4301e76860d.JPG)
![Slide31](https://user-images.githubusercontent.com/118953928/206739235-83e2cea4-f3e0-4999-9a8e-773ba868b1bb.JPG)

> dff_const2
![Slide32](https://user-images.githubusercontent.com/118953928/206739474-f72095c6-ebcb-4f1d-89f0-1bf5dd30951c.JPG)
![Slide33](https://user-images.githubusercontent.com/118953928/206739482-ed833e33-94cb-494a-a768-b43adc19dead.JPG)
![Slide34](https://user-images.githubusercontent.com/118953928/206739485-786f7fdd-b4bd-4f7b-8d10-5c3510b298f6.JPG)
![Slide35](https://user-images.githubusercontent.com/118953928/206739490-610e6cf5-bfa0-4d4b-9b93-f9e421d524c0.JPG)

> dff_const3
![Slide36](https://user-images.githubusercontent.com/118953928/206739643-09d0c2dd-fcde-46d4-93a9-92a5c2aa5e02.JPG)
![Slide37](https://user-images.githubusercontent.com/118953928/206739655-035aa051-035d-43ff-a00c-650ac1e3346b.JPG)
![Slide38](https://user-images.githubusercontent.com/118953928/206739659-73becde7-957f-420e-8baf-65b75981f80c.JPG)
![Slide39](https://user-images.githubusercontent.com/118953928/206739662-d655c9d5-f7cc-4213-83e8-843f2ba4bf11.JPG)

> dff_const4
![Slide40](https://user-images.githubusercontent.com/118953928/206739713-e4e85f6a-2832-4cef-b3f2-ddbf34f8c5ee.JPG)
![Slide41](https://user-images.githubusercontent.com/118953928/206739717-36c7ec57-bfdb-4055-acee-601aa00b449e.JPG)
![Slide42](https://user-images.githubusercontent.com/118953928/206739719-07261030-dddb-420e-a75b-c7af0c923f9b.JPG)
![Slide43](https://user-images.githubusercontent.com/118953928/206739722-7f572319-b2b2-4269-86ed-d72b37333dc4.JPG)

> dff_const5
![Slide44](https://user-images.githubusercontent.com/118953928/206739766-1d8ce70b-073f-4b97-9e76-d7052c506608.JPG)
![Slide45](https://user-images.githubusercontent.com/118953928/206739775-5e5725c9-b9a0-4c75-99e5-24e4edb39a83.JPG)
![Slide46](https://user-images.githubusercontent.com/118953928/206739781-c1b8b53f-4eea-44d0-88f3-2bf7cb3d9160.JPG)
![Slide47](https://user-images.githubusercontent.com/118953928/206739785-3eba604c-7892-43d8-bb09-f91075c0c4bd.JPG)
</details>
  
<details>
  <summary>Lab Topic: Sequential Optimization Unused Outputs</summary>

> **counter_opt.v**
![Slide49](https://user-images.githubusercontent.com/118953928/206739924-9988c8eb-f008-4f2b-a282-5aa73bea282a.JPG)
![Slide50](https://user-images.githubusercontent.com/118953928/206739933-19df3873-8f23-49a8-ba05-556f9c81799b.JPG)
![Slide51](https://user-images.githubusercontent.com/118953928/206739937-82685d9d-a23f-4f54-83bb-34d1e8c1b7f6.JPG)

> **counter_opt2.v**
![Slide52](https://user-images.githubusercontent.com/118953928/206739953-88acd904-7377-4b41-8a06-b7602be7d4cd.JPG)
![Slide53](https://user-images.githubusercontent.com/118953928/206739964-48748c46-eee3-4611-b230-dc944a6ce089.JPG)
![Slide54](https://user-images.githubusercontent.com/118953928/206739969-b20824ca-a468-4b9c-a6af-c7b4e3e3f1fc.JPG)
</details>

## Day 4 - GLS, blocking vs non-blocking and Synthesis-Simulation mismatch

<details>
  <summary>SKY130RTL D4SK1 - GLS, Synthesis-Simulation mismatch and Blocking/Non-blocking statements</summary>
  
> Gate Level Simulation (GLS)
  ![Slide2](https://user-images.githubusercontent.com/118953928/206896202-9096e485-05f3-447d-ba9b-0cdd51a89329.JPG)
  ![Slide3](https://user-images.githubusercontent.com/118953928/206896214-e1f84ff7-e8c6-4d74-b88f-dfc8785829d5.JPG)

> Synthesis Simulation Mismatch
![Slide4](https://user-images.githubusercontent.com/118953928/206896259-33d81798-317a-4244-adfe-b9a385d3d28c.JPG)
![Slide5](https://user-images.githubusercontent.com/118953928/206896261-e2b9485a-0c0f-4095-9b95-d23f4ad27270.JPG)

> Caveat with Blocking Statement
![Slide6](https://user-images.githubusercontent.com/118953928/206896280-f13fc9f1-db05-44cd-82f1-9a73ac57ec7c.JPG)
</details>

<details>
  <summary>SKY130RTL D4SK2 - Labs on GLS and Synthesis-Simulation Mismatch</summary>
  
> ternary_operator_mux.v
![Slide8](https://user-images.githubusercontent.com/118953928/206896341-a343fd4f-772b-4c84-b99d-847be1cea6a9.JPG)
![Slide9](https://user-images.githubusercontent.com/118953928/206896342-24ac97fe-5df6-4e6a-845d-aab6178335a7.JPG)
![Slide10](https://user-images.githubusercontent.com/118953928/206896343-b5e55d4d-92be-4c62-ad30-3a535cee8adb.JPG)
![Slide11](https://user-images.githubusercontent.com/118953928/206896344-c59a9273-86c6-492f-a197-45122a5f04a5.JPG)
![Slide12](https://user-images.githubusercontent.com/118953928/206896345-43670376-a68e-49de-b0e3-b6e27ca13c7f.JPG)

  
> bad_mux.v 
![Slide13](https://user-images.githubusercontent.com/118953928/206896379-277efffe-f224-4913-b810-a8b860418eed.JPG)
![Slide14](https://user-images.githubusercontent.com/118953928/206896382-1b7e158b-a7b7-4c57-bf54-343ecce438a8.JPG)
![Slide15](https://user-images.githubusercontent.com/118953928/206896383-bee1559a-7927-48f4-9ffc-22d1f9320aa7.JPG)
![Slide16](https://user-images.githubusercontent.com/118953928/206896386-984848f3-0573-43d0-994a-f3a761645a6b.JPG)
![Slide17](https://user-images.githubusercontent.com/118953928/206896388-bf5ab0f8-7f94-42e9-b295-ff6727116a3e.JPG)
</details>


<details>
  <summary>SKY130RTL D4SK3 - Labs on synth-sim mismatch for blocking statement</summary>
  
> blocking_caveat,v
![Slide19](https://user-images.githubusercontent.com/118953928/206896424-3eec9110-8095-4408-a567-071bf7a2b628.JPG)
![Slide20](https://user-images.githubusercontent.com/118953928/206896426-44c902d7-7570-409c-b9a0-ab973473b0e8.JPG)
![Slide21](https://user-images.githubusercontent.com/118953928/206896428-9f9223c9-999a-4066-97d5-8658ee021842.JPG)
![Slide22](https://user-images.githubusercontent.com/118953928/206896429-50b0afaa-dc68-4a2f-9cc6-a30389d81160.JPG)
![Slide23](https://user-images.githubusercontent.com/118953928/206896431-5dcdd94c-925e-4ffe-a32b-2f024cd308ba.JPG)
</details>

## Day 5 - DFT
<details>
  <summary>Theory</summary>
  
![NOTE_page-0001](https://user-images.githubusercontent.com/118953928/207774134-36780e59-87df-406f-8b63-e88059134984.jpg)
![NOTE_page-0002](https://user-images.githubusercontent.com/118953928/207774137-a8c22994-59f9-4fcc-817b-b8721634b3f5.jpg)
![NOTE_page-0003](https://user-images.githubusercontent.com/118953928/207774139-6b277ca9-ad78-4f56-919b-246a715128ac.jpg)
![NOTE_page-0004](https://user-images.githubusercontent.com/118953928/207774140-80c88b05-a8f7-4233-b367-2afe48545414.jpg)
![NOTE_page-0005](https://user-images.githubusercontent.com/118953928/207774142-8bdff667-5d0e-49ba-bfb7-87e4dfd04fcb.jpg)
![NOTE_page-0006](https://user-images.githubusercontent.com/118953928/207774145-4719e956-3563-4831-ab8c-81800efda033.jpg)
![NOTE_page-0007](https://user-images.githubusercontent.com/118953928/207774146-1965ac54-84d6-489a-87e8-206102d0689f.jpg)
![NOTE_page-0008](https://user-images.githubusercontent.com/118953928/207774147-5259f349-46d0-476f-80a9-1ecab7d18fbc.jpg)
![NOTE_page-0009](https://user-images.githubusercontent.com/118953928/207774151-2212d469-0045-4ad6-8352-f13e02aadb25.jpg)
![NOTE_page-0010](https://user-images.githubusercontent.com/118953928/207803610-3eee5e1e-11c9-4b6e-8d28-b34e2f06da33.jpg)
![NOTE_page-0011](https://user-images.githubusercontent.com/118953928/207803619-ee155752-933b-4d52-88d5-5c0fbe3274f8.jpg)

  </details>
  

## Day 6 - Introduction to Logic Synthesis

<details>
  <summary>Introduction to the course</summary>
  
  
![Slide2](https://user-images.githubusercontent.com/118953928/208457042-1ce2dc00-4e56-4951-a102-6245cc23bbee.JPG)
![Slide3](https://user-images.githubusercontent.com/118953928/208457050-7c415eda-909d-438b-abeb-d30906b64118.JPG)
![Slide4](https://user-images.githubusercontent.com/118953928/208457057-972819ec-158a-4251-8f15-bf5c66442ad9.JPG)
![Slide5](https://user-images.githubusercontent.com/118953928/208457060-33e6fe96-dcfd-4416-9501-24ded36ccbeb.JPG)
![Slide6](https://user-images.githubusercontent.com/118953928/208457062-4a15e0e8-1497-41e8-ae3f-ce83210efc87.JPG)
</details>
  
  <details>
  <summary>Introduction to DC</summary>
    
![Slide8](https://user-images.githubusercontent.com/118953928/208457254-495162e7-66fc-4f3d-b8ac-a585c9003aa0.JPG)
![Slide9](https://user-images.githubusercontent.com/118953928/208457263-5f0595e5-934f-4223-914c-8e9268cc00b6.JPG)
![Slide10](https://user-images.githubusercontent.com/118953928/208457267-3af6203b-fcf1-4d3c-8cd3-a7cfbd09ce95.JPG)
</details>
  
  <details>
  <summary>Lab 1 - Invoking dc basic setup</summary>
  
![Slide12](https://user-images.githubusercontent.com/118953928/208457416-6029aec6-0e6d-4034-9be3-78d3e0d804ba.JPG)
![Slide13](https://user-images.githubusercontent.com/118953928/208457424-e35b12af-6954-4c0d-9972-c46e79c438a8.JPG)
![Slide14](https://user-images.githubusercontent.com/118953928/208457430-3d364613-c7cc-4ca3-9ffb-2d400ed232ba.JPG)
![Slide15](https://user-images.githubusercontent.com/118953928/208457437-f14929a2-45de-4c0f-850a-5b09de5bbac2.JPG)
![Slide16](https://user-images.githubusercontent.com/118953928/208457440-7063834e-da07-4d3c-90bd-bec958421719.JPG)
![Slide17](https://user-images.githubusercontent.com/118953928/208457445-b145c478-684f-45ea-b6cd-b43191fd6466.JPG)
![Slide18](https://user-images.githubusercontent.com/118953928/208457449-a2d4e2da-48fa-4f6d-9550-3025a8dd6371.JPG)
![Slide19](https://user-images.githubusercontent.com/118953928/208457456-757b1f77-0716-4c12-a58f-d6debd2f12a8.JPG)
![Slide20](https://user-images.githubusercontent.com/118953928/208457460-dbf808ae-120f-4dbe-ac9b-66b70ba5f0ba.JPG)
 </details>
  
  <details>
  <summary>Lab 2 - Intro to ddc gui with design_vision</summary>
  
![Slide22](https://user-images.githubusercontent.com/118953928/208457524-ea70a909-fd67-42aa-a4ab-6f3d8380764d.JPG)
![Slide23](https://user-images.githubusercontent.com/118953928/208457533-d9ed212b-149d-488b-85b8-1f256ad77467.JPG)
![Slide24](https://user-images.githubusercontent.com/118953928/208457536-686236e0-61bf-4c85-89be-fa9db8b8dabf.JPG)

  
   </details>
  
  <details>
  <summary>Lab 3 - dc Synopsys dc setup</summary>
  
![Slide26](https://user-images.githubusercontent.com/118953928/208457592-cca055a8-2be0-4155-9120-78b3cc372233.JPG)
![Slide27](https://user-images.githubusercontent.com/118953928/208457599-b2261352-ddee-4cbc-9110-e2fee0675108.JPG)
 </details>
  
  <details>
  <summary>Lecture 3 - TCL quick refresher</summary>
  
![Slide29](https://user-images.githubusercontent.com/118953928/208457689-ec5ad320-6564-41a6-9090-a7c81c223abb.JPG)
![Slide30](https://user-images.githubusercontent.com/118953928/208457700-1a5cdc14-afe3-41fa-9016-0e1dd7f914e2.JPG)

   </details>
  
  <details>
  <summary>Lab 4 - tcl scripting</summary>
  
![Slide32](https://user-images.githubusercontent.com/118953928/208457751-17929e2e-d7dd-4b9f-87e3-4a2fa5f6c081.JPG)
![Slide33](https://user-images.githubusercontent.com/118953928/208457761-ed040d4d-599b-4797-b52c-360b0e89d84e.JPG)
![Slide34](https://user-images.githubusercontent.com/118953928/208457766-8bf57748-fd69-415b-aaab-cc3ab6b130b6.JPG)
  </details>

## Day 7 - Basics of STA

<details>
  <summary>Lecture session</summary>
  
![Slide2](https://user-images.githubusercontent.com/118953928/208876695-3b23eb15-509d-48e1-90ea-08dfafea6d1e.JPG)
![Slide3](https://user-images.githubusercontent.com/118953928/208876700-08e95fa6-9ef0-47b2-ad08-c5e4a67a7b32.JPG)
![Slide4](https://user-images.githubusercontent.com/118953928/208876701-0a78b623-0408-41b7-9b28-f6e5c6169842.JPG)
![Slide5](https://user-images.githubusercontent.com/118953928/208876708-ddfb8902-3007-4ba4-86ea-7a64a3c525b4.JPG)
![Slide6](https://user-images.githubusercontent.com/118953928/208876710-97f1c790-6955-4c7b-bab4-2f31e785b11b.JPG)
![Slide7](https://user-images.githubusercontent.com/118953928/208876714-1fec14ee-8e8c-43ae-9545-e47e837cb264.JPG)
![Slide8](https://user-images.githubusercontent.com/118953928/208876718-d9d841af-38cf-4fa5-a7c1-9be2565f69bf.JPG)
![Slide9](https://user-images.githubusercontent.com/118953928/208876721-1b6fabc7-828d-4377-bcd8-6422dac07415.JPG)
![Slide10](https://user-images.githubusercontent.com/118953928/208876723-78f7b6eb-f771-495a-80f6-6353b89f2333.JPG)
![Slide11](https://user-images.githubusercontent.com/118953928/208876726-a87dbf3f-27b7-4d11-90ce-2c914f92dce0.JPG)
![Slide12](https://user-images.githubusercontent.com/118953928/208876728-2975a876-ad2b-4d32-8eb7-effd639cabb0.JPG)

  </details>
  
<details>
  <summary>Lect 4 - Intro to STA</summary>
  
![Slide14](https://user-images.githubusercontent.com/118953928/208876768-f6355ea0-91e6-49bf-a5bf-7855fa04b739.JPG)
![Slide15](https://user-images.githubusercontent.com/118953928/208876775-2582b0f2-8d63-41d0-aac7-3e6066da54dd.JPG)
![Slide16](https://user-images.githubusercontent.com/118953928/208876778-a88dfb54-8b45-46e3-9343-8b5976d1557f.JPG)
![Slide17](https://user-images.githubusercontent.com/118953928/208876784-aa808b3b-ae0f-46c7-af3f-ec7fc7e996d0.JPG)
![Slide18](https://user-images.githubusercontent.com/118953928/208876788-e0efee02-99b7-4660-892b-d8db7aaf9c72.JPG)
![Slide19](https://user-images.githubusercontent.com/118953928/208876789-cc771875-08e6-47a5-a974-fd6194a5635d.JPG)
![Slide20](https://user-images.githubusercontent.com/118953928/208876794-61b1ff20-8c45-40f0-8f5f-c85e7080c28f.JPG)

  </details>
  
  <details>
  <summary>Lect 5 - What are constraints?</summary>
  
![Slide22](https://user-images.githubusercontent.com/118953928/208876827-4f34bfb4-4605-4c9e-aee2-29610815edf6.JPG)
![Slide23](https://user-images.githubusercontent.com/118953928/208876837-749c1652-1bd1-4288-9e01-e736abe84345.JPG)
![Slide24](https://user-images.githubusercontent.com/118953928/208876840-122ea900-ddb9-4ffd-821e-f4abe5ca2d37.JPG)
![Slide25](https://user-images.githubusercontent.com/118953928/208876842-31dc4eb9-5aa8-4c72-8eec-350744801fd5.JPG)
![Slide26](https://user-images.githubusercontent.com/118953928/208876851-2200a5b5-02da-4ab4-9270-d6850700ca32.JPG)

  </details>
  
<details>
  <summary>Lect 6 - Inp Trans Output Load</summary>
  
![Slide28](https://user-images.githubusercontent.com/118953928/208876909-9e06f85d-2751-4065-a597-b455332904cb.JPG)
![Slide29](https://user-images.githubusercontent.com/118953928/208876919-15730877-a4db-4afa-a730-d6268be9cf0b.JPG)
![Slide30](https://user-images.githubusercontent.com/118953928/208876971-46259cb5-0d12-4d24-9e3c-a24af66eb936.JPG)

  </details>
  
  <details>
  <summary>Lab 5 - Timing dot Libs</summary>
  
![Slide32](https://user-images.githubusercontent.com/118953928/208877101-892c8180-79ac-43d5-bd5b-140e7e0d2809.JPG)
![Slide33](https://user-images.githubusercontent.com/118953928/208877111-09ec6f65-5766-4dca-9066-8219fef1f329.JPG)
![Slide34](https://user-images.githubusercontent.com/118953928/208877122-7c16ed0d-d33c-46d6-a451-b2a94ca7487b.JPG)
![Slide35](https://user-images.githubusercontent.com/118953928/208877126-9fad1fd8-e3c2-4f01-84af-298149af5dc5.JPG)
![Slide36](https://user-images.githubusercontent.com/118953928/208877128-3adf5412-9a98-46d8-9e97-5a42d9fc59b5.JPG)
![Slide37](https://user-images.githubusercontent.com/118953928/208877132-ea9649c8-19ef-4df0-9852-24de21535812.JPG)
![Slide38](https://user-images.githubusercontent.com/118953928/208877139-4081efa7-75cf-47cd-bd0a-561f6fc87145.JPG)

  </details>
  
  <details>
  <summary>Lab 6 - Exploring dot Lib</summary>
  
![Slide40](https://user-images.githubusercontent.com/118953928/208877162-9ea49546-3400-4a9a-ab8b-d4d246aca796.JPG)
![Slide41](https://user-images.githubusercontent.com/118953928/208877244-d48ef973-7d86-4a89-8bec-f9cf554701b8.JPG)
![Slide42](https://user-images.githubusercontent.com/118953928/208877250-57c1c7b6-1f87-4892-a5dd-320dfece3e25.JPG)
![Slide43](https://user-images.githubusercontent.com/118953928/208877253-7930e79e-0d3d-4440-9ac8-8e024ee7ec6d.JPG)

  </details>
  
  <details>
  <summary>Lab7 - Exploring dot Lib part2</summary>
  

![Slide45](https://user-images.githubusercontent.com/118953928/208877299-d036ae52-cbf8-4eba-8181-dcc408851341.JPG)
![Slide46](https://user-images.githubusercontent.com/118953928/208877307-cb03ffb6-3b40-4003-8e91-4a9cb9e1a09d.JPG)
![Slide47](https://user-images.githubusercontent.com/118953928/208877312-ccc3c4af-c48f-40b2-ac6d-56e278b7246b.JPG)
![Slide48](https://user-images.githubusercontent.com/118953928/208877316-01b38546-48e3-4539-9dd8-faca592599ee.JPG)
![Slide49](https://user-images.githubusercontent.com/118953928/208877317-dee6ebf8-e7b7-43a9-a724-6814d6ce15f5.JPG)
![Slide50](https://user-images.githubusercontent.com/118953928/208877323-08c48ef5-d4c6-4d58-9f4a-76d414373226.JPG)
![Slide51](https://user-images.githubusercontent.com/118953928/208877327-5a15dbaf-4203-40ea-82fd-93d3a07c5536.JPG)
![Slide52](https://user-images.githubusercontent.com/118953928/208877331-69041a11-0101-4c31-818f-2ef5702b3ba3.JPG)

  </details>
  
## Day 8 - Advanced constraints

<details>
  <summary>Lecture 7 - SDC Part1 Clock - Clock Tree Modelling - Uncertainty</summary>

![Slide2](https://user-images.githubusercontent.com/118953928/209176161-7e8a5599-156d-40e8-a19b-1677af5dcae8.jpg)
![Slide3](https://user-images.githubusercontent.com/118953928/209176132-84482f26-f6c5-4e20-9a61-706260d2b9ac.JPG)
![Slide4](https://user-images.githubusercontent.com/118953928/209176139-b2e6b38d-baa9-40a4-b792-340cbbf4f043.JPG)
![Slide5](https://user-images.githubusercontent.com/118953928/209176144-ebb35c42-6776-4c8d-8d91-2bfb72ef36a4.JPG)
![Slide6](https://user-images.githubusercontent.com/118953928/209176148-9340da56-b92b-4c60-b19d-559d8dfb6bca.JPG)
![Slide7](https://user-images.githubusercontent.com/118953928/209176153-0fa5b73e-86b3-40aa-9660-43f5fd4cfe4a.JPG)
![Slide8](https://user-images.githubusercontent.com/118953928/209176159-d6b1f905-5641-4c40-89dc-d2da908236ed.JPG)
</details>

<details>
  <summary>Lecture 8 - SDC Part2 IO delays</summary>

![Slide10](https://user-images.githubusercontent.com/118953928/209176272-b92a4fae-f140-425e-814d-4a31e86903af.JPG)
![Slide11](https://user-images.githubusercontent.com/118953928/209176277-d0f78594-7cc2-4c3e-92f9-21d3bc4e7884.JPG)
![Slide12](https://user-images.githubusercontent.com/118953928/209176282-4621bcff-ec98-4042-a0f4-ab79283e3e04.JPG)
![Slide13](https://user-images.githubusercontent.com/118953928/209176284-ea112835-eb14-4c0a-b4c1-3123f29f154c.JPG)
![Slide14](https://user-images.githubusercontent.com/118953928/209176285-2d703a1b-6d5a-41e0-851f-b26276cee577.JPG)
![Slide15](https://user-images.githubusercontent.com/118953928/209176287-e12018d7-2827-42a9-82a3-dc28483f9816.JPG)
![Slide16](https://user-images.githubusercontent.com/118953928/209176290-db315f4d-b184-48c6-b3ac-179ed81aa7c2.JPG)
![Slide17](https://user-images.githubusercontent.com/118953928/209176294-4000981c-e731-4b5f-9e9b-1d6b56d727e2.JPG)
![Slide18](https://user-images.githubusercontent.com/118953928/209176296-0bd56aa2-984d-4408-b685-85aab473b095.JPG)
</details>

<details>
  <summary>Lab 8 - Loading design get_cells, get_ports, get_nets</summary>

![Slide21](https://user-images.githubusercontent.com/118953928/209462777-6c227638-d1ea-4bac-86b5-a31029e6f214.JPG)
![Slide22](https://user-images.githubusercontent.com/118953928/209462779-46b72346-69a4-464f-ba04-4592f5433966.JPG)
![Slide23](https://user-images.githubusercontent.com/118953928/209462782-7aae4a46-6b41-49bc-ad69-e7d1fcd2b982.JPG)
![Slide24](https://user-images.githubusercontent.com/118953928/209462783-a6e6a54b-d2fd-4cc6-b348-90bc09599758.JPG)
![Slide25](https://user-images.githubusercontent.com/118953928/209462784-1739b615-510f-41f7-abfe-7377f8d78b64.JPG)
![Slide26](https://user-images.githubusercontent.com/118953928/209462785-86a7363d-0a8d-443a-9524-3f75dd629cf3.JPG)
![Slide27](https://user-images.githubusercontent.com/118953928/209462786-7db3f743-0427-4395-8895-d999f0064b70.JPG)
</details>

<details>
  <summary>Lab 9 - get_pins, get_clocks, querying_clocks</summary>

![Slide29](https://user-images.githubusercontent.com/118953928/209462796-e3ac68a5-9107-4ff5-9ec0-34cfc3dc66e1.JPG)
![Slide30](https://user-images.githubusercontent.com/118953928/209462799-c3969e1b-3b7d-4a57-95b5-2f763dcb1085.JPG)
</details>

<details>
  <summary>Lab 10 - create_clock waveform</summary>

![Slide32](https://user-images.githubusercontent.com/118953928/209462807-3e2a4cee-dc60-48c1-9439-e83fa50097b7.JPG)
![Slide33](https://user-images.githubusercontent.com/118953928/209462809-31680b2c-05f7-4c6d-b4fb-71b4e50153d3.JPG)
![Slide34](https://user-images.githubusercontent.com/118953928/209462810-91baa2e4-1df4-4782-b113-24180a501416.JPG)
![Slide35](https://user-images.githubusercontent.com/118953928/209462811-57d826b3-1614-4aa9-8efb-79e6f65616d0.JPG)
![Slide36](https://user-images.githubusercontent.com/118953928/209462812-75ea043b-d5c1-46f9-9700-eee2084219db.JPG)
</details>

<details>
  <summary>Lab 11- Clock Network Modelling - Uncertainty, report_timing</summary>

![Slide38](https://user-images.githubusercontent.com/118953928/209462822-7894e5db-7db1-4c02-afb6-22a6ccd185c1.JPG)
![Slide39](https://user-images.githubusercontent.com/118953928/209462826-e865d63c-35b1-40f9-86c3-878b1c00d930.JPG)
![Slide40](https://user-images.githubusercontent.com/118953928/209462828-77ef3b89-adfa-494e-803a-1fe92929302c.JPG)
![Slide41](https://user-images.githubusercontent.com/118953928/209462832-217632b2-416a-4e96-95ba-98ae94abdde5.JPG)
![Slide42](https://user-images.githubusercontent.com/118953928/209462834-c4dcc7ce-0ddc-42ff-b465-99004005ea39.JPG)
</details>

<details>
  <summary>Lab 12- IO Delays - Uncertainty</summary>

![Slide44](https://user-images.githubusercontent.com/118953928/209462843-9d7249c6-7553-4fc9-9476-cfb56face885.JPG)
![Slide45](https://user-images.githubusercontent.com/118953928/209462845-d088a637-fb7f-4784-ae03-8db87e695b3e.JPG)
![Slide46](https://user-images.githubusercontent.com/118953928/209462846-92795c88-2745-4094-8b51-2ec9df310b6f.JPG)
![Slide47](https://user-images.githubusercontent.com/118953928/209462847-c8e8a137-3d9d-4529-a1ad-f37d7b23a303.JPG)
![Slide48](https://user-images.githubusercontent.com/118953928/209462850-14d161a5-10bd-40d0-a7ab-e3e1c903b6a0.JPG)
![Slide49](https://user-images.githubusercontent.com/118953928/209462851-97f70490-c2de-4461-a99c-48d08c3eaa31.JPG)
![Slide50](https://user-images.githubusercontent.com/118953928/209462852-8713029d-0d71-4a60-81f1-10dec04d822d.JPG)
![Slide51](https://user-images.githubusercontent.com/118953928/209462853-789f93a9-3cee-4488-84b9-fa75ab5ac89f.JPG)
![Slide52](https://user-images.githubusercontent.com/118953928/209462854-0b411e9d-52c0-4b93-a9cb-7b1755c5cbf2.JPG)
![Slide53](https://user-images.githubusercontent.com/118953928/209462855-96276937-368c-4651-b29b-813decae142f.JPG)
![Slide54](https://user-images.githubusercontent.com/118953928/209462856-da9ed510-c2b6-4359-b307-0aec2c609ca5.JPG)
</details>

<details>
  <summary>Lecture 9 - SDC Part3 generated_clk</summary>

![Slide56](https://user-images.githubusercontent.com/118953928/209539007-3448fd48-a25c-4530-b2ce-b3f33cfd4e5e.JPG)
![Slide57](https://user-images.githubusercontent.com/118953928/209539010-808c7b9e-aab8-4c68-a376-4392a15a0f62.JPG)
</details>

<details>
  <summary>Lab 13 - generated_clocks</summary>

![Slide59](https://user-images.githubusercontent.com/118953928/209539038-e4f9430f-4dff-4573-afca-f342f47f851d.JPG)
![Slide60](https://user-images.githubusercontent.com/118953928/209539042-1a50d905-15ee-4834-a811-2362180044e1.JPG)
![Slide61](https://user-images.githubusercontent.com/118953928/209539044-b1663393-520e-4f51-b311-84c7249a8ecb.JPG)
![Slide62](https://user-images.githubusercontent.com/118953928/209539047-731aac47-6a48-4239-a1bf-f0e355dabbcb.JPG)
![Slide63](https://user-images.githubusercontent.com/118953928/209539049-06bde80d-4e51-47ff-83f1-bea53f918881.JPG)
![Slide64](https://user-images.githubusercontent.com/118953928/209539053-792e871b-6cfc-4a4a-9040-87a4413ba022.JPG)
![Slide65](https://user-images.githubusercontent.com/118953928/209539054-54f7d8c7-3c08-4306-ad9c-b30dfc37913a.JPG)
</details>

<details>
  <summary>Lecture 10 - SDC Part4 vclk, max_latency, rise_fall IO Delays</summary>

![Slide67](https://user-images.githubusercontent.com/118953928/209539093-700817b8-4063-4739-83fe-480e184228b6.JPG)
![Slide68](https://user-images.githubusercontent.com/118953928/209539101-502292b3-a555-47d5-8a07-01ded4f4b9cf.JPG)
![Slide69](https://user-images.githubusercontent.com/118953928/209539105-ff4feea1-2cee-49e3-b06b-c40d9be249ad.JPG)
![Slide70](https://user-images.githubusercontent.com/118953928/209539110-4b5af6cc-2f09-4454-a4a2-88627d0ef01f.JPG)
![Slide71](https://user-images.githubusercontent.com/118953928/209539112-31b44c42-7f23-4349-b5fe-1aa8cddf14ff.JPG)
![Slide72](https://user-images.githubusercontent.com/118953928/209539113-2ab9e3b2-1c15-472b-ad74-52fa3467bed4.JPG)
</details>

<details>
  <summary>Lab 15 - part1 Set_Max_delay</summary>

![Slide75](https://user-images.githubusercontent.com/118953928/209539166-c445002b-0c00-48ed-9cd9-a18880ae9101.JPG)
![Slide76](https://user-images.githubusercontent.com/118953928/209539171-d013e896-1e99-4895-b7fb-d136950366ce.JPG)
![Slide77](https://user-images.githubusercontent.com/118953928/209539175-afe17c7d-ae27-4f81-bd86-a39bebee2141.JPG)
![Slide78](https://user-images.githubusercontent.com/118953928/209539176-33a0b4a2-deb3-43cf-9d4f-86f5d978070f.JPG)
![Slide79](https://user-images.githubusercontent.com/118953928/209539180-95427563-fe86-44fb-a691-ce4cde854388.JPG)
![Slide80](https://user-images.githubusercontent.com/118953928/209539184-f0569bda-e49b-48b7-9d75-ccf5cecbb4e0.JPG)
![Slide81](https://user-images.githubusercontent.com/118953928/209539186-110ca6b0-92c6-4ce1-b771-fe051937d831.JPG)
</details>

<details>
  <summary>Lab 15 - part2 - VCLK</summary>

![Slide83](https://user-images.githubusercontent.com/118953928/209539223-ecc2baf2-a4c3-4e55-9286-28641d223103.JPG)
![Slide84](https://user-images.githubusercontent.com/118953928/209539227-4ac22ee5-10dc-4606-a229-134f57cc8237.JPG)
![Slide85](https://user-images.githubusercontent.com/118953928/209539232-20de0cf1-3162-4fa9-bc91-071c322c0ed4.JPG)
![Slide86](https://user-images.githubusercontent.com/118953928/209539234-fc7e51ca-943e-44fe-b6e7-b8b5cc587e6a.JPG)
![Slide87](https://user-images.githubusercontent.com/118953928/209539236-21165a31-5e72-4648-b2f4-6cb9aba429ff.JPG)
![Slide88](https://user-images.githubusercontent.com/118953928/209539238-997e2e74-f632-488a-8003-49956fd0c8e6.JPG)
</details>

## Day 9 - Optimization 

<details>
  <summary>Lecture 11 - Optimizations Combinational Opt</summary>
  
### **Optimization Goals**

- Cost function based optimization
	- Optimization till the cost is met.
		for example cost function for timing is IO delay, clock period, max delay.
	- Over optimization of one goal will harm other goals.
	- Goals for sythesis
		- Meet timing
		- Meet area
		- Meet power
	- Remember that there will be trade-off to get faster cell.
	
### **Combinational Logic Optimization**

1.	Squeezing the logic to get most optimised design.
	- Area and Power savings
2.	Constant  Propagation
	- Direct Optimization
3. 	Boolean Logic Optimization
	- K-Map 
	- Quine McKluskey

![Slide3](https://user-images.githubusercontent.com/118953928/209755542-10728535-fdb2-418b-82eb-67ce436731ef.JPG)
![Slide4](https://user-images.githubusercontent.com/118953928/209755545-03274155-4906-41fe-a9d3-5bfe5867a9e4.JPG)
![Slide5](https://user-images.githubusercontent.com/118953928/209755546-fbef08e8-cf8d-4bbc-9232-017d31163241.JPG)
![Slide6](https://user-images.githubusercontent.com/118953928/209755550-83e86cbf-49f1-41e7-b249-14a0ddc98130.JPG)
![Slide7](https://user-images.githubusercontent.com/118953928/209755552-4b5851e7-09bb-4334-b933-f9714c831534.JPG)
</details>

<details>
  <summary>Lecture 12 Sequential Optimizations</summary>
  
### **Sequential Logic Optimization**

- Basic 
	- Sequential Constant Propagation
	- Retiming
	- Unused Flop removal
	- Clock gating

- Advanced
	- State optimization
	
![Slide9](https://user-images.githubusercontent.com/118953928/209770915-44e42126-506b-4908-8a7e-b280b3725339.JPG)
![Slide10](https://user-images.githubusercontent.com/118953928/209770919-7b1e18c8-2c40-40c9-b575-4eeaf43d932a.JPG)
![Slide11](https://user-images.githubusercontent.com/118953928/209770921-d3f0289c-9d63-4a86-9395-ae364d1f0a47.JPG)

### **Optimization of unloaded output**
![Slide12](https://user-images.githubusercontent.com/118953928/209770974-ae07c530-e3fa-43b1-b328-fbc9978ad507.JPG)
	
### **Controlling sequential optimization in DC**
```
- compile_seqmap_propagate_constants --> for constant optimization
- compile_delete_unloaded_sequential_cells --> for sequential optimization
- compile_register_replication --> for clonning register
```
	

</details>

<details>
  <summary>Lab 16 - part1 Combinational_optimizations</summary>
  
### **Optimization of opt_check.v**
```
IN DESIGN COMPILER
sh gvim DC_WORKSHOP/verilog_files/opt_check*.v -o
read_verilog DC_WORKSHOP/verilog_files/opt_check.v
report_timing
get_cells *
report_timing -to y2
report_timing -to y1
write -f ddc -out opt_check.ddc

```

```
IN DESIGN VISION
reset_design
read_ddc DC_WORKSHOP/verilog_files/opt_check.ddc
```
![Slide14](https://user-images.githubusercontent.com/118953928/209793583-8a6cb822-e553-454a-88d2-b56664fc898b.JPG)
![Slide15](https://user-images.githubusercontent.com/118953928/209793592-05e0ebf2-cf3b-4acc-9bc0-d4b3a5a667b5.JPG)
	
### **Optimization of opt_check2.v**
```
IN DESIGN COMPILER
reset_design
read_ddc DC_WORKSHOP/verilog_files/opt_check2.v 
link
compile
write -f ddc -out opt_check2.ddc
```

```
IN DESIGN VISION
reset_design
read_ddc DC_WORKSHOP/verilog_files/opt_check2.ddc
```
![Slide16](https://user-images.githubusercontent.com/118953928/209793596-5a503ce2-0f71-49a4-bdfb-6736f4d10c35.JPG)
![Slide17](https://user-images.githubusercontent.com/118953928/209793598-37e503fd-91d1-4c33-9f7e-7dba45d31238.JPG)
	
### **Optimization of opt_check3.v**
```
IN DESIGN COMPILER
reset_design
read_ddc DC_WORKSHOP/verilog_files/opt_check3.v 
link
compile
write -f ddc -out opt_check3.ddc
```

```
IN DESIGN VISION
reset_design
read_ddc DC_WORKSHOP/verilog_files/opt_check3.ddc
```
![Slide18](https://user-images.githubusercontent.com/118953928/209793600-4e7c5384-b8af-4adb-8e69-ff5398c8823e.JPG)
![Slide19](https://user-images.githubusercontent.com/118953928/209793604-819c4912-3218-4a76-b570-93677b059aa2.JPG)
	
### **Optimization of opt_check4.v**
```
IN DESIGN COMPILER
reset_design
read_ddc DC_WORKSHOP/verilog_files/opt_check4.v 
link
compile
write -f ddc -out opt_check4.ddc
```

```
IN DESIGN VISION
reset_design
read_ddc DC_WORKSHOP/verilog_files/opt_check4.ddc
```
![Slide20](https://user-images.githubusercontent.com/118953928/209793609-2e0ede4c-c75e-4bc4-8274-fe2393ad4e6f.JPG)
![Slide21](https://user-images.githubusercontent.com/118953928/209793612-48518d7e-5048-4510-8f9e-5cd8faaba70d.JPG)

</details>

<details>
  <summary>Lab 16 - part2 resource sharing optimizations</summary>

### resource_sharing_mult_check.v balance optimization (no constrain set)
```
read_verilog DC_WORKSHOP/verilog_files/resource_sharing_mult_check.v
link
compile_ultra
report_area
```
![Slide23](https://user-images.githubusercontent.com/118953928/209890772-46e230b9-8a66-486b-8afa-1029ad8cccd4.JPG)
![Slide24](https://user-images.githubusercontent.com/118953928/209890694-c9722605-ab94-40fe-bad1-54aad3b4d32e.JPG)
![Slide25](https://user-images.githubusercontent.com/118953928/209890696-8c98e0bc-db0c-4dd7-8a4c-d2240e474c6a.JPG)

### resource_sharing_mult_check.v (max delay 2.5ns)
```
set_max_delay -from [all_inputs] -to [all_outputs] 2.5
report_timing
compile_ultra
report_timing
report_area
```
![Slide26](https://user-images.githubusercontent.com/118953928/209890697-5ab93eab-6672-45cd-8519-0e1b5b83f2b8.JPG)
![Slide27](https://user-images.githubusercontent.com/118953928/209890698-6545ea84-faa0-4f5b-b544-a5ab6c56431b.JPG)
![Slide28](https://user-images.githubusercontent.com/118953928/209890699-c4e2c833-bec1-443a-a030-b600c52703e3.JPG)

### resource_sharing_mult_check.v (max delay 0.1ns)
```
set_max_delay -from sel -to [all_outputs] 0.1
compile_ultra
report_timing
report_area
```
![Slide29](https://user-images.githubusercontent.com/118953928/209890700-e4e2344c-9ed4-42f6-98bc-724c9381fe03.JPG)
![Slide30](https://user-images.githubusercontent.com/118953928/209890703-40e79421-fae6-4c1d-83b2-e042894ff6c6.JPG)

### resource_sharing_mult_check.v (max area 800mm2)
```
set_max_area 800
compile_ultra
report_timing
report_area
```
![Slide31](https://user-images.githubusercontent.com/118953928/209890704-6b51a381-610c-43d2-93a8-1ea99bd7491a.JPG)

## Comparing all the condition
![Slide32](https://user-images.githubusercontent.com/118953928/209890705-2ba48f51-d08a-4003-89ae-868695032488.JPG)

</details>

<details>
  <summary>Lab 17 - seq optimizations</summary>
  
![Slide34](https://user-images.githubusercontent.com/118953928/210192542-6d1d9b51-b5ba-4403-bc63-efecbdc85fd0.JPG)
![Slide35](https://user-images.githubusercontent.com/118953928/210192549-788850bd-df39-4c6c-aa7f-aa758b652306.JPG)
![Slide36](https://user-images.githubusercontent.com/118953928/210192551-1b42f6e0-0a59-4055-9a7d-93f9f5108438.JPG)
![Slide37](https://user-images.githubusercontent.com/118953928/210192552-a04028cf-ae97-40af-a11f-cec9af42a0e0.JPG)
![Slide38](https://user-images.githubusercontent.com/118953928/210192554-0156b5a0-8902-4c5d-8bba-d5cb3fa8fdf0.JPG)
![Slide39](https://user-images.githubusercontent.com/118953928/210192556-160d9e46-b0c9-46d1-a4b8-5bf863b542fe.JPG)
![Slide40](https://user-images.githubusercontent.com/118953928/210192559-e4ca2c1f-b820-4e30-ab95-0d15f351704c.JPG)
![Slide41](https://user-images.githubusercontent.com/118953928/210192561-d83ce0c5-c956-4c7a-9a9f-480bd986f6d6.JPG)
![Slide42](https://user-images.githubusercontent.com/118953928/210192562-ba2fc0d2-100e-4c43-b837-cb8880516b84.JPG)
![Slide43](https://user-images.githubusercontent.com/118953928/210192565-08cf7cb1-30c0-4258-b146-d9bd8c5370b4.JPG)
![Slide44](https://user-images.githubusercontent.com/118953928/210192567-f2c864a6-2178-419e-81f5-3d68268e674f.JPG)
</details>

<details>
  <summary>Lecture 13 special optimizations</summary>
  
![Slide46](https://user-images.githubusercontent.com/118953928/210192583-5fbc793f-a229-4494-9124-5c3a0bd5cd53.JPG)
![Slide47](https://user-images.githubusercontent.com/118953928/210192587-f84bb934-bf66-4690-81c2-f3f1aa213e44.JPG)
![Slide48](https://user-images.githubusercontent.com/118953928/210192589-57ee9c53-897a-4c3c-b197-c161e669ceea.JPG)
![Slide49](https://user-images.githubusercontent.com/118953928/210192590-1685a477-a9c8-4439-8bd3-a75a6474c696.JPG)
![Slide50](https://user-images.githubusercontent.com/118953928/210192592-2eabf78b-20e7-4f83-ad8b-023e49c993be.JPG)
![Slide51](https://user-images.githubusercontent.com/118953928/210192594-1f3f1237-26e6-42a9-94f3-a9df476e6a43.JPG)
</details>

<details>
  <summary>Lecture 14 - How Paths are timed MCP?</summary>
  
![Slide53](https://user-images.githubusercontent.com/118953928/210192614-2200c780-ed7b-4fc7-9571-492948e5b25c.JPG)
![Slide54](https://user-images.githubusercontent.com/118953928/210192617-80ebc7a7-1a46-471d-ae60-0cd7af2892df.JPG)
</details>

<details>
  <summary>Lab 18 - Boundary Optimization</summary>
  
![Slide56](https://user-images.githubusercontent.com/118953928/210192641-d987e246-2576-4f4c-9e7a-a42988800dc6.JPG)
![Slide57](https://user-images.githubusercontent.com/118953928/210192644-5fdb469e-068a-4832-a2f4-ebc6eb37fd78.JPG)
</details>

<details>
  <summary>Lab 19 - Register Retiming</summary>
  
```
read_verilog DC_WORKSHOP/verilog_files/check_reg_retime.v
link
compile
report_timing
sh gvim DC_WORKSHOP/verilog_files/reg_retime_cons.tcl
source DC_WORKSHOP/verilog_files/reg_retime_cons.tcl
report_clocks
report_timing
compile_ultra -retime
```
![Slide59](https://user-images.githubusercontent.com/118953928/210192652-d879ae36-abdd-433a-884d-1a0b7ffdf0f4.JPG)
![Slide60](https://user-images.githubusercontent.com/118953928/210192653-ed514244-cc89-4901-9e84-f6a8be8ce6d3.JPG)
![Slide61](https://user-images.githubusercontent.com/118953928/210192654-6ea8a95b-733d-4112-a712-2972c82ced0c.JPG)
![Slide62](https://user-images.githubusercontent.com/118953928/210192656-9b6c6a0f-f556-43ac-9389-6e0f23200532.JPG)
</details>

<details>
  <summary>Lab 20 - Isolating output ports</summary>
  
```
set_isolate_ports -type buffer [all_outputs]
compile_ultra
report_timing -nosplit -inp -cap -trans -sig 4
report_timing -from val_out_reg[0]/CLK -to val_out_reg[0]/D -nosplit -inp -cap -trans -sig 4
```
![Slide64](https://user-images.githubusercontent.com/118953928/210192667-710da853-13db-4625-ae5d-f4f5d7558366.JPG)
![Slide65](https://user-images.githubusercontent.com/118953928/210192670-63b004be-8b71-495c-ba1b-50e0b122ca86.JPG)
![Slide66](https://user-images.githubusercontent.com/118953928/210192671-d1420054-d82a-436b-b08a-822ffb690fff.JPG)
![Slide67](https://user-images.githubusercontent.com/118953928/210192674-237c4303-c85d-48b6-b86a-9a86d72a3a4c.JPG)
![Slide68](https://user-images.githubusercontent.com/118953928/210192676-0086ccf3-d81e-4ceb-bd1a-39a200e6ab3b.JPG)
![Slide69](https://user-images.githubusercontent.com/118953928/210192681-22b19641-e184-4b95-9959-f8b8e4d5f1e9.JPG)
</details>

<details>
  <summary>Lab 21 - MultiCycle path</summary>
  
```
read_verilog DC_WORKSHOP/verilog_files/mcp_check.v
link
compile_ultra
sh gvim DC_WORKSHOP/verilog_files/mcp_check_cons.tcl
source DC_WORKSHOP/verilog_files/mcp_check_cons.tcl
report_timing
compile_ultra
report_timing
set_multicycle_path -setup 2 -to prod_reg[*]/D -from [all_inputs] 	
report_timing -to prod_reg[*]/D -from valid_reg/CLK
report_clock *
```
![Slide71](https://user-images.githubusercontent.com/118953928/210192700-f795aaae-9cec-4e1c-8f39-057e36ad7215.JPG)
![Slide72](https://user-images.githubusercontent.com/118953928/210192701-e4b1c6d9-f2ea-443d-900a-b79d42f97445.JPG)
![Slide73](https://user-images.githubusercontent.com/118953928/210192702-569e4b99-2f11-45fc-8629-94d9ec7ce378.JPG)
![Slide74](https://user-images.githubusercontent.com/118953928/210192703-7aca42d6-7ae6-4f1a-94d9-6ee75636ecc1.JPG)
```
report_timing -to prod_reg[*]/D -from [all_inputs]
report_timing -delay min
set_multicycle_path -hold 1 -from [all_inputs] -to prod_reg[*]/D
report_timing -delay min -to prod_reg[*]/D -from [all_inputs]
report_timing -nosplit -inp -cap -trans -sig 4
```

![Slide75](https://user-images.githubusercontent.com/118953928/210192704-e380ab1a-e21c-4440-91e5-81b9688a7646.JPG)


</details>

## Day 10 - Quality checks 

<details>
<summary>L1 - Lecture Report timing</summary>
	
![Slide3](https://user-images.githubusercontent.com/118953928/210225260-f0217fb6-e18c-4777-a46e-40510f91bc9b.JPG)
![Slide4](https://user-images.githubusercontent.com/118953928/210225268-880a3d2a-5967-4fd5-9cf9-b49433d6b900.JPG)
![Slide5](https://user-images.githubusercontent.com/118953928/210225276-7e126bf4-093b-47f9-80ad-ccb0553febe2.JPG)
![Slide6](https://user-images.githubusercontent.com/118953928/210225281-9107dfe7-76d3-4400-aa4b-2a96a0429004.JPG)
![Slide7](https://user-images.githubusercontent.com/118953928/210225282-ba127fd4-2c9d-4b7a-8119-fddb22d4ffe5.JPG)
</details>
  
	
<details>
<summary>L2 - Lab Report timing</summary>
	
![Slide9](https://user-images.githubusercontent.com/118953928/210225312-669e7bce-0229-4cda-aace-9e7df89b6703.JPG)
![Slide10](https://user-images.githubusercontent.com/118953928/210225317-71c48336-346f-4340-afa6-c4e1c624e4a0.JPG)
![Slide11](https://user-images.githubusercontent.com/118953928/210225319-027d8db8-518f-452e-9ddd-838e3bd58dd4.JPG)
![Slide12](https://user-images.githubusercontent.com/118953928/210225323-69d3aed5-caec-48fe-b9f8-ea24897ecbdc.JPG)
![Slide13](https://user-images.githubusercontent.com/118953928/210225326-0eafa32e-3821-483b-b8bf-ce592c06b062.JPG)
![Slide14](https://user-images.githubusercontent.com/118953928/210225335-51608585-ba71-4eb5-8366-3cf6b95a087e.JPG)
</details>
	
<details>
<summary>L3 - Lab Check_timing, Check_design, Set_max_capacitance, HFN</summary>
	
![Slide16](https://user-images.githubusercontent.com/118953928/210225408-d836e8c8-1a71-4700-8146-4e685010f2d5.JPG)
![Slide17](https://user-images.githubusercontent.com/118953928/210225419-b6eb9497-016e-4841-8ac4-adc6c8ee2d2f.JPG)
![Slide18](https://user-images.githubusercontent.com/118953928/210225423-9d2aeb6c-a82d-473c-b31c-4e0b19a99ede.JPG)
![Slide19](https://user-images.githubusercontent.com/118953928/210225424-213ea58a-1d45-4a44-b92d-3c310856a933.JPG)
![Slide20](https://user-images.githubusercontent.com/118953928/210225427-e892ef0e-db7d-4fd6-858b-48f66622e676.JPG)
![Slide21](https://user-images.githubusercontent.com/118953928/210225431-c9217d53-988d-4a0b-adbe-0ce6dc3cc241.JPG)
![Slide22](https://user-images.githubusercontent.com/118953928/210225434-1f6cef8c-bb20-4905-9e5b-fb654df50cb0.JPG)
![Slide23](https://user-images.githubusercontent.com/118953928/210225441-a9ec4a8f-dfc2-4e00-8dfc-b875f32fd936.JPG)
![Slide24](https://user-images.githubusercontent.com/118953928/210225442-38006c60-c505-4d2e-a91a-914c0ae49b1a.JPG)
![Slide25](https://user-images.githubusercontent.com/118953928/210225443-480565a7-76bf-488f-9264-d501fcde119e.JPG)
![Slide26](https://user-images.githubusercontent.com/118953928/210225445-4e1d3c6a-8a7d-4966-847b-2a062e852c7e.JPG)
![Slide27](https://user-images.githubusercontent.com/118953928/210225448-8a45d3f0-1e28-439d-8787-db4cd1e48d18.JPG)
![Slide28](https://user-images.githubusercontent.com/118953928/210225453-30fd4306-b1f4-4c6a-bf1c-b5d773f758fe.JPG)
![Slide29](https://user-images.githubusercontent.com/118953928/210225459-75586f3a-8464-4399-a33e-0ef7a2067e99.JPG)
![Slide30](https://user-images.githubusercontent.com/118953928/210225460-426fffef-1e9d-42bd-a828-0de021fd5027.JPG)
![Slide31](https://user-images.githubusercontent.com/118953928/210225462-abbd5f42-31a7-4caa-ac07-8709169197eb.JPG)
![Slide32](https://user-images.githubusercontent.com/118953928/210225464-8fc07b72-b559-484b-831b-ba222d7c9636.JPG)
</details>
	
	
<details>
<summary>Timing Models</summary>
	
![Slide33](https://user-images.githubusercontent.com/118953928/210225488-bc4d5b5f-5af7-4454-ab06-249b678393cc.JPG)
![Slide34](https://user-images.githubusercontent.com/118953928/210225494-b16305ba-3f95-4ec9-bdcd-27afc7462b9c.JPG)
![Slide35](https://user-images.githubusercontent.com/118953928/210225496-288c2700-9ddd-4080-b17f-3b771678e815.JPG)
</details>

## Day 11 -  Introduction to the BabySoC

<details>
<summary>Theory</summary>

![note_page-0001](https://user-images.githubusercontent.com/118953928/210316604-6ede7510-5eec-4d2d-840f-5e97abe87e80.jpg)
![note_page-0002](https://user-images.githubusercontent.com/118953928/210316612-f7f9bec4-18da-4be6-9af1-f35888056002.jpg)
![note_page-0003](https://user-images.githubusercontent.com/118953928/210316614-14a8d378-7453-4bff-9adf-27d2ed36f025.jpg)
</details>


<details>
<summary>Video Summary</summary>

![note_page-0004](https://user-images.githubusercontent.com/118953928/210473719-a6120a4c-0fe1-4d09-9c5a-ac8312c3f4f1.jpg)
![note_page-0005](https://user-images.githubusercontent.com/118953928/210473753-603222a4-a88f-4609-8692-4222b7114922.jpg)
</details>
	
## Day 12 -  BabySoC Modelling

<details>
<summary>Theory</summary>

**Modelling in electroinic**
- The use of a physical or logical representation of a given system to create data and assist decide decisions or make predictions about the system is known as modelling and simulation.
- Models are representations that may be used to help define, analyse, and communicate a collection of concepts.
- The purpose of modelling including:
  - support analysis, specification,
  - design,
  - verification,
  - validation of a system,
  - and communicate certain information.
- In this session we will modelling VSDBabySoC.

**VSDBabySoc Modelling**
- Some initial input signals will be fed into vsdbabysoc module.
- Pll will start generating the proper CLK for the circuit. and  clock signal will make the rvmyth to execute instructions and some values are generated.
- These values then are used by DAC core to provide the final output signal named OUT.
- There  3 main elements (IP cores) and a wrapper as an SoC in this training.

**RVMYTH - Risc-V based MYTH**
- RISC is an abbreviation for Reduced instruction set computer. 
- The term **"ISA" (Instruction Set Architecture)** refers to a basic integer ISA that must be included in every implementation, as well as optional extensions to the base ISA. 
- The width of the integer registers and the associated size of the address space, as well as the number of integer registers, distinguish each base integer instruction set. RV32I and RV64I are the two basic base integer versions.

**A simple one cycle CPU**
![image](https://user-images.githubusercontent.com/118953928/210686265-32cc3ada-51b9-4850-8232-abc1765d60a0.png)

 **Phase Locked Loop**
- A phase-locked loop (PLL) is an electrical circuit that has a voltage or voltage-driven oscillator that continually changes its frequency to match the frequency of an input signal. 
- PLLs are used to create, maintain, modulate, and demodulate signals, including other things.
- The clock will provide several blocks on the chip, and it will have delays because to lengthy connections (if just one clock source is utilised).
- Some blocks may require 200Mhz, while others may require 100Mhz - the idea is that various frequencies may exist on a same tiny chip.
- A ppm (clock accuracy) idea is introduced; whenever quartz is obtained, it comes with an x ppm error.
- The accuracy of a crystal clock is expressed in units of ppm, or parts per million, and it provides a handy manner of comparing the accuracies of different crystal standards.
- A common microcontroller crystal has a 100ppm standard (every day inaccuracy of 8.6s).
- A watch crystal has an inaccuracy of 20ppm, however this equates to 20/1e6 (2e-5) which produces an error over a day of 86400 * 2e-5 = 1.73 seconds each day, 
- thus in a month it loses 30x1.72 = 51 seconds or error rate per day: 1.73 seconds.

**Digital-to-Analog Converter**
- A DAC is a device that transforms a digital input signal to an analogue output signal. 
- A binary code, which is a combination of bits 0 and 1, is used to represent a digital signal. 
- A Digital to Analog Converter (DAC) has several binary inputs and a single output. 
- In general, a DAC's number of binary inputs will be a power of two.
- DACs are classified into two types: R-2R Ladder DAC with Weighted Resistor DAC
</details>
	
<details>
<summary>mythcore_test.v & tb_mythcore_test.v</summary>

![Slide3](https://user-images.githubusercontent.com/118953928/210831890-ee893609-753e-4ad5-9b20-128c91fb1038.JPG)
![Slide4](https://user-images.githubusercontent.com/118953928/210831901-2ff93473-752b-4982-af34-20def09dd156.JPG)
![Slide5](https://user-images.githubusercontent.com/118953928/210831904-3f27d880-6c7e-44b1-9878-e4238a9333d7.JPG)
</details>
	
<details>
<summary>avsddac.v & avsddac_tb_test.v</summary>

![Slide7](https://user-images.githubusercontent.com/118953928/210831996-94d9c0d7-759a-4f95-b5c4-d01314c3ad12.JPG)
![Slide8](https://user-images.githubusercontent.com/118953928/210832002-55ab7941-0d76-46bb-a3c6-380539def390.JPG)
</details>

<details>
<summary>avsd_pll_1v8.v pll_tb.v</summary>

![Slide10](https://user-images.githubusercontent.com/118953928/210832215-12b9a06f-de3f-4b61-8e6f-c8b89f1e5813.JPG)
![Slide11](https://user-images.githubusercontent.com/118953928/210832224-2c81a359-ea3b-4168-8db2-8417d1a422e7.JPG)
</details>

<details>
<summary>interactive mode(debug mode)</summary>

![Slide13](https://user-images.githubusercontent.com/118953928/210832288-ec323a98-f513-47da-81d4-31b4a2e0832f.JPG)
![Slide14](https://user-images.githubusercontent.com/118953928/210832296-4bf92702-abc2-4355-9612-3881ee35f060.JPG)
</details>

<details>
<summary>rvmyth_pll.v & rvmyth_pll_tb.v </summary>

![Slide16](https://user-images.githubusercontent.com/118953928/210832421-30260ec4-6cb9-40b9-8509-3b6741335731.JPG)
![Slide17](https://user-images.githubusercontent.com/118953928/210832431-2dfb3fd1-32da-4e8b-b9f6-e815a561e98b.JPG)
</details>

<details>
<summary>rvmyth_avsddac.v & rvmyth_avsddac_TB.v</summary>

![Slide19](https://user-images.githubusercontent.com/118953928/210832527-d50c3b61-62d0-4d53-b3ba-5ce19ae513f2.JPG)
![Slide20](https://user-images.githubusercontent.com/118953928/210832533-ce78f1b3-ae24-4208-8b82-bdd2c65f2e06.JPG)
</details>


<details>
<summary>Simulate And Model All Three Ip’s Together</summary>

![Slide22](https://user-images.githubusercontent.com/118953928/210958013-55e9ba72-e9fd-4dfb-9f82-8500bd77d705.JPG)
![Slide23](https://user-images.githubusercontent.com/118953928/210958017-00ae8ac2-9c6d-4f3b-8250-f0ac8a49ad64.JPG)
</details>

<details>
<summary>Difference Table For All The Modes In Interactive Mode</summary>

![Slide24](https://user-images.githubusercontent.com/118953928/210832625-b63c4421-154a-4543-be34-98e3abcb7126.JPG)
</details>
	
<details>
<summary>One Take A Example Circuit For Example</summary>

![Slide26](https://user-images.githubusercontent.com/118953928/210832683-a5bfa519-362c-4413-af53-aa71dd7cb30e.JPG)
![Slide27](https://user-images.githubusercontent.com/118953928/210832696-efcd90a1-59e5-421b-95f6-d2fc4792751d.JPG)
</details>



	
## Day 13 -  Post-synthesis simulation

<details>
<summary>Theory</summary>

</details>
