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


# Labs using iverilog and gtkwave
## Introduction to lab

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

## Introduction to iverilog gtkwave part-1

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



# Author
# Acknowledgements
#
#
#
#
