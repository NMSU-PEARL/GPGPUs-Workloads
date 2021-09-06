main ?= csr
exe = sssp
ARCH := -arch=sm_70
NVCC_FLAGS := -Xptxas -O3

ifeq ($(main),csr)
    src += sssp_csr.cu
else ifeq ($(main),ell)
    src += sssp_ell.cu
endif

$(exe): util.o parse.o
	nvcc $(src) $(NVCC_FLAGS) $(ARCH) util.o parse.o -o $(exe) 

util.o:
	g++ -c ../../graph_parser/util.cpp -O3

parse.o:
	g++ -c ../../graph_parser/parse.cpp -O3

clean:
	rm -f *.o *.out $(exe)
