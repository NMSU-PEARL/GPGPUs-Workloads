include ../../common/make.config

CC = gcc
NVCC := $(CUDA_DIR)/bin/nvcc
ARCH := -arch=sm_70
NVCC_FLAGS := -Xptxas -O3 -Icommon -lm

DEFS += -DGPU_TIMER $(SPACE)


CFLAGS += -Icommon -I/usr/include/cuda -O3 -Wall $(SPACE)

# Add source files here
EXECUTABLE  := lud_cuda
# Cuda source files (compiled with cudacc)
CUFILES     := lud_kernel.cu
# C/C++ source files (compiled with gcc / c++)
CCFILES     := lud.c lud_cuda.c common/common.c

OBJS = common/common.o lud.o lud_kernel.o

.PHONY: all clean 
all : $(EXECUTABLE)

.c.o : 
	$(NVCC) $(NVCC_FLAGS) $(ARCH) $(KERNEL_DIM) $(DEFS) -o $@ -c $<

%.o:	%.cu 
	$(NVCC) $(NVCC_FLAGS) $(ARCH) $(KERNEL_DIM) $(DEFS) -o $@ -c $<


$(EXECUTABLE) : $(OBJS)
	$(NVCC) $(NVCC_FLAGS) $(ARCH) -o $@  $?

clean:
	rm -f $(EXECUTABLE) $(OBJS) *.linkinfo

