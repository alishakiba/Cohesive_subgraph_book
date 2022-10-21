# ********     Author: Lijun Chang    ******
# ******** Email: ljchang@outlook.com ******
#
CC=g++ -flto -O3
CFLAGS=-c -I. -std=c++11
SWIG=swig4.0
SWIGFLAGS=-c++ -python
PYTHON=python

all: core_decompose

core_decompose: .obj/main.o .obj/Graph.o
	${CC} .obj/main.o .obj/Graph.o -o core_decompose
	rm .obj/*.o

.obj/main.o: main.cpp
	${CC} ${CFLAGS} -o .obj/main.o main.cpp

.obj/Graph.o: Graph.cpp
	${CC} ${CFLAGS} -o .obj/Graph.o Graph.cpp

clean:
	rm -rf *o .obj/
	mkdir .obj

python: 
	mkdir -p cppfiles
	mkdir -p pyfiles
	${SWIG} ${SWIGFLAGS} Graph.i
	${PYTHON} setup.py build_ext --inplace 
