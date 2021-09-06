main ?= default
exe = fw
ARCH := -arch=sm_70
NVCC_FLAGS := -Xptxas -O3

ifeq ($(main),default)
    src += Floyd-Warshall.cu
else ifeq ($(main),Block)
    src += Floyd-Warshalll_Block.cu
endif

$(exe): util.o parse.o
	nvcc $(src) $(NVCC_FLAGS) $(ARCH) util.o parse.o -o $(exe) 

util.o:
	g++ -c ../../graph_parser/util.cpp -O3

parse.o:
	g++ -c parse.cpp -O3

clean:
	rm -f *.o *.out $(exe)
