# vsd-hdp
<details>
	<summary>Week 1 - Tools Installation </summary>

## Ubuntu 22.04.5 LTS installation in a VirtualBox Machine
<img alt="VBox" src="/images/OracleVBox-tamurae.png">

## Tools installation

### [Yosys](https://yosyshq.net/yosys/)
```
$ git clone https://github.com/YosysHQ/yosys.git
$ cd yosys 
$ sudo apt install make
$ sudo apt install build-essential clang bison flex \
    libreadline-dev gawk tcl-dev libffi-dev git \
    graphviz xdot pkg-config python3 libboost-system-dev \
    libboost-python-dev libboost-filesystem-dev zlib1g-dev
$ make 
$ sudo make install
```

</details>
