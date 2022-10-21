# Core Decomposition Algorithms

This repository implements the algorithms presented in our monograph “Cohesive Subgraph Computation over Large Sparse Graphs”. If you are using the code, please cite our monograph.
<pre>
Lijun Chang and Lu Qin.
<a href="https://www.springer.com/us/book/9783030035983">Cohesive Subgraph Computation over Large Sparse Graphs.</a>
Springer Series in the Data Sciences, 2018
</pre>

## Compile the code
```sh
$ make clean
$ make
```
It generates an executable "core_decompose"

## Run the code
```sh
$ ./core_decompose ../datasets/as-skitter/ list-heap output
$ ./core_decompose ../datasets/as-skitter/ array-heap output
$ ./core_decompose ../datasets/as-skitter/ h-index output
$ ./core_decompose ../datasets/as-skitter/ output
$ ./core_decompose ../datasets/as-skitter/ hierarchy output
```
Note that, parameter "output" is optional
* list-heap uses linked list-based linear heap for core decomposition
* array-heap uses array-based linear heap for core decomposition
* h-index uses h-index-based core decomposition
* The third one is similar to array-heap, but directly implements the logic of the data structure within core decomposition without explicitly constructing a new class
* hierarchy constructs the core spanning tree

## Python bindings
To have the python bindings, you need to install the [SWIG-4.0](https://www.swig.org/) tool, e.g. in Ubuntu linux
```sh
$ sudo apt install swig-4.0
```
It is also advised to construct a virtual environment for python using conda or python virtual environment, e.g. 
```sh
$ conda create -p ./.venv -c local --offline
$ conda activate ./.venv
```
Afterwards, you need to build the SWIG wrappers: 
```sh
$ make python
```
Next, you can use the algorithms as follows:
```python
>>> from Graph import Graph
>>> g = Graph('../datasets/as-skitter/')
>>> g.core_decomposition(0, True)
*** core_decomposition  (Release): ../datasets/as-skitter/ ***
# Start reading graph, Require files "b_degree.bin" and "b_adj.bin"
*	n = 1,694,616; m = 11,094,209 (undirected)
	Max core value: 111, two_core size: 1,463,934
	Total processing time excluding I/O: 2,537,172

>>> g.core_decomposition(1, True)
*** core_decomposition list-heap (Release): ../datasets/as-skitter/ ***
# Start reading graph, Require files "b_degree.bin" and "b_adj.bin"
*	n = 1,694,616; m = 11,094,209 (undirected)
	Max core value: 111, two_core size: 1,463,934
	Total processing time excluding I/O: 2,153,243

>>> g.core_decomposition(2, True)
*** core_decomposition array-heap (Release): ../datasets/as-skitter/ ***
# Start reading graph, Require files "b_degree.bin" and "b_adj.bin"
*	n = 1,694,616; m = 11,094,209 (undirected)
	Max core value: 111, two_core size: 1,463,934
	Total processing time excluding I/O: 2,544,336

>>> g.core_decomposition_hindex(True)
*** core_decomposition h-index (Release): ../datasets/as-skitter/ ***
# Start reading graph, Require files "b_degree.bin" and "b_adj.bin"
*	n = 1,694,616; m = 11,094,209 (undirected)
	Total processing time excluding I/O: 2,963,246

>>> g.core_hierarchy(True)
*** core_hierarchy (Release): ../datasets/as-skitter/ ***
# Start reading graph, Require files "b_degree.bin" and "b_adj.bin"
*	n = 1,694,616; m = 11,094,209 (undirected)
	Total processing time excluding I/O: 3,530,040
```
