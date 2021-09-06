GENCODE_SM70 := -gencode=arch=compute_70,code=\"sm_70,compute_70\"
GENCODE_SM75 := -gencode=arch=compute_75,code=\"sm_75,compute_75\"

ARCH = $(GENCODE_SM70) $(GENCODE_SM75)

BUILDDIR := build
PRODUCT := pennant

SRCDIR := src

HDRS := $(wildcard $(SRCDIR)/*.hh)
SRCS := $(wildcard $(SRCDIR)/*.cc)
OBJS := $(SRCS:$(SRCDIR)/%.cc=$(BUILDDIR)/%.o)
DEPS := $(SRCS:$(SRCDIR)/%.cc=$(BUILDDIR)/%.d)

HDRS += $(SRCDIR)/HydroGPU.hh
SRCS += $(SRCDIR)/HydroGPU.cu
OBJS += $(BUILDDIR)/HydroGPU.o
DEPS += $(BUILDDIR)/HydroGPU.d

BINARY := $(BUILDDIR)/$(PRODUCT)

CPPFLAGS := -I.

# begin compiler-dependent flags
#
# gcc flags:
CXX := g++
CXXFLAGS_DEBUG := -g
CXXFLAGS_OPT := -O3
CXXFLAGS_OPENMP := -fopenmp


# intel flags:
#CXX := icpc
#CXXFLAGS_DEBUG := -g
#CXXFLAGS_OPT := -O3 -fast -fno-alias
#CXXFLAGS_OPENMP := -openmp

# pgi flags:
#CXX := pgCC
#CXXFLAGS_DEBUG := -g
#CXXFLAGS_OPT := -O3 -fastsse
#CXXFLAGS_OPENMP := -mp

# end compiler-dependent flags

CUDAC := nvcc
CUDA_INSTALL_PATH := /software/cuda-10.1
CUDACFLAGS := $(ARCH)
CUDACFLAGS_DEBUG := -G -lineinfo


LD := $(CXX)
LDFLAGS := -L$(CUDA_INSTALL_PATH)/lib64 -lcudart

# select optimized or debug
CXXFLAGS := $(CXXFLAGS_OPT) $(CPPFLAGS)
CUDACFLAGS += $(CUDACFLAGS_OPT) $(CPPFLAGS)
#CXXFLAGS := $(CXXFLAGS_DEBUG) $(CPPFLAGS)
#CUDACFLAGS += $(CUDACFLAGS_DEBUG) $(CPPFLAGS)

# add openmp flags (comment out for serial build)
#CXXFLAGS += $(CXXFLAGS_OPENMP)
#LDFLAGS += $(CXXFLAGS_OPENMP)

all : $(BINARY)

-include $(DEPS)

$(BINARY) : $(OBJS)
	@echo linking $@
	$(maketargetdir)
	$(LD) -o $@ $^ $(LDFLAGS)

$(BUILDDIR)/%.o : $(SRCDIR)/%.cc
	@echo compiling $<
	$(maketargetdir)
	$(CXX) $(CXXFLAGS) $(CXXINCLUDES) -c -o $@ $<

$(BUILDDIR)/%.o : $(SRCDIR)/%.cu
	@echo compiling $<
	$(maketargetdir)
	@# unsetting of CPATH is needed to make nvcc and icpc
	@# play nicely together
	(CPATH=;$(CUDAC) $(CUDACFLAGS) $(CPPFLAGS) -c -o $@ $<)

$(BUILDDIR)/%.d : $(SRCDIR)/%.cc
	@echo making depends for $<
	$(maketargetdir)
	@$(CXX) $(CXXFLAGS) $(CXXINCLUDES) -M $< | sed "1s![^ \t]\+\.o!$(@:.d=.o) $@!" >$@

$(BUILDDIR)/%.d : $(SRCDIR)/%.cu
	@echo making depends for $<
	$(maketargetdir)
	@$(CUDAC) $(CUDACFLAGS) $(CPPFLAGS) -M $< | sed "1s![^ \t]\+\.o!$(@:.d=.o) $@!" >$@

define maketargetdir
	-@mkdir -p $(dir $@) > /dev/null 2>&1
endef

clean :
	rm -f $(BINARY) $(OBJS) $(DEPS)