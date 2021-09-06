main ?= default
exe = pagerank
ARCH := -arch=sm_70
NVCC_FLAGS := -Xptxas -O3

ifeq ($(main),default)
    src += pagerank.cu
else ifeq ($(main),spmv)
    src += pagerank_spmv.cu
endif

$(exe): util.o parse.o
	nvcc $(src) $(NVCC_FLAGS) $(ARCH) util.o parse.o -o $(exe) 

util.o:
	g++ -c ../../graph_parser/util.cpp -O3

parse.o:
	g++ -c ../../graph_parser/parse.cpp -O3

clean:
	rm -f *.o *.out $(exe)