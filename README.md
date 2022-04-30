# RTL design using Verilog with SKY130 Technology

This repository is created to document all the theory and labs done as a part of cloud based 5-day workshop on RTL design using verilog with sky130 technology.

![image](https://user-images.githubusercontent.com/75198926/165884648-3ef050ce-e181-46d6-a8af-00eaa7f70260.png)

# Table of contents
- [Brief description of workshop](https://github.com/nkty02/sky130-RTL-Design-Workshop/edit/main/README.md#brief-description-of-workshop)
- [Day 1: Introduction to verilog RTL design and synthesis](https://github.com/nkty02/sky130-RTL-Design-Workshop/edit/main/README.md#day-1-introduction-to-verilog-rtl-design-and-synthesis)
  - [Introduction to open-source simulator iverilog](https://github.com/nkty02/sky130-RTL-Design-Workshop/edit/main/README.md#introduction-to-open-source-simulator-iverilog)
    - [Introduction to iverilog, design and testbench](https://github.com/nkty02/sky130-RTL-Design-Workshop/edit/main/README.md#introduction-to-iverilog-design-and-testbench) 
  - [Labs using iverilog and gtkwave]()
    - [Introduction to lab]()
    - [Introduction to iverilog gtkwave part-1]()
    - [Introduction to iverilog gtkwave part-2]() 
  - [Introduction to Yosys and logic synthesis]()
    - [Introduction to Yosys]() 
    - [Introduction to logic synthesis part-1]()
    - [Introduction to logic synthesis part-2]()
  - [Labs using Yosys and Sky130 PDKs]()
    - [Yosys good_mux part-1]()
    - [Yosys good_mux part-2]()
    - [Yosys good_mux part-3]()  
- [Day 2: Timing libs, hierarchical vs flat synthesis and efficient flop coding styles]()
  - [Introduction to timing .libs]()
    - [Introduction to .lib part-1]() 
    - [Introduction to .lib part-2]() 
    - [Introduction to .lib part-3]()
  - [Hierarchical vs Flat synthesis]()
    - [Hier synthesis flat synthesis part-1]()
    - [Hier synthesis flat synthesis part-2]() 
  - [Various flop coding styles and optimization]()
    - [Why flops and flop coding styles part-1]() 
    - [Why flops and flop coding styles part-2]()
    - [Flop synthesis simulations lab part-1]()
    - [Flop synthesis simulations lab part-2]()
    - [Interesting optimisations part-1]()
    - [Interesting optimisations part-2]()  
- [Day 3: Combinational and sequential optimisations]()
  - [Introduction to optimisations]()
    - [Introduction to optimisations part-1]() 
    - [Introduction to optimisations part-2]() 
    - [Introduction to optimisations part-3]()
  - [Combinational logic optimisations]()
    - [Combinational logic optimisations part-1]()
    - [Combinational logic optimisations part-2]()
  - [Sequential logic optimisations]()
    - [Sequential logic optimisations part-1]()
    - [Sequential logic optimisations part-2]() 
    - [Sequential logic optimisations part-3]()
  - [Sequential optimisations for unused outputs]()
    - [Sequential optimisations for unused outputs part-1]() 
    - [Sequential optimisations for unused outputs part-2]()      
- [Author]()
- [Acknowledgements]()


# Brief description of workshop

The goal of this workshop is to teach the verilog coding principles, which produce predictable logic in silicon. It's vital to remember that not all verilog code is synthesizable, and even if it is, alternative logic may result depending on the coding style utilised. All of these components of the Verilog HDL are covered in depth in this course, which includes both theory and plenty of practical examples. 
This workshop will train you:
- How to construct digital logic using Verilog HDL. 
- Using Functional Simulation to verify the design's functionality. 
- Writing Test Benches to ensure the RTL design's functionality. 
- Synthesis of the Functional RTL Code's logic. 
- Simulate the synthesized netlist at the gate level.

# Day 1: Introduction to verilog RTL design and synthesis
## Introduction to open-source simulator iverilog
### Introduction to iverilog, design and testbench

**RTL Design** : 

Design is the actual verilog code or set of verilog codes which performs the intended functionality as defined by the specifications(specs). Register-transfer level (RTL) is a design abstraction for modelling a synchronous digital circuit in terms of the flow of digital signals (data) between hardware registers and the logical operations performed on those signals in digital circuit design. 


**Test Bench** : 

After writing code for our design we need to check whether our design is fulfilling all the specifications given to us. For this we need to test our design for various inputs and observe whether our outputs are according to specs or not. So a testbench is a code file setup used to apply stimulus i.e., test_vectors to the design to check its functionality.  

*The below figures describes how a test bench file is used to instantiate the RTL design, apply stimulus to the design and observe the stimulus received from the RTL design to the applied input stimulus and dump those results to .vcd file. Test bench doesnot have any primary inputs and primary outputs. But a RTL design can have any number of primary inputs and primary outputs.* 

![image](https://user-images.githubusercontent.com/75198926/165922382-df74bc91-9de1-4853-9b5b-2667913a0c41.png)

<!-- <img src="https://user-images.githubusercontent.com/75198926/165922382-df74bc91-9de1-4853-9b5b-2667913a0c41.png" width="700" height="300"> --->


**Simulator** : 

A simulator is a tool used to check the functionality of a design. RTL design is the implementation of spec and the correctness of the implementation of spec through RTL design is checked by simulating the design using a simulator. This step is very much helpful in early stage of RTL design as it checks for errors in code and also used to fix those errors. In this course of workshop we used [iverilog](http://iverilog.icarus.com/) tool to simulate our designs. This tool [Icarus Verilog](http://iverilog.icarus.com/) in short [iverilog](http://iverilog.icarus.com/) is an open source Verilog simulation and synthesis tool. For iverilog we need RTL design file and a testbench file to run the simulation. 

*Though this tool iverilog can be used as a simulator and synthesizer, but we use Yosys for synthesis because of its extended advantages over iverilog.* 

**How simulator works**
* Simulator looks for changes in the input signals. 
* It evaluates output only upon change in input signal. 
  * If there no change to the input, then output is not at all evaluated. 

*The below figure illustrates the iverilog based simulation flow where the iverilog simulator takes two input files design file and testbench file and dumps the changes in the output into a .vcd(Value Change Dump) file. Here we use gtkwave tool to view the output waveform generated using this .vcd file.* 

![image](https://user-images.githubusercontent.com/75198926/165926114-1a6a40df-667c-45fb-bc30-62aa8ca97a17.png)


## Labs using iverilog and gtkwave
### Introduction to lab

First we need to create a directory named VLSI to install the tools required to perform during this workshop. For that we open the home folder in the terminal and from there VLSI folder is created in home folder using ``` mkdir VLSI ``` command in the terminal. Then we enter that directory using the command ``` cd VLSI ``` to do git cloning. The vsdflow tools are already installed in our system so we need not do any git cloning for vsdflow tools installation. We did git cloning from this website **https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git** using the command ``` git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git ```. The contents present in that directory after git cloning is as shown in below figure.

![image](https://user-images.githubusercontent.com/75198926/165930928-fe381136-a641-4b83-9fc2-3f58746ba3b4.png)

After git cloning **sky130RTLDesignAndSynthesisWorkshop** is installed in our VLSI directory.

**Contents of sky130RTLDesignAndSynthesisWorkshop directory**

![image](https://user-images.githubusercontent.com/75198926/165932902-66a55778-b470-4563-96eb-28446021f956.png)

``` 
DC_WORKSHOP  
README.md	
my_lib	
verilog_files  
yosys_run.sh 
```

**Contents of my_lib**

![image](https://user-images.githubusercontent.com/75198926/165933517-57b76fea-60e3-43a0-a7de-bffb2d654c33.png)

``` 
lib  
verilog_model
```

**Contents of lib** : 

This contains the sky130_fd_sc_hd__tt_025C_1v80.lib standard cell library file which is used for synthesis.

![image](https://user-images.githubusercontent.com/75198926/165933978-35d339cf-9b96-4978-abed-f9edbe9edaa4.png)

``` 
sky130_fd_sc_hd__tt_025C_1v80.lib
```

**Contents of verilog_model** : 

This contains all standard cells in verilog model of all the standard cells present in the .lib library file mentioned above.

![image](https://user-images.githubusercontent.com/75198926/165934379-918175d2-4912-401d-8acc-46364d02bd4c.png)

``` 
primitives.v  
sky130_fd_sc_hd.v
```

**Contents of verilog_files** :

This verilog_files folder contains all our verilog source files and testbench files to perform our lab experiments.

![image](https://user-images.githubusercontent.com/75198926/165935108-d5b1aba1-41e1-406a-a210-f98f61b5d3e3.png)

Here we can see lot of verilog design files along with corresponding testbench files too.

``` 
a_trans		   blocking_caveat_net.v   dff_const2.v        incomp_case.v		mux_spice.v			tb_bad_counter.v      tb_dff_asyncres.v		 tb_good_shift_reg.v	   tb_ripple_counter.v
bad_case.v	   comp_case.v		   dff_const3.v        incomp_if.v		net.v				tb_bad_latch.v	      tb_dff_asyncres_syncres.v  tb_incomp_case.v	   tb_ternary_operator_mux.v
bad_case_net.v	   counter_opt.v	   dff_const4.v        incomp_if2.v		opt_check.v			tb_bad_latch2.v       tb_dff_const1.v		 tb_incomp_if.v		   tb_up_dn_cntr.v
bad_counter.v	   counter_opt2.v	   dff_const5.v        mul2_net.v		opt_check2.v			tb_bad_mux.v	      tb_dff_const2.v		 tb_incomp_if2.v	   tb_up_dn_cntr_with_load.v
bad_latch.v	   demux_case.v		   dff_net.v	       mult_2.v			opt_check3.v			tb_bad_shift_reg.v    tb_dff_const3.v		 tb_multiple_modules.v	   tb_up_dn_cntr_with_load_with_start_stop.v
bad_latch_2.v	   demux_generate.v	   dff_syncres.v       mult_8.v			opt_check4.v			tb_bad_shift_reg2.v   tb_dff_const4.v		 tb_mux_generate.v	   tb_upcntr.v
bad_latch_net.v    dff_ares.net.v	   fa.v		       multiple_module_opt.v	partial_case_assign.v		tb_blocking_caveat.v  tb_dff_const5.v		 tb_opt_check.v		   ternary_operator_mux.v
bad_mux.v	   dff_async_set.v	   good_counter.v      multiple_module_opt2.v	pattern_detect_fsm.v		tb_comp_case.v	      tb_dff_syncres.v		 tb_opt_check2.v	   ternary_operator_mux_net.v
bad_mux_net.v	   dff_asyncres.v	   good_latch.v        multiple_modules.v	pattern_detect_fsm_bad_style.v	tb_counter_opt.v      tb_good_counter.v		 tb_opt_check3.v	   up_dn_cntr.v
bad_shift_reg.v    dff_asyncres_net.v	   good_mux.v	       multiple_modules_flat.v	rca.v				tb_demux_case.v       tb_good_latch.v		 tb_partial_case_assign.v  up_dn_cntr_with_load.v
bad_shift_reg2.v   dff_asyncres_syncres.v  good_mux_netlist.v  multiple_modules_hier.v	ripple_counter.v		tb_demux_generate.v   tb_good_mux.v		 tb_pattern_detect_fsm.v   up_dn_cntr_with_load_with_start_stop.v
blocking_caveat.v  dff_const1.v		   good_shift_reg.v    mux_generate.v		tb_bad_case.v			tb_dff_async_set.v    tb_good_mux.vcd		 tb_rca.v		   upcntr.v

```

### Introduction to iverilog gtkwave part-1

In this lab we are going to see how to work with iverilog and gtkwave. 

*Loading a verilog file **good_mux.v** and corresponding testbench **tb_good_mux** into iverilog simulator :*

``` 
iverilog good_mux.v tb_good_mux.v 
```
Now we can see that a file called "a.out" is been created.
![image](https://user-images.githubusercontent.com/75198926/165936634-2531ad7e-d227-4b8f-ab2f-ea7c53d515c3.png)

``` 
a.out		   blocking_caveat_net.v   dff_const2.v        incomp_case.v		mux_spice.v			tb_bad_counter.v      tb_dff_asyncres.v		 tb_good_shift_reg.v	   tb_ripple_counter.v
bad_case.v	   comp_case.v		   dff_const3.v        incomp_if.v		net.v				tb_bad_latch.v	      tb_dff_asyncres_syncres.v  tb_incomp_case.v	   tb_ternary_operator_mux.v
bad_case_net.v	   counter_opt.v	   dff_const4.v        incomp_if2.v		opt_check.v			tb_bad_latch2.v       tb_dff_const1.v		 tb_incomp_if.v		   tb_up_dn_cntr.v
bad_counter.v	   counter_opt2.v	   dff_const5.v        mul2_net.v		opt_check2.v			tb_bad_mux.v	      tb_dff_const2.v		 tb_incomp_if2.v	   tb_up_dn_cntr_with_load.v
bad_latch.v	   demux_case.v		   dff_net.v	       mult_2.v			opt_check3.v			tb_bad_shift_reg.v    tb_dff_const3.v		 tb_multiple_modules.v	   tb_up_dn_cntr_with_load_with_start_stop.v
bad_latch_2.v	   demux_generate.v	   dff_syncres.v       mult_8.v			opt_check4.v			tb_bad_shift_reg2.v   tb_dff_const4.v		 tb_mux_generate.v	   tb_upcntr.v
bad_latch_net.v    dff_ares.net.v	   fa.v		       multiple_module_opt.v	partial_case_assign.v		tb_blocking_caveat.v  tb_dff_const5.v		 tb_opt_check.v		   ternary_operator_mux.v
bad_mux.v	   dff_async_set.v	   good_counter.v      multiple_module_opt2.v	pattern_detect_fsm.v		tb_comp_case.v	      tb_dff_syncres.v		 tb_opt_check2.v	   ternary_operator_mux_net.v
bad_mux_net.v	   dff_asyncres.v	   good_latch.v        multiple_modules.v	pattern_detect_fsm_bad_style.v	tb_counter_opt.v      tb_good_counter.v		 tb_opt_check3.v	   up_dn_cntr.v
bad_shift_reg.v    dff_asyncres_net.v	   good_mux.v	       multiple_modules_flat.v	rca.v				tb_demux_case.v       tb_good_latch.v		 tb_partial_case_assign.v  up_dn_cntr_with_load.v
bad_shift_reg2.v   dff_asyncres_syncres.v  good_mux_netlist.v  multiple_modules_hier.v	ripple_counter.v		tb_demux_generate.v   tb_good_mux.v		 tb_pattern_detect_fsm.v   up_dn_cntr_with_load_with_start_stop.v
blocking_caveat.v  dff_const1.v		   good_shift_reg.v    mux_generate.v		tb_bad_case.v			tb_dff_async_set.v    tb_good_mux.vcd		 tb_rca.v		   upcntr.v

```
*Now we will execute this a.out file so that the simulator iverilog will dump the output to .vcd file named **"tb_good_mux.vcd"**.*

The command used to execute this operation is as follows
```
./a.out
```

![image](https://user-images.githubusercontent.com/75198926/165937062-0a58b283-e163-4a70-a349-fdc3a1ee7aba.png)

*Now we will load this .vcd file named **"tb_good_mux.vcd"** into gtkwave tool to view the output waveform of good_mux design.*

The command used to execute this operation is as follows
```
gtkwave tb_good_mux.vcd
``` 
Now gtkwave window will appear where we can see the testbench tb_good_mux and under that we have uut(Unit Under Test). If we click on the testbench we can see primary inputs and primary output given to the good_mux design. We need to drag and drop the inputs under signals to view the corresponding waveform. 

![image](https://user-images.githubusercontent.com/75198926/165938211-bcffac46-8588-4c27-894f-38d1600a9c18.png)

![image](https://user-images.githubusercontent.com/75198926/165938673-391beabb-9538-4c2f-9487-653366d5b1cc.png)

Here we can observe the multiplexer operation i.e., 
- whenever sel = 0; then output is following i0 (y = i0) and 
- whenever sel = 1; then output is following i1 (y = i1)


### Introduction to iverilog gtkwave part-2

Now we look into the RTL design and corresponding testbench files for good_mux design.
To view those files we use the following command :
``` gvim tb_good_mux.v -o good_mux.v ```

A new window opens where the good_mux(design file) and tb_good_mux(testbench file) are opened. 

![image](https://user-images.githubusercontent.com/75198926/165939444-b308cc31-dbdb-42a0-90a7-fc5b2268cdb4.png)

**Design file - good_mux.v** :

It contains the verilog code of multiplexer implementation. The module was named as good_mux. And it takes 3 inputs i0, i1, sel and gives 1 output y. The logic is as follows :

- If (sel = 1)

    - then y = i1 
  
- elseif (sel = 0)

    - then y = i0
  
**Testbench file - tb_good_mux.v** :  

Here we can see that the testbench instantiates the design good_mux. We can also observe that the testbench doesn't contain any rimary inputs or primary outputs. We always call the design instantiation as UUT(Unit Under Test) or DUT(Design Under Test). Then we start dumping the .vcd file named *tb_good_mux.vcd*. Then we have the stimulus generator, it says that initially sel = 0; i0 = 0; i1 = 0 and we are running the simulator for 300nsec and stopping the simulation. Then we apply inputs to our design by toggling the sel, i0, i1 signals. Here we don't have any stimulus observer we are just dumping the output to .vcd file named *tb_good_mux.vcd* and then view the output waveform using gtkwave.


## Introduction to Yosys and logic synthesis

### Introduction to Yosys

[Yosys](https://www.yosyshq.com/open-source) is a open source framework used for RTL synthesis and more. A synthesizer is a tool used for converting the RTL design into netist. [Yosys](https://www.yosyshq.com/open-source) is the synthesizer that we use in this course. To obtain the netlist we need to input 2 files: RTL design file and the .lib file to the synthesizer, here Yosys. 

**Netlist is the representation of the RTL design using the standard cells present in the inputted .lib libaray file**

The flow of synthesis and Yosys setup is as follows:

- we have read_verilog command to read the RTL design
- read_liberty command to read the .lib file
- write_verilog command to write out the netlist file

![image](https://user-images.githubusercontent.com/75198926/165951354-8ca34005-4f19-4f6d-9bb5-34567d61b06b.png)

**Verification of synthesis:**

For verification of the synthesis done by Yosys we use the simulator iverilog. We input netlist and the testbench to the iverilog simulator and if we get the output .vcd file same as previous .vcd file named as "tb_good_mux.vcd", then our synthesis is correct. The flow diagram is shown below:

![image](https://user-images.githubusercontent.com/75198926/165955010-2da013f7-8402-4921-8031-e4a3f83ac6d0.png)

**Note** : The set of primary inputs and primary outputs remains same between the RTL design and the synthesized netlist. So we can use the same testbech to simulate both the files. 


### Introduction to logic synthesis part-1

**RTL Design** : It is the behavioural representation at the Register-Transfer-Level of the given specifications in a Verilog Hardware Description Language(VHDL). 

**Synthesis** : Synthesis is used to map the RTL code to the digital hardware design(netlist). It make the RTL to gate level transition. The design is converted into gates and the connections are made between the gates. This is given out as a Netlist file. The follwing is the flow diagram of the synthesis process. 

![image](https://user-images.githubusercontent.com/75198926/165958406-58a613bd-875a-44b8-9ca7-e1c2434484eb.png)

**What is .lib ?** 

It is the collection of the logical modules which includes all basic logical gates like and, or, nor, nand, etc.. It also contains different flavours of the same gate like slow, medium, fast all 3 versions of 2-input nand gate and 3-input nand gate and so on.

**Why do we need different flavours of same gate ?**

Lets assume we have two FF's A and B connected together by a combinational block as shown in below figure. 
![image](https://user-images.githubusercontent.com/75198926/165960559-20ab0807-0577-4942-aeea-682514a9d1c8.png)

Here the speed of operation of the total digital circuit depends on the delay in the combinational logic block. The time period of the clock must be atleast greater than the propagation delay of FF-A + delay in the combinational logic part + setup time of the FF-B. **So to increase the speed of operation or to achieve maximum clock speed for the digital circuit we need *faster cells* in the combinational logic block.** 

### Introduction to logic synthesis part-2

**Why do we need slow cells ?**

Silmiar to setup time there is hold time for FF-B. Hold time is the minimum time required for the input to latched at FF-A and the time after which the input is captured at FF-B. The minimum delay time should be graeter than the hold time of FF-B. Hold time of FF-B is less than propagation delay of FF-A + delay in the combinational logic part. To ensure that there are no "HOLD" issues at DFF_B, we need cells that work slowly.

- *Hence we need cells that work fast to meet the required performance and we need cells that work slow to meet HOLD time*
- *The collection of various types of cells forms the .lib*

**Faster cells vs Slower cells**

- Faster cells require fast charging/ discharging of the capacitor which requires high current and this is possible for wider width transistors which occupy more space and consume more power.
- Slower cells require slow charging/ discharging of the capacitor which requires low current and this is possible for small width transistors which occupy less space and consume less power.

*Therefore, we need to guide the synthesizer to select the flavour of cells that is optimum for the implementation of logic circuit.*

## Labs using Yosys and Sky130 PDKs

First we need to invoke Yosys using the following command :

```
yosys
```
![image](https://user-images.githubusercontent.com/75198926/165981381-eaf71959-bf0b-44c2-9a28-f3dc7014b1ef.png)

- First we need to read the .lib library file using the following command :

```
read_liberty -lib ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```

![image](https://user-images.githubusercontent.com/75198926/165982101-e33e10c0-4bb3-47f1-871a-296fae55767a.png)

- Next we need to read the design file using the following command :

```
read_verilog good_mux.v
```

![image](https://user-images.githubusercontent.com/75198926/165984361-a503ebc9-e5cb-45e0-9793-9c9fd7a31469.png)

- Next we need to synthesis using the following command :

```
synth -top good_mux
```

![image](https://user-images.githubusercontent.com/75198926/165984841-e3e4203e-63b4-49f4-95af-e383c1fdb6f2.png)

```
yosys> synth -top good_mux

3. Executing SYNTH pass.

3.1. Executing HIERARCHY pass (managing design hierarchy).

3.1.1. Analyzing design hierarchy..
Top module:  \good_mux

3.1.2. Analyzing design hierarchy..
Top module:  \good_mux
Removed 0 unused modules.

3.2. Executing PROC pass (convert processes to netlists).

3.2.1. Executing PROC_CLEAN pass (remove empty switches from decision trees).
Cleaned up 0 empty switches.

3.2.2. Executing PROC_RMDEAD pass (remove dead branches from decision trees).
Marked 1 switch rules as full_case in process $proc$good_mux.v:3$1 in module good_mux.
Removed a total of 0 dead cases.

3.2.3. Executing PROC_PRUNE pass (remove redundant assignments in processes).
Removed 1 redundant assignment.
Promoted 0 assignments to connections.

3.2.4. Executing PROC_INIT pass (extract init attributes).

3.2.5. Executing PROC_ARST pass (detect async resets in processes).

3.2.6. Executing PROC_MUX pass (convert decision trees to multiplexers).
Creating decoders for process `\good_mux.$proc$good_mux.v:3$1'.
     1/1: $0\y[0:0]

3.2.7. Executing PROC_DLATCH pass (convert process syncs to latches).
No latch inferred for signal `\good_mux.\y' from process `\good_mux.$proc$good_mux.v:3$1'.

3.2.8. Executing PROC_DFF pass (convert process syncs to FFs).

3.2.9. Executing PROC_MEMWR pass (convert process memory writes to cells).

3.2.10. Executing PROC_CLEAN pass (remove empty switches from decision trees).
Found and cleaned up 1 empty switch in `\good_mux.$proc$good_mux.v:3$1'.
Removing empty process `good_mux.$proc$good_mux.v:3$1'.
Cleaned up 1 empty switch.

3.3. Executing OPT_EXPR pass (perform const folding).
Optimizing module good_mux.

3.4. Executing OPT_CLEAN pass (remove unused cells and wires).
Finding unused cells or wires in module \good_mux..
Removed 0 unused cells and 3 unused wires.
<suppressed ~1 debug messages>

3.5. Executing CHECK pass (checking for obvious problems).
Checking module good_mux...
Found and reported 0 problems.

3.6. Executing OPT pass (performing simple optimizations).

3.6.1. Executing OPT_EXPR pass (perform const folding).
Optimizing module good_mux.

3.6.2. Executing OPT_MERGE pass (detect identical cells).
Finding identical cells in module `\good_mux'.
Removed a total of 0 cells.

3.6.3. Executing OPT_MUXTREE pass (detect dead branches in mux trees).
Running muxtree optimizer on module \good_mux..
  Creating internal representation of mux trees.
  Evaluating internal representation of mux trees.
  Analyzing evaluation results.
Removed 0 multiplexer ports.
<suppressed ~1 debug messages>

3.6.4. Executing OPT_REDUCE pass (consolidate $*mux and $reduce_* inputs).
  Optimizing cells in module \good_mux.
Performed a total of 0 changes.

3.6.5. Executing OPT_MERGE pass (detect identical cells).
Finding identical cells in module `\good_mux'.
Removed a total of 0 cells.

3.6.6. Executing OPT_DFF pass (perform DFF optimizations).

3.6.7. Executing OPT_CLEAN pass (remove unused cells and wires).
Finding unused cells or wires in module \good_mux..

3.6.8. Executing OPT_EXPR pass (perform const folding).
Optimizing module good_mux.

3.6.9. Finished OPT passes. (There is nothing left to do.)

3.7. Executing FSM pass (extract and optimize FSM).

3.7.1. Executing FSM_DETECT pass (finding FSMs in design).

3.7.2. Executing FSM_EXTRACT pass (extracting FSM from design).

3.7.3. Executing FSM_OPT pass (simple optimizations of FSMs).

3.7.4. Executing OPT_CLEAN pass (remove unused cells and wires).
Finding unused cells or wires in module \good_mux..

3.7.5. Executing FSM_OPT pass (simple optimizations of FSMs).

3.7.6. Executing FSM_RECODE pass (re-assigning FSM state encoding).

3.7.7. Executing FSM_INFO pass (dumping all available information on FSM cells).

3.7.8. Executing FSM_MAP pass (mapping FSMs to basic logic).

3.8. Executing OPT pass (performing simple optimizations).

3.8.1. Executing OPT_EXPR pass (perform const folding).
Optimizing module good_mux.

3.8.2. Executing OPT_MERGE pass (detect identical cells).
Finding identical cells in module `\good_mux'.
Removed a total of 0 cells.

3.8.3. Executing OPT_MUXTREE pass (detect dead branches in mux trees).
Running muxtree optimizer on module \good_mux..
  Creating internal representation of mux trees.
  Evaluating internal representation of mux trees.
  Analyzing evaluation results.
Removed 0 multiplexer ports.
<suppressed ~1 debug messages>

3.8.4. Executing OPT_REDUCE pass (consolidate $*mux and $reduce_* inputs).
  Optimizing cells in module \good_mux.
Performed a total of 0 changes.

3.8.5. Executing OPT_MERGE pass (detect identical cells).
Finding identical cells in module `\good_mux'.
Removed a total of 0 cells.

3.8.6. Executing OPT_DFF pass (perform DFF optimizations).

3.8.7. Executing OPT_CLEAN pass (remove unused cells and wires).
Finding unused cells or wires in module \good_mux..

3.8.8. Executing OPT_EXPR pass (perform const folding).
Optimizing module good_mux.

3.8.9. Finished OPT passes. (There is nothing left to do.)

3.9. Executing WREDUCE pass (reducing word size of cells).

3.10. Executing PEEPOPT pass (run peephole optimizers).

3.11. Executing OPT_CLEAN pass (remove unused cells and wires).
Finding unused cells or wires in module \good_mux..

3.12. Executing ALUMACC pass (create $alu and $macc cells).
Extracting $alu and $macc cells in module good_mux:
  created 0 $alu and 0 $macc cells.

3.13. Executing SHARE pass (SAT-based resource sharing).

3.14. Executing OPT pass (performing simple optimizations).

3.14.1. Executing OPT_EXPR pass (perform const folding).
Optimizing module good_mux.

3.14.2. Executing OPT_MERGE pass (detect identical cells).
Finding identical cells in module `\good_mux'.
Removed a total of 0 cells.

3.14.3. Executing OPT_MUXTREE pass (detect dead branches in mux trees).
Running muxtree optimizer on module \good_mux..
  Creating internal representation of mux trees.
  Evaluating internal representation of mux trees.
  Analyzing evaluation results.
Removed 0 multiplexer ports.
<suppressed ~1 debug messages>

3.14.4. Executing OPT_REDUCE pass (consolidate $*mux and $reduce_* inputs).
  Optimizing cells in module \good_mux.
Performed a total of 0 changes.

3.14.5. Executing OPT_MERGE pass (detect identical cells).
Finding identical cells in module `\good_mux'.
Removed a total of 0 cells.

3.14.6. Executing OPT_DFF pass (perform DFF optimizations).

3.14.7. Executing OPT_CLEAN pass (remove unused cells and wires).
Finding unused cells or wires in module \good_mux..

3.14.8. Executing OPT_EXPR pass (perform const folding).
Optimizing module good_mux.

3.14.9. Finished OPT passes. (There is nothing left to do.)

3.15. Executing MEMORY pass.

3.15.1. Executing OPT_MEM pass (optimize memories).
Performed a total of 0 transformations.

3.15.2. Executing MEMORY_DFF pass (merging $dff cells to $memrd).

3.15.3. Executing OPT_CLEAN pass (remove unused cells and wires).
Finding unused cells or wires in module \good_mux..

3.15.4. Executing OPT_MEM_FEEDBACK pass (finding memory read-to-write feedback paths).

3.15.5. Executing MEMORY_SHARE pass (consolidating $memrd/$memwr cells).

3.15.6. Executing OPT_CLEAN pass (remove unused cells and wires).
Finding unused cells or wires in module \good_mux..

3.15.7. Executing MEMORY_COLLECT pass (generating $mem cells).

3.16. Executing OPT_CLEAN pass (remove unused cells and wires).
Finding unused cells or wires in module \good_mux..

3.17. Executing OPT pass (performing simple optimizations).

3.17.1. Executing OPT_EXPR pass (perform const folding).
Optimizing module good_mux.

3.17.2. Executing OPT_MERGE pass (detect identical cells).
Finding identical cells in module `\good_mux'.
Removed a total of 0 cells.

3.17.3. Executing OPT_DFF pass (perform DFF optimizations).

3.17.4. Executing OPT_CLEAN pass (remove unused cells and wires).
Finding unused cells or wires in module \good_mux..

3.17.5. Finished fast OPT passes.

3.18. Executing MEMORY_MAP pass (converting memories to logic and flip-flops).

3.19. Executing OPT pass (performing simple optimizations).

3.19.1. Executing OPT_EXPR pass (perform const folding).
Optimizing module good_mux.

3.19.2. Executing OPT_MERGE pass (detect identical cells).
Finding identical cells in module `\good_mux'.
Removed a total of 0 cells.

3.19.3. Executing OPT_MUXTREE pass (detect dead branches in mux trees).
Running muxtree optimizer on module \good_mux..
  Creating internal representation of mux trees.
  Evaluating internal representation of mux trees.
  Analyzing evaluation results.
Removed 0 multiplexer ports.
<suppressed ~1 debug messages>

3.19.4. Executing OPT_REDUCE pass (consolidate $*mux and $reduce_* inputs).
  Optimizing cells in module \good_mux.
Performed a total of 0 changes.

3.19.5. Executing OPT_MERGE pass (detect identical cells).
Finding identical cells in module `\good_mux'.
Removed a total of 0 cells.

3.19.6. Executing OPT_SHARE pass.

3.19.7. Executing OPT_DFF pass (perform DFF optimizations).

3.19.8. Executing OPT_CLEAN pass (remove unused cells and wires).
Finding unused cells or wires in module \good_mux..

3.19.9. Executing OPT_EXPR pass (perform const folding).
Optimizing module good_mux.

3.19.10. Finished OPT passes. (There is nothing left to do.)

3.20. Executing TECHMAP pass (map to technology primitives).

3.20.1. Executing Verilog-2005 frontend: /usr/local/bin/../share/yosys/techmap.v
Parsing Verilog input from `/usr/local/bin/../share/yosys/techmap.v' to AST representation.
Generating RTLIL representation for module `\_90_simplemap_bool_ops'.
Generating RTLIL representation for module `\_90_simplemap_reduce_ops'.
Generating RTLIL representation for module `\_90_simplemap_logic_ops'.
Generating RTLIL representation for module `\_90_simplemap_compare_ops'.
Generating RTLIL representation for module `\_90_simplemap_various'.
Generating RTLIL representation for module `\_90_simplemap_registers'.
Generating RTLIL representation for module `\_90_shift_ops_shr_shl_sshl_sshr'.
Generating RTLIL representation for module `\_90_shift_shiftx'.
Generating RTLIL representation for module `\_90_fa'.
Generating RTLIL representation for module `\_90_lcu'.
Generating RTLIL representation for module `\_90_alu'.
Generating RTLIL representation for module `\_90_macc'.
Generating RTLIL representation for module `\_90_alumacc'.
Generating RTLIL representation for module `\$__div_mod_u'.
Generating RTLIL representation for module `\$__div_mod_trunc'.
Generating RTLIL representation for module `\_90_div'.
Generating RTLIL representation for module `\_90_mod'.
Generating RTLIL representation for module `\$__div_mod_floor'.
Generating RTLIL representation for module `\_90_divfloor'.
Generating RTLIL representation for module `\_90_modfloor'.
Generating RTLIL representation for module `\_90_pow'.
Generating RTLIL representation for module `\_90_pmux'.
Generating RTLIL representation for module `\_90_lut'.
Successfully finished Verilog frontend.

3.20.2. Continuing TECHMAP pass.
Using extmapper simplemap for cells of type $mux.
No more expansions possible.
<suppressed ~68 debug messages>

3.21. Executing OPT pass (performing simple optimizations).

3.21.1. Executing OPT_EXPR pass (perform const folding).
Optimizing module good_mux.

3.21.2. Executing OPT_MERGE pass (detect identical cells).
Finding identical cells in module `\good_mux'.
Removed a total of 0 cells.

3.21.3. Executing OPT_DFF pass (perform DFF optimizations).

3.21.4. Executing OPT_CLEAN pass (remove unused cells and wires).
Finding unused cells or wires in module \good_mux..

3.21.5. Finished fast OPT passes.

3.22. Executing ABC pass (technology mapping using ABC).

3.22.1. Extracting gate netlist of module `\good_mux' to `<abc-temp-dir>/input.blif'..
Extracted 1 gates and 4 wires to a netlist network with 3 inputs and 1 outputs.

3.22.1.1. Executing ABC.
Running ABC command: <yosys-exe-dir>/yosys-abc -s -f <abc-temp-dir>/abc.script 2>&1
ABC: ABC command line: "source <abc-temp-dir>/abc.script".
ABC: 
ABC: + read_blif <abc-temp-dir>/input.blif 
ABC: + read_library <abc-temp-dir>/stdcells.genlib 
ABC: Entered genlib library with 13 gates from file "<abc-temp-dir>/stdcells.genlib".
ABC: + strash 
ABC: + dretime 
ABC: + map 
ABC: + write_blif <abc-temp-dir>/output.blif 

3.22.1.2. Re-integrating ABC results.
ABC RESULTS:               MUX cells:        1
ABC RESULTS:        internal signals:        0
ABC RESULTS:           input signals:        3
ABC RESULTS:          output signals:        1
Removing temp directory.

3.23. Executing OPT pass (performing simple optimizations).

3.23.1. Executing OPT_EXPR pass (perform const folding).
Optimizing module good_mux.

3.23.2. Executing OPT_MERGE pass (detect identical cells).
Finding identical cells in module `\good_mux'.
Removed a total of 0 cells.

3.23.3. Executing OPT_DFF pass (perform DFF optimizations).

3.23.4. Executing OPT_CLEAN pass (remove unused cells and wires).
Finding unused cells or wires in module \good_mux..
Removed 0 unused cells and 4 unused wires.
<suppressed ~1 debug messages>

3.23.5. Finished fast OPT passes.

3.24. Executing HIERARCHY pass (managing design hierarchy).

3.24.1. Analyzing design hierarchy..
Top module:  \good_mux

3.24.2. Analyzing design hierarchy..
Top module:  \good_mux
Removed 0 unused modules.

3.25. Printing statistics.

=== good_mux ===

   Number of wires:                  4
   Number of wire bits:              4
   Number of public wires:           4
   Number of public wire bits:       4
   Number of memories:               0
   Number of memory bits:            0
   Number of processes:              0
   Number of cells:                  1
     $_MUX_                          1

3.26. Executing CHECK pass (checking for obvious problems).
Checking module good_mux...
Found and reported 0 problems.

```

- Now we need to write the verilog file i.e., we need to generate the netlist using the following command :

```
abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```

```
yosys> abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib

4. Executing ABC pass (technology mapping using ABC).

4.1. Extracting gate netlist of module `\good_mux' to `<abc-temp-dir>/input.blif'..
Extracted 1 gates and 4 wires to a netlist network with 3 inputs and 1 outputs.

4.1.1. Executing ABC.
Running ABC command: <yosys-exe-dir>/yosys-abc -s -f <abc-temp-dir>/abc.script 2>&1
ABC: ABC command line: "source <abc-temp-dir>/abc.script".
ABC: 
ABC: + read_blif <abc-temp-dir>/input.blif 
ABC: + read_lib -w /home/reachkty/VLSI/sky130RTLDesignAndSynthesisWorkshop/verilog_files/../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
ABC: Parsing finished successfully.  Parsing time =     0.18 sec
ABC: Scl_LibertyReadGenlib() skipped cell "sky130_fd_sc_hd__decap_12" without logic function.
ABC: Scl_LibertyReadGenlib() skipped cell "sky130_fd_sc_hd__decap_3" without logic function.
ABC: Scl_LibertyReadGenlib() skipped cell "sky130_fd_sc_hd__decap_4" without logic function.
ABC: Scl_LibertyReadGenlib() skipped cell "sky130_fd_sc_hd__decap_6" without logic function.
ABC: Scl_LibertyReadGenlib() skipped cell "sky130_fd_sc_hd__decap_8" without logic function.
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__dfbbn_1".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__dfbbn_2".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__dfbbp_1".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__dfrbp_1".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__dfrbp_2".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__dfrtn_1".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__dfrtp_1".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__dfrtp_2".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__dfrtp_4".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__dfsbp_1".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__dfsbp_2".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__dfstp_1".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__dfstp_2".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__dfstp_4".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__dfxbp_1".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__dfxbp_2".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__dfxtp_1".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__dfxtp_2".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__dfxtp_4".
ABC: Scl_LibertyReadGenlib() skipped cell "sky130_fd_sc_hd__diode_2" without logic function.
ABC: Scl_LibertyReadGenlib() skipped cell "sky130_fd_sc_hd__dlclkp_1" without logic function.
ABC: Scl_LibertyReadGenlib() skipped cell "sky130_fd_sc_hd__dlclkp_2" without logic function.
ABC: Scl_LibertyReadGenlib() skipped cell "sky130_fd_sc_hd__dlclkp_4" without logic function.
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__dlrbn_1".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__dlrbn_2".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__dlrbp_1".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__dlrbp_2".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__dlrtn_1".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__dlrtn_2".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__dlrtn_4".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__dlrtp_1".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__dlrtp_2".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__dlrtp_4".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__dlxbn_1".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__dlxbn_2".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__dlxbp_1".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__dlxtn_1".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__dlxtn_2".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__dlxtn_4".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__dlxtp_1".
ABC: Scl_LibertyReadGenlib() skipped three-state cell "sky130_fd_sc_hd__ebufn_1".
ABC: Scl_LibertyReadGenlib() skipped three-state cell "sky130_fd_sc_hd__ebufn_2".
ABC: Scl_LibertyReadGenlib() skipped three-state cell "sky130_fd_sc_hd__ebufn_4".
ABC: Scl_LibertyReadGenlib() skipped three-state cell "sky130_fd_sc_hd__ebufn_8".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__edfxbp_1".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__edfxtp_1".
ABC: Scl_LibertyReadGenlib() skipped three-state cell "sky130_fd_sc_hd__einvn_0".
ABC: Scl_LibertyReadGenlib() skipped three-state cell "sky130_fd_sc_hd__einvn_1".
ABC: Scl_LibertyReadGenlib() skipped three-state cell "sky130_fd_sc_hd__einvn_2".
ABC: Scl_LibertyReadGenlib() skipped three-state cell "sky130_fd_sc_hd__einvn_4".
ABC: Scl_LibertyReadGenlib() skipped three-state cell "sky130_fd_sc_hd__einvn_8".
ABC: Scl_LibertyReadGenlib() skipped three-state cell "sky130_fd_sc_hd__einvp_1".
ABC: Scl_LibertyReadGenlib() skipped three-state cell "sky130_fd_sc_hd__einvp_2".
ABC: Scl_LibertyReadGenlib() skipped three-state cell "sky130_fd_sc_hd__einvp_4".
ABC: Scl_LibertyReadGenlib() skipped three-state cell "sky130_fd_sc_hd__einvp_8".
ABC: Scl_LibertyReadGenlib() skipped cell "sky130_fd_sc_hd__lpflow_bleeder_1" without logic function.
ABC: Scl_LibertyReadGenlib() skipped cell "sky130_fd_sc_hd__lpflow_decapkapwr_12" without logic function.
ABC: Scl_LibertyReadGenlib() skipped cell "sky130_fd_sc_hd__lpflow_decapkapwr_3" without logic function.
ABC: Scl_LibertyReadGenlib() skipped cell "sky130_fd_sc_hd__lpflow_decapkapwr_4" without logic function.
ABC: Scl_LibertyReadGenlib() skipped cell "sky130_fd_sc_hd__lpflow_decapkapwr_6" without logic function.
ABC: Scl_LibertyReadGenlib() skipped cell "sky130_fd_sc_hd__lpflow_decapkapwr_8" without logic function.
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__lpflow_inputisolatch_1".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__sdfbbn_1".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__sdfbbn_2".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__sdfbbp_1".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__sdfrbp_1".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__sdfrbp_2".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__sdfrtn_1".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__sdfrtp_1".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__sdfrtp_2".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__sdfrtp_4".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__sdfsbp_1".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__sdfsbp_2".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__sdfstp_1".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__sdfstp_2".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__sdfstp_4".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__sdfxbp_1".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__sdfxbp_2".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__sdfxtp_1".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__sdfxtp_2".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__sdfxtp_4".
ABC: Scl_LibertyReadGenlib() skipped cell "sky130_fd_sc_hd__sdlclkp_1" without logic function.
ABC: Scl_LibertyReadGenlib() skipped cell "sky130_fd_sc_hd__sdlclkp_2" without logic function.
ABC: Scl_LibertyReadGenlib() skipped cell "sky130_fd_sc_hd__sdlclkp_4" without logic function.
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__sedfxbp_1".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__sedfxbp_2".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__sedfxtp_1".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__sedfxtp_2".
ABC: Scl_LibertyReadGenlib() skipped sequential cell "sky130_fd_sc_hd__sedfxtp_4".
ABC: Library "sky130_fd_sc_hd__tt_025C_1v80" from "/home/reachkty/VLSI/sky130RTLDesignAndSynthesisWorkshop/verilog_files/../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib" has 334 cells (94 skipped: 63 seq; 13 tri-state; 18 no func; 0 dont_use).  Time =     0.25 sec
ABC: Memory =   16.00 MB. Time =     0.25 sec
ABC: Warning: Detected 9 multi-output gates (for example, "sky130_fd_sc_hd__fa_1").
ABC: + strash 
ABC: + ifraig 
ABC: + scorr 
ABC: Warning: The network is combinational (run "fraig" or "fraig_sweep").
ABC: + dc2 
ABC: + dretime 
ABC: + strash 
ABC: + &get -n 
ABC: + &dch -f 
ABC: + &nf 
ABC: + &put 
ABC: + write_blif <abc-temp-dir>/output.blif 

4.1.2. Re-integrating ABC results.
ABC RESULTS:   sky130_fd_sc_hd__mux2_1 cells:        1
ABC RESULTS:        internal signals:        0
ABC RESULTS:           input signals:        3
ABC RESULTS:          output signals:        1
Removing temp directory.
```
*So, abc command is used to convert RTL code file into gates using the standard cells present in the .lib file whose path is also gievn as a part of command.*

```
4.1.2. Re-integrating ABC results.
ABC RESULTS:   sky130_fd_sc_hd__mux2_1 cells:        1
ABC RESULTS:        internal signals:        0
ABC RESULTS:           input signals:        3
ABC RESULTS:          output signals:        1
```

Here we can see that there are 3 input signals, 1 output signal in our design and 0 internal signals in our design. This used sky130_fd_sc_hd__mux2_1 cells to realize a multiplexer which is our good_mux RTL design. 

- We can use ```show``` command to see the logic implementation of the synthesized design.

![image](https://user-images.githubusercontent.com/75198926/165986650-8d245fb4-a0ef-4d00-a13b-1b524ff6badf.png)

![image](https://user-images.githubusercontent.com/75198926/165986794-e0569262-6d56-482a-8b3b-d3fed4ff4a4c.png)

- Now we need to write the netlist using the following command :

```
write_verilog good_mux_netlist.v
```
![image](https://user-images.githubusercontent.com/75198926/165987242-b4376338-185b-49d8-b148-f1f0efd63426.png)

- To open the netlist we used the following command :

```
!gvim good_mux_netlist.v
```

![image](https://user-images.githubusercontent.com/75198926/165987648-0e738b34-3b68-426a-88f4-ae7a358d6298.png)


## Day 2: Timing libs, hierarchical vs flat synthesis and efficient flop coding styles

### Introduction to timing .libs

In this section we looked that exactly a .lib library file contains. We used the following command to open the sky130_fd_sc_hd__tt_025C_1v80.lib library file :

```
gvim ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```

The following library file opens:

![image](https://user-images.githubusercontent.com/75198926/165990583-4e3d5c44-795e-4988-b6f5-ab53bf85f25e.png)

- The first line tells the name of the library it's **sky130_fd_sc_hd__tt_025C_1v80.lib**. It is a 130nm technology library(sky130 idicates this) and *tt* indicates that this library is typical library and the *025C* indicates that temperature is 25 degrees celsius for this library, and *1v80* indicates that the rail voltage for this library is 1.8Volts. These parameters are called PVT (Process Voltage Temperature) and these parameters determine how my silicon is going to work faster or typical or slower. We also have studied how these PVT variations occur during fabrication and why is it important to consider PVT variations while designing our circuit. 
- This also tells that CMOS technology is used in this library. And the delay model is the lookup table model. Units of time, power, current, voltage, capacitance, resistance are also mentioned in the library. Operation conditions is as follows :

![image](https://user-images.githubusercontent.com/75198926/165993613-8731443c-a097-48ad-9484-89018ea908cf.png)

- In the library we can see that there are many types of cells. The following figures shows different types of cells present in the **sky130_fd_sc_hd__tt_025C_1v80.lib** library. 

![image](https://user-images.githubusercontent.com/75198926/165994720-0144fa10-d996-4931-b24c-609135ead043.png)


- We can see the features of a particular cell by using the following command :
```
:sp ../my_lib/verilog_model/sky130_fd_sc_hd__a2111o.behavioral.v
```
We can also see the leakage power, timing information, input capacitance, delay associated with each pins. 

*The following figure compares the power, area and delay between 3 types of and2 cells. Here we considered and2_0, and2_2 and and2_4 cells. As we can in the below figure that as we move from and2_0 cell to ans2_4 cell the transistor width increases, power increases, delay decreases and area increases.*

![image](https://user-images.githubusercontent.com/75198926/166003829-525aac0a-fc41-479e-8c53-f237d40f31e5.png)

 
## Hierarchical vs Flat synthesis

Here we use the following command to observe difference between hierarchical synthesis and flat synthesis. 
```
gvim multiple_modules.v
```

Then a files appears on the screen that contains three modules :
- sub_module1 : This is a 2-input **and** gate
- sub_module2 : This is a 2-input **or** gate
- multiple_modules : This is a three input gate that uses top two modules to perform the logic y = a&b + c

![image](https://user-images.githubusercontent.com/75198926/166090070-e1352ead-a9bf-4d23-a98b-203f9688428d.png)

**Hierarchical Synthesis**

Now we are going to synthesize the multiple_modules.v RTL design to see how the netlist will look like. So we again invoke the Yosys for synthesis. 
![image](https://user-images.githubusercontent.com/75198926/166090966-943b37dd-805f-43ee-9b34-cdfc551737a2.png)

Then we read the liberty file as follows:
![image](https://user-images.githubusercontent.com/75198926/166091045-3916c0f4-7b6a-4e72-aae3-7c35521403b2.png)

Now we will read the verilog RTL design file using the following command :
![image](https://user-images.githubusercontent.com/75198926/166091101-213a3b79-1e32-48a4-bbd2-587ad40cdfe5.png)

Now we will synthesize the RTL design to netlist using the following command :
```
synth -top multiple_modules
```
![image](https://user-images.githubusercontent.com/75198926/166091207-d0051edf-a048-4b99-a4c5-60a3014b7c38.png)
![image](https://user-images.githubusercontent.com/75198926/166091233-947e5d50-b517-4178-8202-03fe3a281b11.png)

We use the following command to extract the netlist using the standard cells present in the library mentioned in the command :
```
abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```

![image](https://user-images.githubusercontent.com/75198926/166091447-8192b6e2-8569-4f23-bc2d-5dab18de1a08.png)

We use ``` show ``` command to view the logic part of the synthesized netlist.
![image](https://user-images.githubusercontent.com/75198926/166091541-2fb08937-638d-48fc-ac4e-1375f0973d28.png)

![image](https://user-images.githubusercontent.com/75198926/166091569-2df0e75a-b1bb-4e64-b8b2-7ebf4dfc6ed9.png)

This is know as the hierarchical design where the hierarchies are preserved. 

![image](https://user-images.githubusercontent.com/75198926/166092525-8ad601f2-ed64-4669-a064-8e00cc2794fb.png)

![image](https://user-images.githubusercontent.com/75198926/166092590-78f40c1d-15a4-4215-b3e4-522c95eeb2b6.png)

![image](https://user-images.githubusercontent.com/75198926/166092638-f1281da7-b04a-41ec-91a0-9fbeec94a9ea.png)

*Here sub_module1 is realized using a and2 cell present in library but or gate is not realized using standard or cell that is present in the library rather combination of nand and inverters are used to realize or gate. This is because for realizing or gate directly in cmos technology we need to use nor gate followed by inverter, but here the problem is we have stacked pmos in nor gate implementation in cmos technology which is not desired as pmos has lower mobility and high logical effort compared to nand gate and to have low delay we need to increase the width of the transistors and area increases as well as power consumption also increases.* 

**Flat Synthesis**

![image](https://user-images.githubusercontent.com/75198926/166093265-bd64c62c-b24a-4203-bd3c-f93434919d1c.png)

![image](https://user-images.githubusercontent.com/75198926/166093358-81e3de70-22b6-452a-9316-b9dd45a33caa.png)

![image](https://user-images.githubusercontent.com/75198926/166093394-dae92b67-e444-45f5-b64c-bfcee7ceb0f8.png)

![image](https://user-images.githubusercontent.com/75198926/166093423-3ec1cabb-1975-4d54-8ed3-f06ccb62580a.png)

![image](https://user-images.githubusercontent.com/75198926/166093737-506f0a08-cacd-49c1-8674-5ca34747e5c9.png)

![image](https://user-images.githubusercontent.com/75198926/166094368-96268fad-dbb7-4157-8c04-26170df50a40.png)



**Submodule level synthesis**

![image](https://user-images.githubusercontent.com/75198926/166095863-7808b012-9d0e-4018-b4d3-f2558af53c16.png)

![image](https://user-images.githubusercontent.com/75198926/166095844-345540ac-c0db-44ae-b8f5-51bdcefb1a9d.png)

![image](https://user-images.githubusercontent.com/75198926/166095789-39bc23a3-683f-403a-93df-10a1a306518c.png)

![image](https://user-images.githubusercontent.com/75198926/166095832-a0b30255-6112-4259-bfe0-c27ce778a783.png)

![image](https://user-images.githubusercontent.com/75198926/166095924-5462a17e-9274-4b58-8c17-400adf445c3b.png)


## Various flop coding styles and optimization 

In this session we will look into how to code flop and how many different types of flops available and different styles of flop coding. 

**Why flops ?**
In general, a combinational circuit is a digital circuit whose output changes after the circuit's propagation delay for the change in inputs has passed. Due to this propagation delay glitches occur while connecting different devices of different propagation delays. More the number of combinational blocks in the circuits more will be the glitches. If we add more number of combinational blocks in series then our output will be more glitchy and it keeps on changing continuously so we need a new device to store the computed output value and display only under certain conditions. These new devices are called flops that are used to store data. To initialize these flops we have 2 control pins called reset and set pins. 

**Asyncres.v**

![image](https://user-images.githubusercontent.com/75198926/166105356-d3e1405f-38b2-4bd8-bda3-af619d4e3491.png)

![image](https://user-images.githubusercontent.com/75198926/166105369-b929526e-0696-462c-95cb-4fb9783a4150.png)


![image](https://user-images.githubusercontent.com/75198926/166105064-5f11e8b1-b004-4529-89a7-d1c60379eda6.png)

posedge reset
![image](https://user-images.githubusercontent.com/75198926/166105179-a184f4d6-2fb1-48a5-8a8f-2aa7391fd3c8.png)

negedge reset
![image](https://user-images.githubusercontent.com/75198926/166105206-8cf3088c-e3eb-4a97-a58d-82f9f72a4ae0.png)

**Async set.v**

![image](https://user-images.githubusercontent.com/75198926/166105705-d082ed71-5c55-4e75-ae2e-cfd778a859f6.png)

![image](https://user-images.githubusercontent.com/75198926/166105773-690a461a-2ac3-4dfa-be15-82de64ecf1ae.png)

![image](https://user-images.githubusercontent.com/75198926/166105901-c2f960d1-895c-4d9f-ad17-66b221928e92.png)

![image](https://user-images.githubusercontent.com/75198926/166105926-aafb532c-35c1-48c1-b468-7b35f5258c8c.png)

**Sync reset**


![image](https://user-images.githubusercontent.com/75198926/166106047-0109a518-94b8-4da9-8526-042c4378ec7b.png)

![image](https://user-images.githubusercontent.com/75198926/166106133-3509fecb-424e-403a-93d9-a0e3717c4168.png)

![image](https://user-images.githubusercontent.com/75198926/166106144-67f305c0-be14-424d-a3e4-2d6e1ed0862c.png)


**Synthesis**

![image](https://user-images.githubusercontent.com/75198926/166106828-d784540e-58ed-45d5-a4da-53d5d114d331.png)

![image](https://user-images.githubusercontent.com/75198926/166106990-d2fd6694-7fd0-43b7-ba92-f895b3b4d375.png)

![image](https://user-images.githubusercontent.com/75198926/166107012-b389ea9c-d0c7-4fd1-ac6e-27b2fbf1a8e4.png)

![image](https://user-images.githubusercontent.com/75198926/166107024-4707f2e8-f53d-402a-ab62-1eaf392babe8.png)

![image](https://user-images.githubusercontent.com/75198926/166107057-0e217067-7756-4ed7-9c64-9544243bc933.png)

![image](https://user-images.githubusercontent.com/75198926/166107091-a62cb336-f567-4e44-a311-8426b4ba1831.png)

![image](https://user-images.githubusercontent.com/75198926/166107399-67ae61a2-75b1-4165-b4b5-442c676683ce.png)

![image](https://user-images.githubusercontent.com/75198926/166107423-3f943d11-8dd6-4cac-8b81-8ebb11d315f4.png)

**Mult_8**

![image](https://user-images.githubusercontent.com/75198926/166107575-21bbf740-7dfb-47f8-8b1c-ffcd4cdeacd6.png)

![image](https://user-images.githubusercontent.com/75198926/166107697-7476084c-70f6-4da1-96d9-dad5095daaa9.png)

![image](https://user-images.githubusercontent.com/75198926/166107711-383b7097-3cdd-4226-ae97-0aea5c992154.png)

![image](https://user-images.githubusercontent.com/75198926/166107717-366a7b64-433a-4cd9-b56e-ba49b09e90eb.png)

![image](https://user-images.githubusercontent.com/75198926/166107769-db3f1832-d799-4a6e-85a0-8ae25bda2b6b.png)

# Day 3
## Combi logic optimization

**opt_check**
 
![image](https://user-images.githubusercontent.com/75198926/166110009-06cd2f44-e853-4b87-8e09-0d5fd676b155.png)
 
 ![image](https://user-images.githubusercontent.com/75198926/166110374-fba5c8f5-6414-4255-809e-6f98ea811b1e.png)

![image](https://user-images.githubusercontent.com/75198926/166110427-60b2efc9-0e71-4682-978c-f891d1f3682b.png)

![image](https://user-images.githubusercontent.com/75198926/166110441-e0578cc2-222a-4991-9f08-df49d20836b5.png)

![image](https://user-images.githubusercontent.com/75198926/166110463-4b1710a2-a878-41b2-b3c1-00b35aad23b2.png)

**opt_check2**

![image](https://user-images.githubusercontent.com/75198926/166110592-f41b5608-1fd7-4016-9444-407df6eceb03.png)

![image](https://user-images.githubusercontent.com/75198926/166110608-0aa38ff6-a43b-48b3-90a7-fffdc4248bf8.png)

![image](https://user-images.githubusercontent.com/75198926/166110636-4756c7cf-4a1d-453b-97b3-0b64c4d0cc7b.png)

![image](https://user-images.githubusercontent.com/75198926/166110657-9f94f6b4-3929-405c-8f7e-24b300da067b.png)





# Author
# Acknowledgements
#
#
#
#
