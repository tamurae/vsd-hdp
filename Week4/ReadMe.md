## VSDBabySoC - Timing Analysis

### Tools installation
  
#### [CUDD](https://davidkebo.com/cudd/)

<details>
<summary>Build and install CUDD</summary>

 ```bash
 $ wget https://github.com/davidkebo/cudd/raw/main/cudd_versions/cudd-3.0.0.tar.gz
 $ tar zxvf cudd-3.0.0.tar.gz
 $ cd cudd-3.0.0
 $ ./configure --prefix=$HOME/cudd
 ```
 <img alt="cudd_config" src="./images/cudd_config.png">

 ```bash
 $ make -j$(nproc)
 $ make install

 ```
 <img alt="cudd_install" src="./images/cudd_install.png">

 ```bash
 $ cd  
 ```

</details>

#### [OpenSTA](https://github.com/parallaxsw/OpenSTA)

<details>
<summary>Build and install OpenSTA</summary>

 ```bash
 $ git clone https://github.com/parallaxsw/OpenSTA.git
 $ cd OpenSTA
 $ mkdir build
 $ cd build
 $ cmake -DCUDD_DIR=$HOME/cudd ..
 ```
 <img alt="OpenSTA_cmake" src="./images/OpenSTA_cmake.png">

 ```bash
 $ make -j$(nproc)
 $ ./sta

 ```
 <img alt="OpenSTA" src="./images/OpenSTA.png">

 ```bash
 $ cd  
 ```

</details>

### Timing Analysis Example using the command line

<details>
<summary>Example Circuit</summary>

 ```
 $ cd OpenSTA/examples/
 $ yosys
 > read_liberty -lib nangate45_slow.lib.gz
 > read_verilog example1.v
 > synth -top top
 > show
 ```
 <img alt="example1" src="./images/example1.png">

</details>

<details>
<summary>Clock Setup Analysis for Register-to-Register Path</summary>

  ```
  $ sta
  % read_liberty nangate45_slow.lib.gz
  % read_verilog example1.v
  % link_design top
  % create_clock -name clk -period 10 {clk1 clk2 clk3}
  % set_input_delay -clock clk 0 {in1 in2}
  % report_checks
 ```
 <img alt="OpenSTA_example1" src="./images/OpenSTA_example1.png">

 <img alt="example1_timing" src="./images/example1_timing.png">

</details>

> [!NOTE]  
> The previous analysis did not consider wiring delays

<details>
<summary>Clock Setup Analysis for Register-to-Register Path considering wiring</summary>

This analysis requires using the corresponding [SPEF](https://www.vlsisystemdesign.com/spef-format-part-1/) (Standard Parasitic Exchange Format) file for the circuit

  ```
  $ sta
  % read_liberty nangate45_slow.lib.gz
  % read_verilog example1.v
  % link_design top
  % read_spef example1.dspef
  % create_clock -name clk -period 10 {clk1 clk2 clk3}
  % set_input_delay -clock clk 0 {in1 in2}
  % report_checks
 ```
 <img alt="OpenSTA_example1_spef" src="./images/OpenSTA_example1_spef.png">

 <img alt="example1_timing_spef" src="./images/example1_timing_spef.png">

</details>

### Timing Analysis Example using a [Tcl](https://wiki.tcl-lang.org/page/Tcl+Tutorial+Index) script

<details>
<summary>Clock Setup (max path) and Hold (min path) Analysis</summary>
  
  ```
  $ sta
  % source min_max_delays.tcl
 ```
 <img alt="OpenSTA_example1_tcl" src="./images/OpenSTA_example1_tcl.png">

</details>
