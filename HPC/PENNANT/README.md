PENNANT: an unstructured mesh mini‐app for advanced architecture research
=============

PENNANT is an unstructured mesh physics mini-app designed for advanced architecture research.  It contains mesh data structures and a few physics algorithms adapted from the LANL rad-hydro code FLAG, and gives a sample of the typical memory access patterns of FLAG.

* since the test data is big consider downling the test folder from the source: https://github.com/lanl/PENNANT/tree/cuda/test

* GPU CUDA source code: https://github.com/lanl/PENNANT/tree/cuda


## To build:
* edit the following in the Makefile with the correct information: 

    CUDA_INSTALL_PATH := /software/cuda-10.1   
    CUDACFLAGS := -arch=sm_70

* Then just build the app with make command


## To run all the application with specific input:
* Make sure you have the tests inside this directory

* run the following command with your desried input:
    ```
    ./build/pennant test/<testname>/<testname>.pnt

    ```

* for example running liblancbig:
    ```
    ./build/pennant test/liblancbig/liblancbig.pnt

    ```


## Info about PENNANT can be found at:
* https://www.lanl.gov/projects/crossroads/_assets/docs/ssi/Summary_PENNANT.pdf
* https://onlinelibrary.wiley.com/doi/abs/10.1002/cpe.3422


## Paper:
Ferenbaugh, C. R. (2015) PENNANT: an unstructured mesh mini‐app for advanced architecture research. Concurrency Computat.: Pract. Exper., 27: 4555– 4572. doi: 10.1002/cpe.3422.
