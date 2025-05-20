# VSD - Hardware Design Program
<details>
<summary>Week 1 - Tools Installation </summary>

## Ubuntu 22.04.5 LTS installation in a VirtualBox Machine
<img alt="VBox" src="/images/OracleVBox-tamurae.png">

## Tools installation

### [Yosys](https://yosyshq.net/yosys/)
```
$ sudo apt update
$ sudo apt upgrade
$ sudo apt install build-essential clang bison flex \
    libreadline-dev gawk tcl-dev libffi-dev git \
    graphviz xdot pkg-config python3 libboost-system-dev \
    libboost-python-dev libboost-filesystem-dev zlib1g-dev
$ git clone https://github.com/YosysHQ/yosys.git
$ cd yosys
$ git submodule update --init
$ make config-gcc
$ make 
$ sudo make install
```
<img alt="Yosys" src="/images/yosys.png">

### [Icarus Verilog (iverilog)](https://github.com/steveicarus/iverilog?tab=readme-ov-file#the-icarus-verilog-compilation-system)
```
$ sudo apt install iverilog
```
<img alt="Yosys" src="/images/iverilog.png">

### [GTKWave](https://github.com/gtkwave/gtkwave?tab=readme-ov-file#gtkwave)
```
$ sudo apt install gtkwave
```
<img alt="Yosys" src="/images/GTKWave.png">

### [OpenSTA](https://github.com/The-OpenROAD-Project/OpenSTA?tab=readme-ov-file#static-timing-analysis)
```
$ sudo apt install cmake swig
$ sudo apt install libeigen3-dev tcl-tclreadline
$ wget -c https://github.com/davidkebo/cudd/blob/main/cudd_versions/cudd-3.0.0.tar.gz

```
</details>

<details>
	<summary>Week 2 - Tools Installation (cont.) </summary>

### [ngspice](https://ngspice.sourceforge.io/)

### [Magic VLSI](http://opencircuitdesign.com/magic/)

### [OpenLane](https://github.com/The-OpenROAD-Project/OpenLane)

</details>
