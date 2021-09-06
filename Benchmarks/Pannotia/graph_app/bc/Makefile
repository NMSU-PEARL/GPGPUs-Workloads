exe = bc
ARCH := -arch=sm_70
NVCC_FLAGS := -Xptxas -O3

src = BC.cu 

$(exe): util.o
	nvcc $(src) $(NVCC_FLAGS) $(ARCH) util.o -o $(exe) 

util.o:
	g++ -c ../../graph_parser/util.cpp -O3

clean:
	rm -f *.o $(exe)
