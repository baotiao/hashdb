CXX = g++
ifeq ($(__PERF), 1)
	CXXFLAGS = -O0 -g -pg -pipe -fPIC -D__XDEBUG__ -W -Wwrite-strings -Wpointer-arith -Wreorder -Wswitch -Wsign-promo -Wredundant-decls -Wformat -D_GNU_SOURCE -D__STDC_FORMAT_MACROS -std=c++11 -Wno-unused-variable
else
	CXXFLAGS = -O2 -pipe -fPIC -W -Wwrite-strings -Wpointer-arith -Wreorder -Wswitch -Wsign-promo -Wredundant-decls -Wformat -Wall -D_GNU_SOURCE -D__STDC_FORMAT_MACROS -std=c++11 -Wno-unused-variable -Wno-maybe-uninitialized -Wno-unused-parameter
	# CXXFLAGS = -Wall -W -DDEBUG -g -O0 -D__XDEBUG__ 
endif

OBJECT = main

SRC_DIR = ./
THIRD_PATH = ../third

OUTPUT = ./output

LIB_PATH = -L../ \
					 -L../output/lib/ \
					 -L../third/slash/output/lib 

LIBS = -lbitcask \
			 -lslash \
			 -lpthread

INCLUDE_PATH = -I../output/include/ \
							 -I../output \
							 -I../ \
							 -I$(THIRD_PATH)/

.PHONY: all clean main


BASE_BOJS := $(wildcard $(SRC_DIR)/*.cc)
OBJS = $(patsubst %.cc,%.o,$(BASE_BOJS))

all: $(OBJECT)
	rm -rf $(OUTPUT)
	mkdir -p $(OUTPUT)
	mkdir -p $(OUTPUT)/bin
	cp $(OBJECT) $(OUTPUT)/bin/
	rm -rf $(OBJECT)
	@echo "Success, go, go, go..."


main: main.cc
	$(CXX) $(CXXFLAGS) -o $@ $^ $(INCLUDE_PATH) $(LIB_PATH) $(LIBS)


$(OBJS): %.o : %.cc
	$(CXX) $(CXXFLAGS) -c $< -o $@ $(INCLUDE_PATH) 

clean: 
	rm -rf $(OUTPUT)
	rm -f $(SRC_DIR)/*.o
	rm -rf $(OBJECT)
	rm -rf gmon.out

