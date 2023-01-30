# Operating System Requirement
For this tutorial we are using a fresh installation of ubuntu 20.04 (LTS)[Download link](https://releases.ubuntu.com/focal/ubuntu-20.04.5-desktop-amd64.iso)  with minimal installation options. 
We can try with different versions of any *NIX based operating systems but then the installation requirements will vary. 

# Installing Dependencies

## Update apt-get 
First, update the apt-get so you have correct repository links. This command updates the package lists from the existing repositories. Ubuntu by default comes with some repository lists. 

```
sudo apt-get update 
```
## Installing required packages
Then install the following required softwares. Gem5 requires some tools/software to function properly. You can install those via the follwing command 
```
sudo apt install clang llvm lld git m4 scons libprotobuf-dev libgoogle-perftools-dev python3-dev libhdf5-dev libpng-dev
```

# Getting Gem5
## Get Gem5 source files
For this tutorial we will be using gem5 v22.1.0 [Download Link](https://github.com/gem5/gem5/archive/refs/tags/v22.1.0.0.tar.gz) 
There are other versions of gem5 that can be used too. However, each versions might have different requirements and working features. use the following command to get the gem5 in your current directory
```
wget https://github.com/gem5/gem5/archive/refs/tags/v22.1.0.0.tar.gz
```

## Untar the gzipped archive 
This command will unzip (untar) the archive to gem5-v22.1.0.0 directory
```
tar xvzf v22.1.0.0.tar.gz
```



# Install & Run

## Change directory to the gem5 directory
```
cd gem5-22.1.0.0 
```

## Install gem5.opt binary using scons

```
scons build/X86/gem5.opt -j8
```
Here, we are using ```-j8``` to use 8 threads. If our systems have more threads, we can use that. This step requires a long time (~hours). If you get compilation error, try to compile without -j flag 
This will built the gem5 executable which is optimal for X86 ISA. You can build for other ISAs like (ARM, RISCV, MIPS etc.)

## Run hello world example in Syscall Emulation Mode
```
./build/X86/gem5.opt configs/example/se.py -c tests/test-progs/hello/bin/x86/linux/hello
```

This should produce a ```Hello world!``` example using the Syscall Emulation (SE) mode as we have used the ```configs/example/se.py``` file as configuration file. Results of this simulation will be saved in ```m5out``` directory


<!-- # Full System Mode

## Get Linux Kernel
For this tutorial we are using 5.15.90 LTS kernel 
```
wget https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-5.15.90.tar.xz
```

Decompress the archive 
```
tar -xJvf linux-5.15.90.tar.xz 
``` -->

