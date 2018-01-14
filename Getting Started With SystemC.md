### Prerequisites

```
$ sudo apt-get update
$ sudo apt-get  install build-essential
$ sudo apt-get install linux-headers-$(uname -r)
```
### SystemC download and installation

1. Download systemc package from official site [Accellera website](http://www.accellera.org/downloads/standards/systemc).
2. Untar the package
```
$ tar -xzvf systemc-2.3.1a.tar.gz
$ ls systemc-2.3.1a
```
3. Make a directory `systemc_installed` for installation in your `/usr/local/` path. As i have no root permission i am creating this directory in local folder. Also create temporary directory to process installation files.
```
$ mkdir systemc_installed
$ mkdir objdir
```
4. Compile & Build SystemC.
```
$ cd objdir/
$ ../systemc-2.3.1a/configure --prefix=<absolute_path_to_>/systemc_installed
$ make && make install
$ ls systemc_installed
```
Note: Use `sudo make && make install`, if your installation directory is in `/` (root) directory.
Thats all! the installation is done.

### Hello World
- Create hello.cpp file as follows : 
```
#include <iostream>
#include <systemc>

using namespace std;

SC_MODULE(hello)
{
	SC_CTOR(hello)
	{
		cout<<"Hello World"<<endl;
	}
};

int sc_main(int argc, char *argv[])
{
	hello 	h("h");

	return 0;
}
```
#### Compilation
```
$ export SYSTEMC_HOME=<absolute_path_to_>/systemc_installed
$ g++ -I$SYSTEMC_HOME/include -L$SYSTEMC_HOME/lib-linux64 -Wl,-rpath=$SYSTEMC_HOME/lib-linux64 -o sim hello.cpp -lsystemc -lm
$ ./sim
        SystemC 2.3.1-Accellera --- Jul  3 2017 09:46:22
        Copyright (c) 1996-2014 by all Contributors,
        ALL RIGHTS RESERVED
Hello World
```

### Documentations
- I would prefer doxygen docs as there are lot of benefits of using it, you can find that on internet by yourself & if you want rapid start you can follow [this](https://github.com/VisheshPatel/DeveloperUseful/blob/master/doxygen.md).
- Please note that graphviz if dependency for doxygen & doxygen should be preinstalled.
- After the installation of SystemC, go to docs/sysc/doxygen in the installed folder(i.e. 'systemc_installed' in out case). There you will find doxygen project file. You have to generate browsable .html file for documentation.
```
$ cd $SYSTEMC_HOME/docs/sysc/doxygen
$ doxygen Doxyfile
....
Patching output file 330/332
Patching output file 331/332
Patching output file 332/332
lookup cache used 15080/65536 hits=283764 misses=16094
finished...
$ firefox html/index.html
```
- That's it. You promoted with SystemC documentation message in browser.

