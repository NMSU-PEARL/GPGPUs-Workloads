include ../../common/make.config

CC = g++
GCC_OPTS=-O3 -Wall -Wextra -m64
NVCC := $(CUDA_DIR)/bin/nvcc
ARCH := -arch=sm_70
NVCC_FLAGS := -w -Xptxas -O3

OBJ = main_test_cu.o stats_logger.o vlc_kernel_sm64huff.o scan.o pack_kernels.o cpuencode.o
SRC = main_test_cu.cu
EXE = pavle

ifdef TESTING 
override TESTING = -DTESTING
endif

ifdef CACHECWLUT
override TESTING = -DCACHECWLUT
endif

pavle: $(OBJ) 
	$(NVCC) $(NVCC_FLAGS) $(ARCH) $(TESTING) $(CACHECWLUT) $(OBJ) -o $(EXE) 

vlc_kernel_sm64huff.o: vlc_kernel_sm64huff.cu 
	$(NVCC) $(NVCC_FLAGS) $(ARCH) $(TESTING) -c vlc_kernel_sm64huff.cu 

scan.o: scan.cu 
	$(NVCC) $(NVCC_FLAGS) $(ARCH) -c scan.cu

#cpuencode.o: cpuencode.cu
#	$(NVCC) -c $(NVCC_OPTS) cpuencode.cu

pack_kernels.o: pack_kernels.cu 
	$(NVCC) $(NVCC_FLAGS) $(ARCH) -c pack_kernels.cu

main_test_cu.o: main_test_cu.cu cutil.h
	$(NVCC) $(NVCC_FLAGS) $(ARCH) $(TESTING) -c main_test_cu.cu 

.o:.cpp
	$(CC) ++ $(GCC_OPTS) -c $@ -o $<

clean:
	rm -f *.o $(EXE) 
