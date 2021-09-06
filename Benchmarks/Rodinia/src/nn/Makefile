include ../../common/make.config

LOCAL_CC = gcc -g -O3 -Wall -w
NVCC := $(CUDA_DIR)/bin/nvcc
ARCH := -arch=sm_70
NVCC_FLAGS := -Xptxas -O3
INCLUDE := $(CUDA_DIR)/include

all : nn hurricane_gen

clean :
	rm -rf *.o nn hurricane_gen

nn : nn_cuda.cu
	$(NVCC) $(NVCC_FLAGS) $(ARCH) -o nn nn_cuda.cu

hurricane_gen : hurricane_gen.c
	$(LOCAL_CC) -o $@ $< -lm

#data :
#	mkdir data
#	./gen_dataset.sh
