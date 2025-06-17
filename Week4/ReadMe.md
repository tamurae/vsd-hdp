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
