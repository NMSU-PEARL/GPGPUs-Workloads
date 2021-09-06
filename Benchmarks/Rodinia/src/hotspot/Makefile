include ../../common/make.config

KERNEL_DIM := -DRD_WG_SIZE_0=16

NVCC := $(CUDA_DIR)/bin/nvcc
ARCH := -arch=sm_70
NVCC_FLAGS := -w -Xptxas -O3
INCLUDE := $(CUDA_DIR)/include

SRC = hotspot.cu
EXE = hotspot

release: $(SRC)
	$(NVCC) $(NVCC_FLAGS) $(ARCH) $(KERNEL_DIM) $(SRC) -o $(EXE) -I$(INCLUDE) -L$(CUDA_LIB_DIR) 

enum: $(SRC)
	$(NVCC) $(NVCC_FLAGS) $(ARCH) $(KERNEL_DIM) -deviceemu $(SRC) -o $(EXE) -I$(INCLUDE) -L$(CUDA_LIB_DIR) 

debug: $(SRC)
	$(NVCC) $(NVCC_FLAGS) $(ARCH) $(KERNEL_DIM) -g $(SRC) -o $(EXE) -I$(INCLUDE) -L$(CUDA_LIB_DIR) 

debugenum: $(SRC)
	$(NVCC) $(NVCC_FLAGS) $(ARCH) $(KERNEL_DIM) -g -deviceemu $(SRC) -o $(EXE) -I$(INCLUDE) -L$(CUDA_LIB_DIR) 

clean: $(SRC)
	rm -f $(EXE) $(EXE).linkinfo result.txt
