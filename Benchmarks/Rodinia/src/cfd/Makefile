include ../../common/make.config

NVCC := $(CUDA_DIR)/bin/nvcc
ARCH := -arch=sm_70
NVCC_FLAGS := -Xptxas -O3
KERNEL_DIM:= -DRD_WG_SIZE_1=128 -DRD_WG_SIZE_2=192 -DRD_WG_SIZE_3=128 -DRD_WG_SIZE_4=256

all: euler3d euler3d_double  pre_euler3d  pre_euler3d_double 

euler3d: euler3d.cu
	$(NVCC) $(NVCC_FLAGS) $(ARCH) $(KERNEL_DIM) euler3d.cu -o euler3d

euler3d_double: euler3d_double.cu
	$(NVCC) $(NVCC_FLAGS) $(ARCH) euler3d_double.cu -o euler3d_double

pre_euler3d: pre_euler3d.cu
	$(NVCC) $(NVCC_FLAGS) $(ARCH) pre_euler3d.cu -o pre_euler3d 

pre_euler3d_double: pre_euler3d_double.cu
	$(NVCC) $(NVCC_FLAGS) $(ARCH) pre_euler3d_double.cu -o pre_euler3d_double 


clean:
	rm -f euler3d euler3d_double pre_euler3d pre_euler3d_double momentum density_energy density *.linkinfo
