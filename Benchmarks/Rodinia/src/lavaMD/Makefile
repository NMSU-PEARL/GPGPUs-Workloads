include ../../common/make.config

# Example
# target: dependencies
	# command 1
	# command 2
          # .
          # .
          # .
	# command n
ifdef OUTPUT
override OUTPUT = -DOUTPUT
endif

C_C = gcc -w
OMP_LIB = -lgomp
OMP_FLAG = -fopenmp


KERNEL_DIM := -DRD_WG_SIZE_0=128

NVCC := $(CUDA_DIR)/bin/nvcc
ARCH := -arch=sm_70
NVCC_FLAGS := -w -Xptxas -O3


# link objects (binaries) together
a.out:		main.o \
			./kernel/kernel_gpu_cuda_wrapper.o \
			./util/num/num.o \
			./util/timer/timer.o \
			./util/device/device.o
	$(C_C)	$(KERNEL_DIM) main.o \
			./kernel/kernel_gpu_cuda_wrapper.o \
			./util/num/num.o \
			./util/timer/timer.o \
			./util/device/device.o \
			-lm \
			-L/usr/local/cuda/lib64 \
			-lcuda -lcudart \
			$(OMP_LIB) \
			-o lavaMD

# compile function files into objects (binaries)
main.o:		main.h \
			main.c \
			./kernel/kernel_gpu_cuda_wrapper.h \
			./kernel/kernel_gpu_cuda_wrapper.cu \
			./util/num/num.h \
			./util/num/num.c \
			./util/timer/timer.h \
			./util/timer/timer.c \
			./util/device/device.h \
			./util/device/device.cu
	$(C_C)	$(KERNEL_DIM) $(OUTPUT) main.c \
			-c \
			-o main.o \
			-O3

./kernel/kernel_gpu_cuda_wrapper.o:	./kernel/kernel_gpu_cuda_wrapper.h \
									./kernel/kernel_gpu_cuda_wrapper.cu
	$(NVCC) $(NVCC_FLAGS) $(ARCH) $(KERNEL_DIM)						./kernel/kernel_gpu_cuda_wrapper.cu \
									-c \
									-o ./kernel/kernel_gpu_cuda_wrapper.o \
									-O3 \
									$(CUDA_FLAG)

./util/num/num.o:	./util/num/num.h \
					./util/num/num.c
	$(C_C)			./util/num/num.c \
					-c \
					-o ./util/num/num.o \
					-O3

./util/timer/timer.o:	./util/timer/timer.h \
						./util/timer/timer.c
	$(C_C)				./util/timer/timer.c \
						-c \
						-o ./util/timer/timer.o \
						-O3

./util/device/device.o:	./util/device/device.h \
						./util/device/device.cu
	$(NVCC) $(NVCC_FLAGS) $(ARCH) ./util/device/device.cu \
						-c \
						-o ./util/device/device.o \
						-O3

# delete all object and executable files
clean:
	rm	*.o \
		./kernel/*.o \
		./util/num/*.o \
		./util/timer/*.o \
		./util/device/*.o \
		lavaMD
