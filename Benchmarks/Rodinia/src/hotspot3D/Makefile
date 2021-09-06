include ../../common/make.config

NVCC := $(CUDA_DIR)/bin/nvcc
ARCH := -arch=sm_70
NVCC_FLAGS := -w -Xptxas -O3
INCLUDE := $(CUDA_DIR)/include

SRC = 3D.cu
EXE = 3D 
OUTPUT = *.out
FLAGS = -g -G 

release: $(SRC)
	$(NVCC) $(NVCC_FLAGS) $(KERNEL_DIM) $(SRC) -o $(EXE) -I$(INCLUDE) -L$(CUDA_LIB_DIR) 

enum: $(SRC)
	$(NVCC) $(KERNEL_DIM) $(FLAGS) -deviceemu $(SRC) -o $(EXE) -I$(INCLUDE) -L$(CUDA_LIB_DIR) 

debug: $(SRC)
	$(NVCC) $(KERNEL_DIM) $(FLAGS) -g $(SRC) -o $(EXE) -I$(INCLUDE) -L$(CUDA_LIB_DIR) 

debugenum: $(SRC)
	$(NVCC) $(KERNEL_DIM) $(FLAGS) -g -deviceemu $(SRC) -o $(EXE) -I$(INCLUDE) -L$(CUDA_LIB_DIR) 

clean: $(SRC)
	rm -f $(EXE) $(EXE).linkinfo $(OUTPUT) 
