include ../../common/make.config

NVCC := $(CUDA_DIR)/bin/nvcc
ARCH := -arch=sm_70
NVCC_FLAGS := -w -Xptxas -O3 


all: naive float

naive: ex_particle_CUDA_naive_seq.cu
	$(NVCC) $(NVCC_FLAGS) $(ARCH) -L$(CUDA_LIB_DIR) -lcuda -g -lm ex_particle_CUDA_naive_seq.cu -o particlefilter_naive
	
float: ex_particle_CUDA_float_seq.cu
	$(NVCC) $(NVCC_FLAGS) $(ARCH) -L$(CUDA_LIB_DIR) -lcuda -g -lm ex_particle_CUDA_float_seq.cu -o particlefilter_float

clean:
	rm particlefilter_naive particlefilter_float
