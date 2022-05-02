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
- [Day 4: GLS, blocking vs non-blocking and synthesis-simulation mismatch]()
  - [GLS, blocking vs non-blocking and synthesis-simulation mismatch]()
    - [GLS concepts and flow using iverilog]() 
    - [Synthesis-simulation mismatch]() 
    - [Blocking and non-blocking statements in verilog]()
    - [caveats with blocking statements]()
  - [Labs on GLS and synthesis-simulation mismatch]()
    - [Labs on GLS and synthesis-simulation mismatch part-1]()
    - [Labs on GLS and synthesis-simulation mismatch part-2]()
  - [Labs on synthesis-simulation mismatch for blocking statements]()
    - [Labs on synthesis-simulation mismatch for blocking statements part-1]()
    - [Labs on synthesis-simulation mismatch for blocking statements part-2]() 
- [Day 5: If, case, for loop and for generate]()
  - [If case constructs]()
    - [If case constructs part-1]() 
    - [If case constructs part-2]() 
    - [If case constructs part-3]()
  - [Labs on Incomplete If Case ]()
    - [Labs on Incomplete If Case part-1]()
    - [Labs on Incomplete If Case part-2]()
  - [Labs on Incomplete overlapping case]()
    - [Labs on Incomplete overlapping case part-1]()
    - [Labs on Incomplete overlapping case part-2]() 
    - [Labs on Incomplete overlapping case part-3]()'
    - [Labs on Incomplete overlapping case part-4]()
  - [For loop and For Generate]()
    - [For loop and For Generate part-1]() 
    - [For loop and For Generate part-2]() 
    - [For loop and For Generate part-3]()
  - [Labs on For loop and For Generate]()
    - [Labs on For loop and For Generate part-1]()
    - [Labs on For loop and For Generate part-2]() 
    - [Labs on For loop and For Generate part-3]()'
    - [Labs on For loop and For Generate part-4]()
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
yosys> abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib

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

- The first line tells the name of the library it's **sky130_fd_sc_hd__tt_025C_1v80.lib**. It is a 130nm technology library(sky130 idicates this) and *tt* indicates that this library is typical library and the *025C* indicates that temperature is 25 degrees celsius for this library, and *1v80* indicates that the rail voltage for this library is 1.8Volts. These parameters are called PVT (Process Voltage Temperature) and these parameters determine how my silicon is going to work faster or typical or slower. We also have studied how these PVT variations occur during fabrication and why is it important to consider PVT variations while designing our circuit. The following is the pictorial representation of the understanding of PVT paraeters.

