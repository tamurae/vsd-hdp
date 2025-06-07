<details>
<summary>Verilog RTL design and synthesis</summary>
  
  #### - Lab2: iverilog and GTKWave
  Functional verification (Boolean simulation: i.e., zero delays)
  ```
  $ git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
  $ cd sky130RTLDesignAndSynthesisWorkshop/verilog_files
  $ iverilog good_mux.v tb_good_mux.v
  $ ./a.out
  $ gtkwave tb_good_mux.vcd
  ```
  <img alt="gtkwave_good_mux" src="./images/GTKWave_good_mux.png">

  #### - Lab3: Yosys and abc
  - Logical synthesis
  ```
  $ yosys
  > read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80_nomux.lib
  > read_verilog good_mux.v
  > synth -top good_mux
  ```
  <img alt="Yosys_good_mux" src="./images/Yosys_good_mux.png">

  - Mapping to a given technology (Sky130 standard cells in this case) using [ABC](https://people.eecs.berkeley.edu/~alanmi/abc/)
  ```
  > abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80_nomux.lib
  > show
  ```
  <img alt="Yosys_good_mux_nomux_show" src="./images/Yosys_good_mux_nomux_show.png">

  ```
  > write_verilog -noattr good_mux_netlist.v
  > exit
  ```
  - Resulting schematic using Sky130 standard cells
  <img alt="Yosys_good_mux_sch" src="./images/Yosys_good_mux_sch.png">
</details>

  ### * Timing libs, hierarchical vs flat synthesis, and efficient flop coding styles
  #### - Lab5: Hierarchical vs Flat Synthesis
  ```
  $ cd sky130RTLDesignAndSynthesisWorkshop/verilog_files
  $ yosys
  > read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  > read_verilog multiple_modules.v
  > synth -top multiple_modules
  > abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  > show multiple_modules
  ```
  - Resulting schematic
  <img alt="Yosys_multiple_modules" src="./images/Yosys_multiple_modules.png">

  ```
  > write_verilog -noattr multiple_modules_hier.v
  ```
  - Resulting Verilog netlist
  <img alt="mmodules" src="./images/mmodules.png">

  ```
  > show sub_module1
  ```
  - Resulting schematic using Sky130 standard cells
  <img alt="Yosys_sub_module1" src="./images/Yosys_sub_module1.png">

  ```
  > show sub_module2
  ```
  - Resulting schematic using Sky130 standard cells
  <img alt="Yosys_sub_module2" src="./images/Yosys_sub_module2.png">

  #### - Various Flip-Flop Coding Styles

  ##### - DFF functional simulation
  ```
$ iverilog dff_asyncres.v tb_dff_asyncres.v
$ ./a.out
$ gtkwave tb_dff_asyncres.vcd

  ```

  ### * Combinational and sequential optimizations

  ### * Gate-Level Simulation, blocking vs non-blocking, and Synthesis-Simulation mismatches
