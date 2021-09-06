include ../../common/make.config



# ===============================================================
#	GCC
# ===============================================================
C_C = gcc
# OMP_LIB = -lgomp
# OMP_FLAG = -fopenmp
# OCL_LIB = -lOpenCL


# ===============================================================
#	NVCC
# ===============================================================
CUDA_LIB =	-lcuda -lcudart
NVCC := $(CUDA_DIR)/bin/nvcc
ARCH := -arch=sm_70
NVCC_FLAGS := -Xptxas -O3


# ===============================================================
#	EXECUTABLES (LINK OBJECTS TOGETHER INTO BINARY)
# ===============================================================
b+tree:	./main.o \
		./kernel/kernel_gpu_cuda_wrapper.o \
		./kernel/kernel_gpu_cuda_wrapper_2.o \
		./util/timer/timer.o \
		./util/num/num.o \
		./util/cuda/cuda.o
	$(C_C)	./main.o \
			./kernel/kernel_gpu_cuda_wrapper.o \
			./kernel/kernel_gpu_cuda_wrapper_2.o \
			./util/timer/timer.o \
			./util/num/num.o \
			./util/cuda/cuda.o \
			-lm \
			-L$(CUDA_LIB_DIR) \
			$(CUDA_LIB)\
            -o b+tree


# ===============================================================
#	MAIN FUNCTION
# ===============================================================
main.o:	./common.h \
		./main.h \
		./main.c
	$(C_C)	$(KERNEL_DIM) ./main.c \
			-c \
			-o ./main.o \
			-O3

# ===============================================================
#	KERNELS
# ===============================================================
./kernel/kernel_gpu_cuda_wrapper.o:	./common.h \
									./kernel/kernel_gpu_cuda_wrapper.h \
									./kernel/kernel_gpu_cuda_wrapper.cu
	$(NVCC) $(NVCC_FLAGS) $(ARCH) $(KERNEL_DIM) ./kernel/kernel_gpu_cuda_wrapper.cu \
				-c \
				-o ./kernel/kernel_gpu_cuda_wrapper.o

./kernel/kernel_gpu_cuda_wrapper_2.o:	./common.h \
										./kernel/kernel_gpu_cuda_wrapper_2.h \
										./kernel/kernel_gpu_cuda_wrapper_2.cu
	$(NVCC) $(NVCC_FLAGS) $(ARCH) $(KERNEL_DIM) ./kernel/kernel_gpu_cuda_wrapper_2.cu \
				-c \
				-o ./kernel/kernel_gpu_cuda_wrapper_2.o

# ===============================================================
#	UTILITIES
# ===============================================================
./util/timer/timer.o:	./common.h \
						./util/timer/timer.h \
						./util/timer/timer.c
	$(C_C)	./util/timer/timer.c \
			-c \
			-o ./util/timer/timer.o \
			-O3

./util/num/num.o:	./common.h \
					./util/num/num.h \
					./util/num/num.c
	$(C_C)	./util/num/num.c \
			-c \
			-o ./util/num/num.o \
			-O3

./util/cuda/cuda.o:	./common.h \
					./util/cuda/cuda.h \
					./util/cuda/cuda.cu
	$(NVCC) $(NVCC_FLAGS) $(ARCH)	./util/cuda/cuda.cu \
				-c \
				-o ./util/cuda/cuda.o


# ===============================================================
#	CLEAN
# ===============================================================
clean:
	rm	b+tree *.o \
		./kernel/*.o \
		./util/timer/*.o \
		./util/num/*.o \
		./util/cuda/*.o \
        *.txt
