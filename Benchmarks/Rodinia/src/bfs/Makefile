include ../../common/make.config


INCLUDE := $(CUDA_DIR)/include
NVCC := $(CUDA_DIR)/bin/nvcc
ARCH := -arch=sm_70
NVCC_FLAGS := -Xptxas -O3

SRC = bfs.cu
EXE = bfs

release: $(SRC)
	$(NVCC) $(NVCC_FLAGS) $(ARCH) $(SRC) -o $(EXE) -I$(INCLUDE) -L$(CUDA_LIB_DIR) 

enum: $(SRC)
	$(NVCC) $(NVCC_FLAGS) $(ARCH) -deviceemu $(SRC) -o $(EXE) -I$(INCLUDE) -L$(CUDA_LIB_DIR) 

debug: $(SRC)
	$(NVCC) $(NVCC_FLAGS) $(ARCH) -g $(SRC) -o $(EXE) -I$(INCLUDE) -L$(CUDA_LIB_DIR) 

debugenum: $(SRC)
	$(NVCC) $(NVCC_FLAGS) $(ARCH) -g -deviceemu $(SRC) -o $(EXE) -I$(INCLUDE) -L$(CUDA_LIB_DIR) 

clean: $(SRC)
	rm -f $(EXE) $(EXE).linkinfo result.txt
