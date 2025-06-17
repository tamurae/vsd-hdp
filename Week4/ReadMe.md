## VSDBabySoC - Timing Analysis

### Tools installation
  
#### [CUDD](https://davidkebo.com/cudd/)

<details>
<summary>Build and install CUDD</summary>

 ```
 $ wget https://github.com/davidkebo/cudd/raw/main/cudd_versions/cudd-3.0.0.tar.gz
 $ tar zxvf cudd-3.0.0.tar.gz
 $ cd cudd-3.0.0
 $ ./configure --prefix=$HOME/cudd
 ```
 <img alt="cudd_config" src="./images/cudd_config.png">

 ```
 $ make -j$(nproc)
 $ make install

 ```
 <img alt="cudd_install" src="./images/cudd_install.png">

 ```
 $ cd  
 ```

</details>

#### [OpenSTA](https://github.com/parallaxsw/OpenSTA)

<details>
<summary>Build and install OpenSTA</summary>

 ```
 $ git clone https://github.com/parallaxsw/OpenSTA.git
 $ cd OpenSTA
 $ mkdir build
 $ cd build
 $ cmake -DCUDD_DIR=$HOME/cudd ..
 ```
 <img alt="OpenSTA_cmake" src="./images/OpenSTA_cmake.png">

 ```
 $ make -j$(nproc)
 $ ./sta

 ```
 <img alt="OpenSTA" src="./images/OpenSTA.png">

 ```
 $ cd  
 ```

</details>

#### Timing Analysis Example using the command line

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


