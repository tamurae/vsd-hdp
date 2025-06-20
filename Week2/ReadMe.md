## Synthesis and Functional Simulation

<details>
<summary>Verilog RTL design and synthesis</summary>
  
  #### - Lab2: iverilog and GTKWave
  Functional verification (Boolean simulation: i.e., zero delays)
  ```bash
  $ git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
  $ cd sky130RTLDesignAndSynthesisWorkshop/verilog_files
  $ iverilog good_mux.v tb_good_mux.v
  $ ./a.out
  $ gtkwave tb_good_mux.vcd
  ```
  <img alt="gtkwave_good_mux" src="./images/GTKWave_good_mux.png">

  #### - Lab3: Yosys and abc
  - Logical synthesis
    
> [*** IMPORTANT *****]

> Note the library name...
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

<details>
<summary>Timing libs, hierarchical vs flat synthesis, and efficient flop coding styles</summary>

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

  ##### - Asynchronous Reset DFF - functional simulation
  ```bash
$ iverilog dff_asyncres.v tb_dff_asyncres.v
$ ./a.out
$ gtkwave tb_dff_asyncres.vcd
  ```
<img alt="GTKWave_dff_asyncres" src="./images/GTKWave_dff_asyncres.png">

  ##### - Synchronous Set DFF - functional simulation
  ```bash
$ iverilog dff_async_set.v tb_dff_async_set.v
$ ./a.out
$ gtkwave tb_dff_async_set.vcd
  ```
<img alt="GTKWave_dff_asyncset" src="./images/GTKWave_dff_asyncset.png">

  ##### - Synchronous Reset DFF - functional simulation
  ```bash
$ iverilog dff_syncres.v tb_dff_syncres.v
$ ./a.out
$ gtkwave tb_dff_syncres.vcd
  ```
<img alt="GTKWave_dff_syncres" src="./images/GTKWave_dff_syncres.png">

  ##### - Asynchronous Reset, Synchronous Reset DFF - functional simulation
  ```bash
$ iverilog dff_asyncres_syncres.v tb_dff_asyncres_syncres.v
$ ./a.out
$ gtkwave tb_dff_asyncres_syncres.vcd
  ```
<img alt="GTKWave_dff_asyncres_syncres" src="./images/GTKWave_dff_asyncres_syncres.png">

  ##### - Asynchronous Reset DFF - synthesis
  ```
$ yosys

> read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

> read_verilog dff_asyncres.v
> synth -top dff_asyncres
> dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
> abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
> show
  ```
<img alt="Yosys_dff_asyncres" src="./images/Yosys_dff_asyncres.png">
<img alt="dff_asyncres" src="./images/dff_asyncres.png">

  ##### - Asynchronous Set DFF - synthesis
  ```
> read_verilog dff_async_set.v
> synth -top dff_async_set
> dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
> abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
> show
  ```
<img alt="Yosys_dff_asyncset" src="./images/Yosys_dff_asyncset.png">
<img alt="dff_asyncset" src="./images/dff_asyncset.png">

  ##### - Synchronous Reset DFF - synthesis
  ```
> read_verilog dff_syncres.v
> synth -top dff_syncres
> dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
> abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
> show
  ```
<img alt="Yosys_dff_sync_reset" src="./images/Yosys_dff_sync_reset.png">
<img alt="dff_sync_reset" src="./images/dff_sync_reset.png">

#### - Interesting optimisations

##### - Multiplying by two - synthesis
```
$ yosys
> read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib

> read_verilog mult_2.v
> synth -top mul2
> abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
> show
```
<img alt="Yosys_mul2" src="./images/Yosys_mul2.png">

<img alt="mul2" src="./images/mul2.png">

##### - Multiplying by eight - synthesis

> [*** WARNING *****]

> It is actually multiplying by nine
```
> read_verilog mult_8.v
> synth -top mult8
> abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
> show
```
<img alt="Yosys_mult8" src="./images/Yosys_mult8.png">

<img alt="mult8" src="./images/mult8.png">

</details>

<details>
<summary>Combinational and sequential optimizations</summary>

  #### - Sequential logic optimizations
  ```bash
  $ cd sky130RTLDesignAndSynthesisWorkshop/verilog_files
  $ iverilog dff_const3.v tb_dff_const3.v
  $ ./a.out
  $ gtkwave tb_dff_const3.vcd
  ```
  <img alt="GTKWave_dff_const3" src="./images/GTKWave_dff_const3.png">

  ```
  $ yosys
  > read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  > read_verilog dff_const3.v
  > synth -top dff_const3
  > dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  > abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  > show
  ```
  <img alt="Yosys_dff_const3" src="./images/Yosys_dff_const3.png">

  <img alt="dff_const3" src="./images/dff_const3.png">

  <img alt="dff_const3_waveform" src="./images/dff_const3_waveform.png">