![image](https://user-images.githubusercontent.com/75198926/166183397-c6c11008-92e1-48fd-851b-789dc9524d31.png)


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

![image](https://user-images.githubusercontent.com/75198926/166183689-fbb69040-97ea-4a71-9cd9-c2932eb5cabb.png)

 
## Hierarchical vs Flat synthesis


In this module we will see how a hierarchical synthesis differs from a flat synthesis and also how to flatten the hierarchical design to get flat synthesis. Here we use the following command to open a file which is used to observe difference between hierarchical synthesis and flat synthesis. 
```
gvim multiple_modules.v
```

![image](https://user-images.githubusercontent.com/75198926/166090070-e1352ead-a9bf-4d23-a98b-203f9688428d.png)

Then a files appears on the screen as shown above that contains three modules :
- sub_module1 : This is a 2-input **and** gate
- sub_module2 : This is a 2-input **or** gate
- multiple_modules : This is a three input gate that uses top two modules to perform the logic y = a&b + c

![image](https://user-images.githubusercontent.com/75198926/166184786-3609f62e-938f-481c-a44f-bb26f33fd223.png)


**Hierarchical Synthesis**

Now we are going to synthesize the multiple_modules.v RTL design to see how the netlist will look like. 

1. **So we again invoke the Yosys for synthesis**

![image](https://user-images.githubusercontent.com/75198926/166090966-943b37dd-805f-43ee-9b34-cdfc551737a2.png)

2. **Then we read the liberty file as follows :**

![image](https://user-images.githubusercontent.com/75198926/166091045-3916c0f4-7b6a-4e72-aae3-7c35521403b2.png)

3. **Now we will read the verilog RTL design file using the following command :**

![image](https://user-images.githubusercontent.com/75198926/166091101-213a3b79-1e32-48a4-bbd2-587ad40cdfe5.png)

4. **Now we will synthesize the RTL design to netlist using the following command :**
```
synth -top multiple_modules
```

![image](https://user-images.githubusercontent.com/75198926/166185887-7e85da3c-c94b-4995-90f0-aeef4d2197b2.png)

5. **We use the following command to extract the netlist using the standard cells present in the library mentioned in the command :**
```
abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```

![image](https://user-images.githubusercontent.com/75198926/166091447-8192b6e2-8569-4f23-bc2d-5dab18de1a08.png)

6. **We use ``` show ``` command to view the logic part of the synthesized netlist.**

![image](https://user-images.githubusercontent.com/75198926/166091541-2fb08937-638d-48fc-ac4e-1375f0973d28.png)

![image](https://user-images.githubusercontent.com/75198926/166186186-47b499d0-5a33-43ef-9d1c-f8f5957ebd4c.png)

Here we can see that the hierarchy is maintained. Because even after synthesis of multiple_module we got sub_module1 and sub_module2 in the logic part of the synthesized netlist inplace of completely synthesized sub modules. This is know as hierarchical synthesis where the sub modules information is preserved.

![image](https://user-images.githubusercontent.com/75198926/166092525-8ad601f2-ed64-4669-a064-8e00cc2794fb.png)

7. **Here we have written the hierarchical synthesis netlist of the multiple_module RTL design to a file. Here we used the command ```-noattr``` for easy intepretation of the netlist.** 

![image](https://user-images.githubusercontent.com/75198926/166092590-78f40c1d-15a4-4215-b3e4-522c95eeb2b6.png)

8. **Below is the command used to open the netlist file to read.**

![image](https://user-images.githubusercontent.com/75198926/166092638-f1281da7-b04a-41ec-91a0-9fbeec94a9ea.png)

*Here sub_module1 is realized using a **and2** cell present in library but **or** gate is not realized using standard **or** cell that is present in the library rather combination of nand and inverters are used to realize or gate. This is because for realizing or gate directly in cmos technology we need to use nor gate followed by inverter, but here the problem is we have stacked pmos in nor gate implementation in cmos technology which is not desired as pmos has lower mobility and high logical effort compared to nand gate and to have low delay we need to increase the width of the transistors and area increases as well as power consumption also increases.* 

**Flat Synthesis**

Now we are going to do flat synthesis of the multiple_modules.v RTL design to see how the netlist will look like. 

1. **For this we follow the same steps followed for hierarchical design but we nned to flatten the design so we use the comand ``` flatten ``` before writing the netlist to the file.**  

![image](https://user-images.githubusercontent.com/75198926/166093265-bd64c62c-b24a-4203-bd3c-f93434919d1c.png)

2. **Here we have written the flat synthesis netlist of the multiple_module RTL design to a file. Here we used the command ```-noattr``` for easy intepretation of the netlist.**

![image](https://user-images.githubusercontent.com/75198926/166093358-81e3de70-22b6-452a-9316-b9dd45a33caa.png)

3. **Below is the command used to open the netlist file to read.**

![image](https://user-images.githubusercontent.com/75198926/166093394-dae92b67-e444-45f5-b64c-bfcee7ceb0f8.png)

**The netlist file generated after flat synthesis of the multiple_module RTL design is as follows :**

![image](https://user-images.githubusercontent.com/75198926/166093423-3ec1cabb-1975-4d54-8ed3-f06ccb62580a.png)


**When we compare the netlists generated through hierarchical synthesis and flat synthesis we observe some critical differences.** 
- *We can see that in hierarchical synthesized netlist sub_module1 and sub_module2 are still present where as in netlist synthesized using flat synthesis the hierarcies are flattend out and there is single module i.e, multiple_module and all the gates are instantiated directly instead of sub_modules.*

![image](https://user-images.githubusercontent.com/75198926/166093737-506f0a08-cacd-49c1-8674-5ca34747e5c9.png)


**Below is the logic flow diagram of flat synthesized netlist. Clearly we can see that no hierarchy is preserved and hence there are no sub modules in the flow chart instead all the submodules are directly instantiated using standard cells.**  

![image](https://user-images.githubusercontent.com/75198926/166094368-96268fad-dbb7-4157-8c04-26170df50a40.png)



## Submodule level synthesis of sub_module1

**Why sub module level synthesis ?**
- When our RTL design contains multiple instantiation of the same sub module then we do submodule level synthesis for one time and replicate that result for remaining submodules. This saves a lot of time required for synthesizing main module. 
- Also when we have massive RTL design containing numerous submodules then synthesizing main modules consumes a lot of time. So we use divide and conquer rule for synthesizing our design and do submodule level synthesize that saves a lot of time for synthesis and testing the design. 

Now we are going to synthesize a sub module named sub_module1 present in multiple_module RTL design. Following are steps followed for synthesis.

1. **So we again invoke the Yosys for synthesis. Then we read the liberty file. Then read the verilog RTL design file using the following commands :**

![image](https://user-images.githubusercontent.com/75198926/166095863-7808b012-9d0e-4018-b4d3-f2558af53c16.png)

2. **Here we synthesize only the sub module named sub_module1 part inplace of suntheisizing whole RTL design. Now we will synthesize using the following command :**

![image](https://user-images.githubusercontent.com/75198926/166095844-345540ac-c0db-44ae-b8f5-51bdcefb1a9d.png)

![image](https://user-images.githubusercontent.com/75198926/166095789-39bc23a3-683f-403a-93df-10a1a306518c.png)

3. **Then we use the following command to extract the netlist using the standard cells present in the library :

```
abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```

![image](https://user-images.githubusercontent.com/75198926/166095832-a0b30255-6112-4259-bfe0-c27ce778a783.png)

4. **Then we use ```show``` command to see the logical part of the netlist. Here as we synthesized sub_module1 which is effectively an AND gate. After synthesis also we got standard and2_0 gate in place of sub_module1.**

![image](https://user-images.githubusercontent.com/75198926/166095924-5462a17e-9274-4b58-8c17-400adf445c3b.png)


## Various flop coding styles and optimization 

### Flop synthesis simulations

In this session we will look into how to code flop and know many different types of flops available and different styles of flop codings. 

**Why flops ?**

In general, a combinational circuit is a digital circuit whose output changes after the circuit's propagation delay for the change in inputs has passed. Due to this propagation delay glitches occur while connecting different devices of different propagation delays. More the number of combinational blocks in the circuits more will be the glitches. If we add more number of combinational blocks in series then our output will be more glitchy and it keeps on changing continuously so we need a new device to store the computed output value and display only under certain conditions. These new devices are called flops that are used to store data. To initialize these flops we have 2 control pins called reset and set pins on a flop to initialize the flop, other wise a garbage value is sent out to the next combinational circuit. These control pins can be synchronous or asynchronous.

### D-Flipflop with Asynchronous reset

Here we are using reset control signal to initialize the flop. Here the output q goes low whenever reset is high (q = 0 when reset = 1) and as it is asynchronous reset resetting will not wait for the clock's posedge, i.e., irrespective of clock, the output is changed to low when reset = 1.

The below figure shows the **Asyncres.v** RTL design file along with the testbench. 

![image](https://user-images.githubusercontent.com/75198926/166105356-d3e1405f-38b2-4bd8-bda3-af619d4e3491.png)

Below is the waveform generated by gtkwave for asyncres.v simulation.

![image](https://user-images.githubusercontent.com/75198926/166105064-5f11e8b1-b004-4529-89a7-d1c60379eda6.png)

Here we need to note two major instances from the waveform. 

- **posedge of reset :** Here the reset goes from 0 to 1 i.e., reset is applied so as soon as the reset goes to 1 our output q went to 0 immediately without waiting for next posedge of the clock. 

![image](https://user-images.githubusercontent.com/75198926/166105179-a184f4d6-2fb1-48a5-8a8f-2aa7391fd3c8.png)

- **negedge of reset :** Here the reset goes from 1 to 0 i.e., reset is switched off so as soon as the reset goes to 0 our output q remained at 0 waiting for next posedge of the clock and when next posedge occured then d followed q untill next posedge.

![image](https://user-images.githubusercontent.com/75198926/166105206-8cf3088c-e3eb-4a97-a58d-82f9f72a4ae0.png)



### D-Flipflop with Asynchronous set

Here we are using set control signal to initialize the flop. Here the output q goes high whenever set is high (q = 1 when set = 1) and as it is asynchronous set it will not wait for the clock's posedge, i.e., irrespective of clock, the output is changed to high when set = 1.

The below figure shows the **Asyncset.v** RTL design file along with the testbench. 

![image](https://user-images.githubusercontent.com/75198926/166105926-aafb532c-35c1-48c1-b468-7b35f5258c8c.png)

Here we need to note two major instances from the waveform. 

- **posedge of set :** Here the set goes from 0 to 1 i.e., set is applied so as soon as the set goes to 1 our output q went to 1 immediately without waiting for next posedge of the clock. 

![image](https://user-images.githubusercontent.com/75198926/166105773-690a461a-2ac3-4dfa-be15-82de64ecf1ae.png)

- **negedge of set :** Here the set goes from 1 to 0 i.e., set is switched off so as soon as the set goes to 0 our output q remained at 1 waiting for next posedge of the clock and when next posedge occured then d followed q untill next posedge.

![image](https://user-images.githubusercontent.com/75198926/166105705-d082ed71-5c55-4e75-ae2e-cfd778a859f6.png)



### D-Flipflop with synchronous reset

Here we are using reset control signal to initialize the flop. Here the output q goes low whenever reset is high (q = 0 when reset = 1) and as it is synchronous set it will wait for the clock's posedge, i.e., when posedge of clock occurs then only the output is changed to low when reset = 1.

The below figure shows the **syncres.v** RTL design file along with the testbench. 

![image](https://user-images.githubusercontent.com/75198926/166106133-3509fecb-424e-403a-93d9-a0e3717c4168.png)

Here we need to note two major instances from the waveform. 

- **posedge of reset :** Here the reset goes from 0 to 1 i.e., reset is applied only at posedge of clock even when reset goes to 1 our output q went to 0 after waiting for next posedge of the clock. 

- **negedge of reset :** Here the reset goes from 1 to 0 i.e., reset is switched off as reset goes to 0 our output q remained at previous state(0) waiting for next posedge of the clock and when next posedge occured then d followed q untill next posedge.

![image](https://user-images.githubusercontent.com/75198926/166106047-0109a518-94b8-4da9-8526-042c4378ec7b.png)


## Interesting optimizations

This lab session deals with some automatic and interesting optimisations of the circuits based on logic. 

**Multiply with 2**

In the example below, we can see that multiplication of a number(a) by 2 does not require any additional hardware; all that is required is connecting the bits from a to y and grounding the LSB bit of y, as demonstrated by Yosys.

![image](https://user-images.githubusercontent.com/75198926/166197919-a3931abe-d536-4d26-a4b2-8a9380f7470f.png)

The following is the RTL design code for multiplying a number(a) with 2.

![image](https://user-images.githubusercontent.com/75198926/166106828-d784540e-58ed-45d5-a4da-53d5d114d331.png)

The following is the statistics after performing ```synth -top mul2``` :

![image](https://user-images.githubusercontent.com/75198926/166107423-3f943d11-8dd6-4cac-8b81-8ebb11d315f4.png)

Here while extracting netlist it says that there is no need for extraction as there are no gates in the design.

![image](https://user-images.githubusercontent.com/75198926/166107024-4707f2e8-f53d-402a-ab62-1eaf392babe8.png)

The logical part of the generated netlist is as follows: *Clearly we can see that multiplication of a number(a) by 2 does not require any additional hardware; all that is required is connecting the bits from a to y and grounding the LSB bit of y*

![image](https://user-images.githubusercontent.com/75198926/166107057-0e217067-7756-4ed7-9c64-9544243bc933.png)

The generated netlist file is as follows : Here simply y is assigned as y = {a, 1'h0}

![image](https://user-images.githubusercontent.com/75198926/166107399-67ae61a2-75b1-4165-b4b5-442c676683ce.png)



**Multiply with 9**

In the example below, we can see that multiplication of a number(a) by 9 does not require any additional hardware; all that is required is connecting the bits from a to y twice i.e., y = {a, a} as demonstrated by Yosys.

![image](https://user-images.githubusercontent.com/75198926/166199543-d13a3f81-8a3e-42c4-8a17-fad39e07020a.png)


The following is the RTL design code for multiplying a number(a) with 9.

![image](https://user-images.githubusercontent.com/75198926/166106828-d784540e-58ed-45d5-a4da-53d5d114d331.png)


The following is the statistics after performing ```synth -top mult8``` :

![image](https://user-images.githubusercontent.com/75198926/166107575-21bbf740-7dfb-47f8-8b1c-ffcd4cdeacd6.png)


The generated netlist file is as follows : Here simply y is assigned as y = {a, a}

![image](https://user-images.githubusercontent.com/75198926/166107697-7476084c-70f6-4da1-96d9-dad5095daaa9.png)


The logical part of the generated netlist is as follows: *Clearly we can see that multiplication of a number(a) by 9 does not require any additional hardware; all that is required is connecting the bits from a to y twice.*

![image](https://user-images.githubusercontent.com/75198926/166107769-db3f1832-d799-4a6e-85a0-8ae25bda2b6b.png)




# Day 3: Combinational and sequential optimisations

## Combinational logic optimisations

There are three types of combinational logic optimisations. They are :
- squeezing the logic to get the most optimized design 
  - Area and power savings
- Constant propagation
  - direct optimisation
- Boolean logic optimisation
  - K-map 
  - Quine McKluskey


**Constant Propagation : Example**

Let us consider the following combinational circuit consisting of one AND gate and one NOR gate. Let us use constant propagation optimisation to optimise the design and bring down to a circuit consisting of one inverter. 

![image](https://user-images.githubusercontent.com/75198926/166215271-365d45ef-e971-44e6-952b-9dead8cce782.png)

- Transistor - level implementation :

We can clearly see that number of transistors required after constant propagation optimisation is less than original design. This is achieved by making A as contstant and propagating the same to output. 

![image](https://user-images.githubusercontent.com/75198926/166217447-e79c05ef-5629-4743-be7e-1a87fc5344c7.png)


**Boolean Logic Optimisation : Example**

Let us consider the following statement y = a?(b?c:(c?a:0)):(!c). Let us use boolean logic optimisation to optimise the design and bring down to a circuit consisting of one XNOR gate. 

![image](https://user-images.githubusercontent.com/75198926/166220895-bcca5259-1579-400d-b718-7058c0f7ef04.png)


## Sequential logic optimisations

There are two types of sequential logic optimisations. They are :
- Basic 
  - Sequential constant propagation
- Advanced (*Not discussed*)
  - State optimisation
  - Retiming 
  - Sequential logic cloning

**Sequential Constant Propagation :**

**Example : 1**
Let us consider the following sequential+combinational mixed circuit consisting of one Flop with asychronous rest and one NAND gate. Let us use constant propagation optimisation to optimise the design and bring down to a circuit consisting of no gates. 

![image](https://user-images.githubusercontent.com/75198926/166228332-58d4a81d-228a-464c-a0a9-91fe224a7da8.png)

**Here the output flop is always 0, so the output evaluates to 1 always. Now the complete circuit is no more needed.** 


**Example : 2**
Let us consider the following sequential+combinational mixed circuit consisting of one Flop with asychronous set and one NAND gate. Let us try to use constant propagation optimisation to optimise the design and see if the design can be optimised or not. 

![image](https://user-images.githubusercontent.com/75198926/166228947-29e29682-b44a-4da6-9409-720928049ff0.png)

**Here the output q changes based on set and clock. Therefore, the circuit cannot be optimised.**

## Advanced sequential optimisations :

- **State Optimisation** : Optimisation of unused states is known as state optimization. We can design the most optimised state machine using this strategy.
- **Cloning** : When executing physical aware synthesis, this optimisation is done. Consider the case of flop A, which is linked to flops B and C via a combination logic. There is a routing path delay if B and C are situated far from A in the flowplan. To avoid this, we connect A to two intermediate flops, then send the output from these flops to B and C, reducing the latency. Because we are creating two new flops with the identical functionality as A, this technique is known as cloning.
- **Retiming** : Retiming is a powerful sequential optimization approach for moving registers across combinational logic or optimising the amount of registers to enhance performance via a power-delay trade-off while maintaining the circuit's input-output behaviour.


## Labs on Combinational Logic Optimization

Through this lab session we are going to see some examples on combinational logic optimisation. In yosys we require a unique command to perform combinational optimisation, the command is as follows :

```
yosys> opt_clean -purge
```

**Example : 1**
**opt_check**

The following figure depicts the RTL design of our first combinational circuit : 
 
![image](https://user-images.githubusercontent.com/75198926/166110009-06cd2f44-e853-4b87-8e09-0d5fd676b155.png)


The following is the statistics after performing synth -top opt_check :

![image](https://user-images.githubusercontent.com/75198926/166110441-e0578cc2-222a-4991-9f08-df49d20836b5.png)


The logical part of the synthesized netlist is as follows :
 
![image](https://user-images.githubusercontent.com/75198926/166110374-fba5c8f5-6414-4255-809e-6f98ea811b1e.png)



**Explanation :**

![image](https://user-images.githubusercontent.com/75198926/166231750-a3b1fead-6639-4c4c-8ec7-488a48b229f5.png)



**Example : 2**
**opt_check2**

The following figure depicts the RTL design of our first combinational circuit : 
 
![image](https://user-images.githubusercontent.com/75198926/166110009-06cd2f44-e853-4b87-8e09-0d5fd676b155.png)


The following is the statistics after performing synth -top opt_check2 :

![image](https://user-images.githubusercontent.com/75198926/166110636-4756c7cf-4a1d-453b-97b3-0b64c4d0cc7b.png)


The logical part of the synthesized netlist is as follows :

![image](https://user-images.githubusercontent.com/75198926/166110592-f41b5608-1fd7-4016-9444-407df6eceb03.png)


**Explanation :**

![image](https://user-images.githubusercontent.com/75198926/166232337-6730fa24-441a-4911-b547-c9804d0c76d1.png)


**Example : 3**
**opt_check3**

The following figure depicts the RTL design of our first combinational circuit : 

![image](https://user-images.githubusercontent.com/75198926/166233123-146797af-b8c1-4ffb-aa45-752c21242602.png)


The following is the statistics after performing synth -top opt_check3 :

![image](https://user-images.githubusercontent.com/75198926/166110902-52fa218f-d6dd-48d7-9395-2912a56020d4.png)


The logical part of the synthesized netlist is as follows :

![image](https://user-images.githubusercontent.com/75198926/166110849-9ddaf188-6643-4552-aa50-444ef6954ccf.png)



**Explanation :**

![image](https://user-images.githubusercontent.com/75198926/166237055-ad873875-9263-4075-82a8-903017314cad.png)



**Example : 4**
**opt_check4**

The following figure depicts the RTL design of our first combinational circuit : 

![image](https://user-images.githubusercontent.com/75198926/166112918-66ddd0ac-9ac0-4645-a38f-3152a031d2a8.png)


The logical part of the synthesized netlist is as follows :

![image](https://user-images.githubusercontent.com/75198926/166112247-f089909f-af9a-4aa0-8158-e02a20b44a67.png)


**Explanation :**

![image](https://user-images.githubusercontent.com/75198926/166237249-b689707d-7540-4908-a9f5-ef371f92de7c.png)





**Example : 5**
**multiple_module_opt**

The following figure depicts the RTL design of our first combinational circuit : 

![image](https://user-images.githubusercontent.com/75198926/166113125-aeabe018-5d48-43aa-93aa-d778bf3caf36.png)


The logical part of the synthesized netlist is as follows :

![image](https://user-images.githubusercontent.com/75198926/166237637-4d6599f7-e592-4334-aede-e7088608d2d1.png)



**Explanation :**

![image](https://user-images.githubusercontent.com/75198926/166239471-f46315e1-3c9e-4039-aebf-7486a91ff7b6.png)



**Example : 6**
**multiple_module_opt2**

The following figure depicts the RTL design of our first combinational circuit : 

![image](https://user-images.githubusercontent.com/75198926/166113169-b1ad1563-8389-4d2d-8a1b-6dd00367b7ed.png)


The logical part of the synthesized netlist is as follows :

![image](https://user-images.githubusercontent.com/75198926/166237721-8780b532-1706-422f-a963-22cb0dddec71.png)



**Explanation :**

![image](https://user-images.githubusercontent.com/75198926/166240252-fa673ecf-2864-4a69-a436-8d594154d2d8.png)




## Labs on Sequential Logic Optimization

Through this lab session we are going to see some examples on sequential logic optimisation. In yosys we require a unique command to perform sequential optimisation, the command is as follows :

```
yosys> dfflibmap -liberty ../my_lib/lib/sky130_fd_sc_hd_tt__025C_1v80.lib
```

**Example : 1**

**dff_const1**

The following figure depicts the RTL design of our first sequential circuit :

![image](https://user-images.githubusercontent.com/75198926/166241299-abf6ebf5-7832-4a4a-940b-6fc148b2584f.png)


The waveform generated by gtkwave of the simulated design is as follows :

![image](https://user-images.githubusercontent.com/75198926/166117056-bf1191e1-baf5-4c19-98ab-4b081656a8c6.png)


The logical part of the synthesized netlist is as follows :

![image](https://user-images.githubusercontent.com/75198926/166117435-c0d3b0c4-1008-453e-b136-dc5873d247da.png)


**Explanation :**

- From the waveform generated by gtkwave we can see that the output is not constant but depends on clk and reset. So a flop is needed to realize this design. From the flow chart diagram, we can see that a Dflop was used in this example.


**Example : 2**

**dff_const2**

The following figure depicts the RTL design of our second sequential circuit :

![image](https://user-images.githubusercontent.com/75198926/166241757-5b21cff1-ce76-4583-bfdb-e2bd6f11080d.png)


The waveform generated by gtkwave of the simulated design is as follows :

![image](https://user-images.githubusercontent.com/75198926/166117152-c3a68da1-4fa6-455d-90f8-9640019521a4.png)


The logical part of the synthesized netlist is as follows :

![image](https://user-images.githubusercontent.com/75198926/166117764-dc34e927-5b8f-4f00-88d4-a404734d6f15.png)


**Explanation :**

- From the waveform generated by gtkwave we can see that the output is constant(1'b1). So a flop is not needed to realize this design. From the flow chart diagram, we can see no flop was used in this example.


**Example : 3**

**dff_const3**

The following figure depicts the RTL design of our third sequential circuit :

![image](https://user-images.githubusercontent.com/75198926/166118034-4f399de4-97c9-4684-a782-917327e1ef2a.png)


The waveform generated by gtkwave of the simulated design is as follows :

![image](https://user-images.githubusercontent.com/75198926/166118174-17047699-28c7-4e8b-a9c9-5474093a7e9b.png)


The logical part of the synthesized netlist is as follows :


![image](https://user-images.githubusercontent.com/75198926/166118274-52967360-a3bf-4ad2-8bc3-2e933882d9de.png)


**Explanation :**

- From the waveform generated by gtkwave we can see that the both outputs q and q1 are not constant. So two flops are needed to realize this design. From the flow chart diagram, we can see that two flops were used in this example.


**Example : 4**

**dff_const4**

The following figure depicts the RTL design of our forth sequential circuit :

![image](https://user-images.githubusercontent.com/75198926/166119232-5c153a0f-a84f-49c7-af7a-9f84b901ca36.png)


The waveform generated by gtkwave of the simulated design is as follows :

![image](https://user-images.githubusercontent.com/75198926/166244216-249ed2ff-6075-4b71-8aa1-30fe94f92e90.png)


The logical part of the synthesized netlist is as follows :

![image](https://user-images.githubusercontent.com/75198926/166119357-db6b052d-3779-4739-a56a-802fcc4b2f55.png)


**Explanation :**

- From the waveform generated by gtkwave we can see that the both outputs q and q1 are constant. So no flops are needed to realize this design. From the flow chart diagram, we can see that no flops were used in this example.


**Example : 5**

**dff_const5**

The following figure depicts the RTL design of our fifth sequential circuit :

![image](https://user-images.githubusercontent.com/75198926/166119306-8e6740e5-4f9d-48cf-9500-a56e5cd16722.png)


The waveform generated by gtkwave of the simulated design is as follows :

![image](https://user-images.githubusercontent.com/75198926/166244700-8041fa23-81e3-47b1-8ffb-221171cbc629.png)


The logical part of the synthesized netlist is as follows :

![image](https://user-images.githubusercontent.com/75198926/166119407-ffdd2ec3-9e35-4b58-b233-e82ab49b36ee.png)


**Explanation :**

- From the waveform generated by gtkwave we can see that the both outputs q and q1 are not constant. So two flops are needed to realize this design. From the flow chart diagram, we can see that two flops were used in this example.


## Sequential Optimisation of unused outputs

**Example : 1**

The following figure depicts the RTL design of our first sequential circuit to be synthesized :

![image](https://user-images.githubusercontent.com/75198926/166119830-a4521a7d-dd05-4058-9120-1ec3792c5e8a.png)


The logical part of the synthesized netlist is as follows :

![image](https://user-images.githubusercontent.com/75198926/166119765-b7d82396-1f20-44e6-ad98-b461f0e687c1.png)





 

# Day 4: GLS, blocking vs non-blocking and synthesis-simulation mismatch

## GLS concepts and flow using iverilog

**What is GLS ?**

- GLS means Gate Level Simulation. Here for this simulation netlist is used as Design Under Test (DUT). We know that netlist is logically same as RTL code so the same testbench can be used for both simulations i.e., RTL simulation and GLS simulation.


**Why GLS ?**

- GLS is used to verify the correctness of the RTL design after synthesis. Because the synthesiser ignores the sensitivity list and only looks at the statements in the procedural block, it infers that the circuit is correct. Simulating the netlist code, on the other hand, will result in a synthesis simulation mismatch.

**Flow using iverilog**

![image](https://user-images.githubusercontent.com/75198926/166248188-9cd8f894-b5e0-4523-85cc-e2a184928cac.png)



## Synthesis-simulation mismatch

There are three main causes for synthesis-simulation mismatches. They are :

- Missing sensitivity list : To avoid synthesis-simulation mismatch due to missing sensitivity list we generally keep always @(\*) condition while writing always block.
- Blocking vs non-blocking assignments : 
  - Inside "always" block 
    - Blocking : Executes statements in the order written. 
    - Non-blocking : Executes all the RHS when always block is entered and assigns to LHS.
- Non standard verilog coding 


## Labs on GLS and synthesis-simulation mismatch

In this lab session we will see different types of examples that results in synthesis-simulation mismatch and understand the ways to prevent those mismatches.

**Example : 1**

**ternary_operator_mux**

The following figure depicts the RTL design of our first combinational circuit which causes synthesis-simulation mismatch :

![image](https://user-images.githubusercontent.com/75198926/166255530-04bc0c96-8edd-4264-90e2-184442427135.png)


The waveform generated by gtkwave of the simulated design using RTL simulation is as follows :

![image](https://user-images.githubusercontent.com/75198926/166135293-13bedfa1-20b6-4abd-9648-41ae87734b91.png)


The logical part of the synthesized netlist is as follows :

![image](https://user-images.githubusercontent.com/75198926/166135446-6ff90887-4127-49ad-bc22-f3ba58aae614.png)


The waveform generated by gtkwave of the simulated design using GLS simulation is as follows :

![image](https://user-images.githubusercontent.com/75198926/166136073-178b0adf-64f9-4ce7-9378-aaff81491e71.png)


**Example : 2**

**bad_mux**

The following figure depicts the RTL design of our second combinational circuit which causes synthesis-simulation mismatch :

![image](https://user-images.githubusercontent.com/75198926/166256309-c847510b-ac63-465c-afcc-65866fa6fec7.png)


The waveform generated by gtkwave of the simulated design using RTL simulation is as follows :

![image](https://user-images.githubusercontent.com/75198926/166137050-48b11dd9-ffac-4dfd-8acc-c975423840c8.png)


The logical part of the synthesized netlist is as follows :

![image](https://user-images.githubusercontent.com/75198926/166140367-a67ce795-ab0c-4950-beb6-1507740a5cbd.png)


The waveform generated by gtkwave of the simulated design using GLS simulation is as follows :

![image](https://user-images.githubusercontent.com/75198926/166140471-532556e2-93c1-4bec-8f5d-e1360ec9ceac.png)


## Lab on Synthesis-simulation mismatch due to blocking statement

**Example : 1**

**blocking_caveat.v**

- **The following figure depicts the RTL design of our first sequential circuit which causes synthesis-simulation mismatch :** 

![image](https://user-images.githubusercontent.com/75198926/166140715-025fe5f9-8d7f-476a-a132-1d58d5a1c8d5.png)


- **The waveform generated by gtkwave of the simulated design using RTL simulation is as follows :**

![image](https://user-images.githubusercontent.com/75198926/166140979-059ead63-823f-4363-8d69-c52b5e49159f.png)\


- **The logical part of the synthesized netlist is as follows :**

![image](https://user-images.githubusercontent.com/75198926/166141109-1e2c887f-513b-422d-ad31-51d73ffd3f1d.png)


- **The waveform generated by gtkwave of the simulated design using GLS simulation is as follows :**

![image](https://user-images.githubusercontent.com/75198926/166141285-600fc9f4-4b7f-4115-b257-f3f133b58526.png)



# Day 5

**Lab on IF**

![image](https://user-images.githubusercontent.com/75198926/166143459-1631526b-96f5-4838-afdd-44f6d90c375a.png)

![image](https://user-images.githubusercontent.com/75198926/166143613-c71f909f-17bb-415a-946a-57dfe14198df.png)

![image](https://user-images.githubusercontent.com/75198926/166143725-f01e2eb1-5fab-4d6b-abdf-91592e5ccc1a.png)


**IF2**

![image](https://user-images.githubusercontent.com/75198926/166143829-bf8a2ab3-38d5-4404-90a9-3b3cc557ba3c.png)

![image](https://user-images.githubusercontent.com/75198926/166144458-7b1a1864-e0e5-45d9-b56d-ca10a8fbbd6a.png)

![image](https://user-images.githubusercontent.com/75198926/166144553-64121868-1f62-414f-9dc8-ed980fe35094.png)


**incomp_case**

![image](https://user-images.githubusercontent.com/75198926/166145023-507dc592-e4a7-4af0-9d2f-9d2292ced8a1.png)

![image](https://user-images.githubusercontent.com/75198926/166145065-70771ada-8508-4b86-9396-e62c9615258a.png)

![image](https://user-images.githubusercontent.com/75198926/166145118-908fde31-f514-4f44-b82e-f01a910cb1a2.png)

![image](https://user-images.githubusercontent.com/75198926/166146468-ec98ded8-b848-4276-84f9-6410a5391d76.png)

![image](https://user-images.githubusercontent.com/75198926/166147249-7f99c7cf-f25d-4fbc-85c5-7fe539efb1b2.png)


**Comp_case**

![image](https://user-images.githubusercontent.com/75198926/166147656-05eae314-dd7d-4a97-aff7-294750951b57.png)

![image](https://user-images.githubusercontent.com/75198926/166147833-2934be10-5670-4d4c-bb54-c7bff3aa8356.png)

![image](https://user-images.githubusercontent.com/75198926/166147939-35e214c7-c58c-4cac-8abc-e0e586c1f729.png)


**Partial_case**

![image](https://user-images.githubusercontent.com/75198926/166148133-c4c6876e-bb9f-464c-bfcb-688b3fc4d019.png)

![image](https://user-images.githubusercontent.com/75198926/166148418-2307f7dd-ebf3-4b9d-9d3e-5158de8a623c.png)


**Bad case**

![image](https://user-images.githubusercontent.com/75198926/166148681-96ef43e8-3f41-43e2-bc73-50856e50f3ef.png)

![image](https://user-images.githubusercontent.com/75198926/166149126-d11c3674-d239-41ef-87f7-be648685dc6c.png)

![image](https://user-images.githubusercontent.com/75198926/166149228-90871695-a449-4899-b331-ec03a8b4e6d0.png)

![image](https://user-images.githubusercontent.com/75198926/166149239-35eee8e8-5345-491f-811a-90b62b07b0cf.png)

Latching to value 1.

![image](https://user-images.githubusercontent.com/75198926/166149705-b825ccd8-9442-4a6c-a66f-23d3e802530d.png)


Synthesis

![image](https://user-images.githubusercontent.com/75198926/166150132-034528bd-67cf-4b33-aa08-6071c18779ad.png)


# For

**Lab01**

![image](https://user-images.githubusercontent.com/75198926/166157840-d27dee53-257e-4702-b06e-3d11c58edd8d.png)

![image](https://user-images.githubusercontent.com/75198926/166158239-c3f4838c-29fe-48b6-9df6-b4422e741126.png)

![image](https://user-images.githubusercontent.com/75198926/166158504-647e968d-ddf3-4e00-b7fe-28cb36d68481.png)

![image](https://user-images.githubusercontent.com/75198926/166158714-d4457453-d031-4458-a23f-0786d6bf7559.png)


**Lab 02**

![image](https://user-images.githubusercontent.com/75198926/166158801-8ae36b97-901c-457e-86bb-0e8afebb3867.png)

![image](https://user-images.githubusercontent.com/75198926/166158862-e99ee595-ab31-4d15-b911-17b8b893a482.png)

![image](https://user-images.githubusercontent.com/75198926/166159141-0cb6d5d8-e757-407d-a395-09f61f362475.png)

![image](https://user-images.githubusercontent.com/75198926/166159164-acc4cfd2-c552-44c1-8deb-9249461b303a.png)

![image](https://user-images.githubusercontent.com/75198926/166159260-44e97a60-df5f-4765-b170-17d461985e2c.png)

![image](https://user-images.githubusercontent.com/75198926/166159356-09e87322-c2c6-44ea-8fbd-5ff4e671c2b1.png)

![image](https://user-images.githubusercontent.com/75198926/166159731-3c0093d0-d98c-4590-a750-3bad46eb0dbe.png)

![image](https://user-images.githubusercontent.com/75198926/166159908-b059b45c-c37f-4862-b9ba-3ccb8d8759c6.png)



**Lab03**

![image](https://user-images.githubusercontent.com/75198926/166160898-47876349-1850-4a55-b749-bb486dacd3fd.png)

![image](https://user-images.githubusercontent.com/75198926/166160973-257fa740-ebba-4d90-b2c7-8d2d06bd6260.png)

![image](https://user-images.githubusercontent.com/75198926/166161406-87e5ba05-d2c6-4bda-a7d3-48abb9595bbf.png)

![image](https://user-images.githubusercontent.com/75198926/166161423-47173e0b-03cb-4004-9ff4-19690ec70402.png)

![image](https://user-images.githubusercontent.com/75198926/166161694-b8eadb9e-0c24-4929-8c96-bc78a60d9d87.png)

![image](https://user-images.githubusercontent.com/75198926/166161714-8c9a22e3-ffa1-4524-bf0d-feb28c4529c7.png)

![image](https://user-images.githubusercontent.com/75198926/166161879-09e93306-0d5c-443b-a55a-f05e4f79a2d2.png)








# Author
# Acknowledgements
#
#
#
#
