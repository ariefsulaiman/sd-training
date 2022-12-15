# This is my first repository

## Table of content

[Day 0 - System/Tool Setup Check. GitHub ID creation](https://github.com/ariefsulaiman/sd-training/blob/main/Readme.md#day-0---systemtool-setup-check-github-id-creation)\
[Day 1 - Introduction to Verilog RTL design and Synthesis](https://github.com/ariefsulaiman/sd-training/blob/main/Readme.md#day-1---introduction-to-verilog-rtl-design-and-synthesis)\
[Day 2 - Timing libs(QTMs/ETMs), hierarchical vs flat synthesis and efficient flop coding styles](https://github.com/ariefsulaiman/sd-training/blob/main/Readme.md#day-2---timing-libsqtmsetms-hierarchical-vs-flat-synthesis-and-efficient-flop-coding-styles)\
[Day 3 - Combinational and Sequential Optimizations](https://github.com/ariefsulaiman/sd-training/blob/main/Readme.md#day-3---combinational-and-sequential-optimizations)\
[Day 4 - GLS, blocking vs non-blocking and Synthesis-Simulation mismatch](https://github.com/ariefsulaiman/sd-training/blob/main/Readme.md#day-4---gls-blocking-vs-non-blocking-and-synthesis-simulation-mismatch)

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
  
  content
  
  </details>
  





