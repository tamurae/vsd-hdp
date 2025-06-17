## VSDBabySoC - Timing Analysis using [OpenSTA](https://github.com/parallaxsw/OpenSTA)

 ### Tools installation
  
  #### [CUDD](https://davidkebo.com/cudd/)

<details>
<summary>Build and install CUDD</summary>

```
$ wget https://github.com/davidkebo/cudd/raw/main/cudd_versions/cudd-3.0.0.tar.gz
$ tar zxvf cudd-3.0.0.tar.gz
$ cd cudd-3.0.0
$ ./configure --prefix=$HOME/cudd
$ make -j$(nproc)
$ make install
$ cd  
```
</details>

