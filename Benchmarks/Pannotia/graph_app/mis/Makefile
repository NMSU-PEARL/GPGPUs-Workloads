exe = mis
ARCH := -arch=sm_70
NVCC_FLAGS := -Xptxas -O3

src = mis.cu

$(exe): util.o parse.o
	nvcc $(src) $(NVCC_FLAGS) $(ARCH) util.o parse.o -o $(exe) 

util.o:
	g++ -c ../../graph_parser/util.cpp -O3

parse.o:
	g++ -c ../../graph_parser/parse.cpp -O3

clean:
	rm -f *.o *.out $(exe)