</details>

<details>
<summary>Gate-Level Simulation, blocking vs non-blocking, and Synthesis-Simulation mismatches</summary>

  #### - Ternary Operator Mux

  ##### - Functional simulation
  ```bash
$ iverilog ternary_operator_mux.v tb_ternary_operator_mux.v
$ ./a.out
$ gtkwave tb_ternary_operator_mux.vcd
$ mv tb_ternary_operator_mux.vcd tb_ternary_operator_mux_fsim.vcd
  ```
  <img alt="GTKWave_ternary_operator_mux_fsim" src="./images/GTKWave_ternary_operator_mux_fsim.png">

  ##### - Synthesis
  ```
$ yosys
> read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
> read_verilog ternary_operator_mux.v
> synth -top ternary_operator_mux
> abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
> show
  ```
  <img alt="Yosys_ternary_operator_mux" src="./images/Yosys_ternary_operator_mux.png">

  ```
> write_verilog -noattr ternary_operator_mux_net.v
  ```

  ##### - Gate-Level Functional simulation
  ```bash
$ iverilog ../my_lib/verilog_model/primitives.v  ../my_lib/verilog_model/sky130_fd_sc_hd.v ternary_operator_mux_net.v tb_ternary_operator_mux.v
$ ./a.out
$ gtkwave tb_ternary_operator_mux.vcd
$ mv tb_ternary_operator_mux.vcd tb_ternary_operator_mux_gls.vcd
  ```
  <img alt="GTKWave_ternary_operator_mux_gls" src="./images/GTKWave_ternary_operator_mux_gls.png">

  #### - Synthesis-Simulation mismatch - Incomplete sensitivity list

  ##### - Functional simulation
  ```bash
$ iverilog bad_mux.v tb_bad_mux.v
$ ./a.out
$ gtkwave tb_bad_mux.vcd
$ mv tb_bad_mux.vcd tb_bad_mux_fsim.vcd
  ```
  <img alt="GTKWave_bad_mux_fsim" src="./images/GTKWave_bad_mux_fsim.png">

  ##### - Synthesis
  ```
$ yosys
> read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
> read_verilog bad_mux.v
> synth -top bad_mux
> abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
> show
  ```
  <img alt="Yosys_bad_mux" src="./images/Yosys_bad_mux.png">

  ```
$ write_verilog -noattr bad_mux_net.v
  ```

  ##### - Gate-Level Functional simulation
  ```bash
$ iverilog ../my_lib/verilog_model/primitives.v  ../my_lib/verilog_model/sky130_fd_sc_hd.v bad_mux_net.v tb_bad_mux.v
$ ./a.out
$ gtkwave tb_bad_mux.vcd
$ mv tb_bad_mux.vcd tb_bad_mux_gls.vcd
  ```
  <img alt="GTKWave_bad_mux_gls" src="./images/GTKWave_bad_mux_gls.png">

  #### - Synthesis-Simulation mismatch - Misuse of blocking statements

  ##### - Functional simulation
  ```bash
$ iverilog blocking_caveat.v tb_blocking_caveat.v
$ ./a.out
$ gtkwave tb_blocking_caveat.vcd
$ mv tb_blocking_caveat.vcd tb_blocking_caveat_fsim.vcd
  ```
  <img alt="GTKWave_blocking_caveat_fsim" src="./images/GTKWave_blocking_caveat_fsim.png">

  ##### - Synthesis
  ```
$ yosys
> read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
> read_verilog blocking_caveat.v
> synth -top blocking_caveat
> abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
> show
  ```
  <img alt="Yosys_blocking_caveat" src="./images/Yosys_blocking_caveat.png">

  ```
> write_verilog -noattr blocking_caveat_net.v
  ```

  ##### - Gate-Level Functional simulation
  ```bash
$ iverilog ../my_lib/verilog_model/primitives.v  ../my_lib/verilog_model/sky130_fd_sc_hd.v blocking_caveat_net.v tb_blocking_caveat.v
$ ./a.out
$ gtkwave tb_blocking_caveat.vcd
$ mv tb_blocking_caveat.vcd tb_blocking_caveat_gls.vcd
  ```
  <img alt="GTKWave_blocking_caveat_gls" src="./images/GTKWave_blocking_caveat_gls.png">

</details>
