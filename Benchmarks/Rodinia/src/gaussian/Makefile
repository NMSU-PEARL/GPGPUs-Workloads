include ../../common/make.config

KERNEL_DIM := -DRD_WG_SIZE_0=128 -DRD_WG_SIZE_1=16

NVCC := $(CUDA_DIR)/bin/nvcc
ARCH := -arch=sm_70
NVCC_FLAGS := -Xptxas -O3


INCLUDE := $(CUDA_DIR)/include

SRC = gaussian.cu
EXE = gaussian

release: $(SRC)
	$(NVCC) $(NVCC_FLAGS) $(ARCH) $(KERNEL_DIM) $(SRC) -o $(EXE) -I$(INCLUDE) -L$(CUDA_LIB_DIR) 

clean:
	rm gaussian
