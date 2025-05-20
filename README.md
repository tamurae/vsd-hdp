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
    graphviz xdot pkg-config python3 libboost-system-dev \OpenSTA
    libboost-python-dev libboost-filesystem-dev zlib1g-dev
$ git clone https://github.com/YosysHQ/yosys.git
$ cd yosys
$ git submodule update --init
$ make config-gcc
$ make OpenSTA
$ sudo make installOpenSTA
```
<img alt="Yosys" src="/images/yosys.png">

### [Icarus Verilog (iverilog)](https://github.com/steveicarus/iverilog?tab=readme-ov-file#the-icarus-verilog-compilation-system)
```
$ sudo apt install iverilog
```
<img alt="Yosys" src="/images/iverilog.png">

### [GTKWave](https://github.com/gtkwave/gtkwave?tab=readme-ov-file#gtkwave)
```
$ sudo apt install gtkwaveOpenSTA
```
<img alt="Yosys" src="/images/GTKWave.png">

### [OpenSTA](https://github.com/The-OpenROAD-Project/OpenSTA?tab=readme-ov-file#static-timing-analysis)
```
$ sudo apt install cmake swig
$ sudo apt install libeigen3-dev tcl-tclreadline
$ tar xvfz cudd-3.0.0.tar.gz
$ cd cudd-3.0.0
$ ./configure --prefix=/usr/local
$ make
$ sudo make install
$ git clone https://github.com/parallaxsw/OpenSTA.git
$ cd OpenSTA
$ mkdir build
$ cmake -DCUDD_DIR=/usr/local/ .
$ make
$ sudo make install
```
<img alt="OpenSTA" src="/images/OpenSTA.png">
</details>

<details>
	<summary>Week 2 - Tools Installation (cont.) </summary>

### [ngspice](https://ngspice.sourceforge.io/)
```
$ tar -zxvf ngspice-44.2.tar.gz
$ cd ngspice-44.2
$ mkdir release
$ cd release
$ ../configure  --with-x --with-readline=yes --disable-debug
$ make
$ sudo make install
```
<img alt="OpenSTA" src="/images/ngspice.png">

### [Magic VLSI](http://opencircuitdesign.com/magic/)
```
$ sudo apt install m4 tcsh csh tcl-dev tk-dev libx11-dev \
    libcairo2-dev mesa-common-dev libglu1-mesa-dev libncurses-dev
```
### [OpenLane](https://github.com/The-OpenROAD-Project/OpenLane)

</details>
