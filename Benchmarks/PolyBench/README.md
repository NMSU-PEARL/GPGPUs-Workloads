## To build:

* If you want to generate code for any other  GPU architecture or add any nvcc flags, you can do so in utilities/common.mk:   

* build all applications with make command
    ```
    make all
    ```
 * you can also build specific application, for example building 2mm app:   
    ```
    make -C linear-algebra/2mm
    ```

## To run: 
* run the binary of each application directory, applications are inside ***datamining, linear-algebra,*** and ***stencils*** directories. If you want to change the input; see ***application.cuh*** file for each application before building
* see ***run_nvprof_rodinia.sh*** for running all the applications with ***nvprof*** while collecting some metrics, you can define your metrics list inside the file

## Paper: 

S. Grauer-Gray, L. Xu, R. Searles, S. Ayalasomayajula and J. Cavazos, "Auto-tuning a high-level language targeted to GPU codes," 2012 Innovative Parallel Computing (InPar), San Jose, CA, 2012, pp. 1-10, doi: 10.1109/InPar.2012.6339595.
