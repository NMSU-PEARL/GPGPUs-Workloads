include ../../common/make.config

NVCC := $(CUDA_DIR)/bin/nvcc
ARCH := -arch=sm_70
NVCC_FLAGS := -Xptxas -O3
INCLUDE := $(CUDA_DIR)/include

SRC = pathfinder.cu
EXE = pathfinder

release:
	$(NVCC) $(NVCC_FLAGS) $(ARCH) $(SRC) -o $(EXE) -I$(INCLUDE) -L$(CUDA_LIB_DIR) 

enum:
	$(NVCC) $(NVCC_FLAGS) $(ARCH) -deviceemu $(SRC) -o $(EXE) -I$(INCLUDE) -L$$(CUDA_LIB_DIR) 

debug:
	$(NVCC) $(NVCC_FLAGS) $(ARCH) -g $(SRC) -o $(EXE) -I$(INCLUDE) -L$$(CUDA_LIB_DIR) 

debugenum:
	$(NVCC) $(NVCC_FLAGS) $(ARCH) -g -deviceemu $(SRC) -o $(EXE) -I$(INCLUDE) -L$(CUDA_LIB_DIR) 

clean:
	rm -f pathfinder