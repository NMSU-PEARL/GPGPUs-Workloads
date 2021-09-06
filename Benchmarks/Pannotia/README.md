Pannotia v0.9
=============

© 2014 Advanced Micro Devices, Inc. All rights reserved.

Pannotia is a suite of parallel graph applications.
It is implemented with OpenCL and consists of applications from
diverse graph domains such as shortest path, graph partitioning, 
and web and graph analytics.

Here is the link for Pannotia wiki: https://github.com/pannotia/pannotia/wiki

## To build:

* build all applications with make command
    ```
    make all
    ```
 * you can also build specific application, for example building 2mm app:   
    ```
    make -C graph_app/bc
    ```

## To run: 
* see ***how_to_run.txt*** for each application inside ***graph_app*** directory
* see ***run_nvprof_rodinia.sh*** for running all the applications with ***nvprof*** while collecting some metrics, you can define your metrics list inside the file

## Paper:
S. Che et al., Pannotia: Understanding Irregular GPGPU Graph Applications. In Proceedings of the IEEE International Symposium on Workload Characterization (IISWC), Sept. 2013.
