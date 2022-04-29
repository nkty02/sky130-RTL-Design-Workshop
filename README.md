# RTL design using Verilog with SKY130 Technology

![image](https://user-images.githubusercontent.com/75198926/165884648-3ef050ce-e181-46d6-a8af-00eaa7f70260.png)

# Table of contents
- [Brief description of workshop]()
- [Day 1: Introduction to verilog RTL design and synthesis]()
  - [Introduction to open-source simulator iverilog]()
    - [Introduction to iverilog design testbench]() 
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

# Author
# Acknowledgements
#
#
#
#
