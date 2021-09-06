GENCODE_SM70 := -gencode=arch=compute_70,code=\"sm_70,compute_70\"
GENCODE_SM75 := -gencode=arch=compute_75,code=\"sm_75,compute_75\"

ARCH = $(GENCODE_SM70) $(GENCODE_SM75)
#ARCH := -arch=sm_70
NVCC_FLAGS += -Xptxas -O3

CUFILE = gru_host.cu
EXECUTABLE = GRU.out

all:
	nvcc $(NVCC_FLAGS) $(ARCH) ${CUFILE} -o ${EXECUTABLE} 
clean:
	rm -f *~ *.out