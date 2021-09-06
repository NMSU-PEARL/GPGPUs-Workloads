## To build:

* build all applications with make command
    ```
    make all
    ```
 * you can also build specific application, for example building 2mm app:   
    ```
    make -C src/nn

## To run: 
* see ***how_to_run.txt*** for each application inside the src directory
* see ***run_nvprof_rodinia.sh*** for running all the applications with ***nvprof*** while collecting some metrics, you can define your metrics list inside the file

## Paper: 

S. Che et al., "Rodinia: A benchmark suite for heterogeneous computing," 2009 IEEE International Symposium on Workload Characterization (IISWC), Austin, TX, 2009, pp. 44-54, doi: 10.1109/IISWC.2009.5306797.
