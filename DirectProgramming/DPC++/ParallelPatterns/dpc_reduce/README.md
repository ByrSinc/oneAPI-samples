﻿# `dpc_reduce` Sample

The `dpc_reduce` is a simple program that calculates pi.  This program is implemented using C++ and Data Parallel C++ (DPC++) for Intel&reg; CPU and accelerators. This code sample also demonstrates how to incorporate DPC++ into an MPI program.

For comprehensive instructions see the [DPC++ Programming](https://software.intel.com/en-us/oneapi-programming-guide) and search based on relevant terms noted in the comments.

| Optimized for                     | Description
|:---                               |:---
| OS	                            | Linux* Ubuntu* 18.04,
| Hardware	                    | Skylake with GEN9 or newer,
| Software	                    | Intel® oneAPI DPC++/C++ Compiler
| What you will learn               | how to perform reduction with oneAPI on CPU and GPU
| Time to complete                  | 30 min

## Purpose
This example demonstrates how to do reduction by using one of several methods:
- the CPU in serial mode
- the CPU in parallel mode (using TBB)
- the GPU using direct DPC++ coding
- the GPU using multiple steps with Intel&reg; oneAPI DPC++ Library algorithms transform and reduce,
- Finally, using the oneAPI DPC++ Library transform_reduce algorithm.

All these different modes use a simple calculation for Pi.   It is a well known
mathematical formula that if you integrate from 0 to 1 over the function,
(4.0 / (1+x*x) )dx the answer is pi.   One can approximate this integral
by summing up the area of a large number of rectangles over this same range.

Each of the different function calculates pi by breaking the range into many
tiny rectangles and then summing up the results.

The parallel computations are performed using oneTBB and oneAPI DPC++ Library (oneDPL).

This example also demonstrates how to incorporate Intel Data Parallel C++ into an MPI program.
Using DPC++, the code sample runs multiple MPI ranks to distribute the
calculation of the number Pi. Each rank offloads the computation to an accelerator
(GPU/CPU) using the oneAPI DPC++ Compiler to compute a partial computation of the number Pi.

If you run the sample on a CPU as your default device,  you may need to increase
the memory allocation for OpenCL.  You can do this by setting an environment variable,
    "CL_CONFIG_CPU_FORCE_PRIVATE_MEM_SIZE=16MB


## Key Implementation Details
The basic DPC++ implementation explained in the code includes accessor,
kernels, queues, buffers, as well as some oneDPL calls.

## License

Code samples are licensed under the MIT license. See
[License.txt](https://github.com/oneapi-src/oneAPI-samples/blob/master/License.txt) for details.

Third party program Licenses can be found here: [third-party-programs.txt](https://github.com/oneapi-src/oneAPI-samples/blob/master/third-party-programs.txt)


## Building the dpc_reduce program for CPU and GPU

> Note: if you have not already done so, set up your CLI
> environment by sourcing  the setvars script located in
> the root of your oneAPI installation.
>
> Linux Sudo: . /opt/intel/oneapi/setvars.sh
> Linux User: . ~/intel/oneapi/setvars.sh

### Include Files
The include folder is located at `%ONEAPI_ROOT%\dev-utilities\latest\include` on your development system".

### Running Samples In DevCloud
If running a sample in the Intel DevCloud, remember that you must specify the compute node (CPU, GPU, FPGA) as well whether to run in batch or interactive mode. For more information see the Intel® oneAPI Base Toolkit Get Started Guide (https://devcloud.intel.com/oneapi/get-started/base-toolkit/)


### Using Visual Studio Code*  (Optional)

You can use Visual Studio Code (VS Code) extensions to set your environment, create launch configurations,
and browse and download samples.

The basic steps to build and run a sample using VS Code include:
 - Download a sample using the extension **Code Sample Browser for Intel oneAPI Toolkits**.
 - Configure the oneAPI environment with the extension **Environment Configurator for Intel oneAPI Toolkits**.
 - Open a Terminal in VS Code (**Terminal>New Terminal**).
 - Run the sample in the VS Code terminal using the instructions below.

To learn more about the extensions and how to configure the oneAPI environment, see
[Using Visual Studio Code with Intel® oneAPI Toolkits](https://software.intel.com/content/www/us/en/develop/documentation/using-vs-code-with-intel-oneapi/top.html).

After learning how to use the extensions for Intel oneAPI Toolkits, return to this readme for instructions on how to build and run a sample.

### On a Linux* System
Perform the following steps:
1. Build the program using the following 'cmake' commands
export I_MPI_CXX=dpcpp
mkdir build
cd build
cmake ..
make

2. Run the program using:
make run or './dpc_reduce' or 'mpirun ./dpc_reduce'

3. Clean the program using:
make clean


## Running the Sample
### Application Parameters

        Usage: mpirun -n <num> ./dpc_reduce

where

        <num> : number of MPI rank.


### Example of Output
```c++
Rank #0 runs on: lqnguyen-NUC1, uses device: Intel(R) Gen9 HD Graphics NEO \
Number of steps is 1000000 \
Cpu Seq calc:               PI =3.14 in 0.00422 seconds \
Cpu TBB  calc:              PI =3.14 in 0.00177 seconds \
oneDPL native:              PI =3.14 in 0.209 seconds \
oneDPL native2:             PI =3.14 in 0.213 seconds \
oneDPL native3:             PI =3.14 in 0.00222 seconds \
oneDPL native4:             PI =3.14 in 0.00237 seconds \
oneDPL two steps:           PI =3.14 in 0.0014 seconds \
oneDPL transform_reduce:    PI =3.14 in 0.000528 seconds \
mpi native:                 PI =3.14 in 0.548 seconds \
mpi transform_reduce:       PI =3.14 in 0.000498 seconds \
succes \
```
