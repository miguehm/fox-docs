# MPI Fox Algorithm

> Implementation of the Fox algorithm for matrix multiplication using MPI

![](./media/fox.gif) 

We have based the majority of our implementation on the following in the following paper

_Dean, N. (2017). Matrix Multiplication. Retrieved from [https://www.cs.csi.cuny.edu/~gu/teaching/courses/csc76010/slides/Matrix%20Multiplication%20by%20Nur.pdf](https://www.cs.csi.cuny.edu/~gu/teaching/courses/csc76010/slides/Matrix%20Multiplication%20by%20Nur.pdf)_

The objective of this project is to show the execution time and RAM usage of the algorithm for different matrix sizes and number of processes. 

The program will run the algorithm for all the matrix sizes \\( 2^x\ \forall\ x \in [n, m] \\) five times and will calculate the average execution time and RAM usage. The results will be used to generate a graph that will be saved in the `graphs` folder. The graph will be saved in the following format:

Developed by:

- Jose Felipe Marcial Rojas. [Github](https://github.com/Felamar) 
- Miguel Angel Hernández Moreno. [Github](https://github.com/miguehm) 

## TO DO
- [ ] Add RAM measurement for Windows.
- [x] Create CSV files with the results.
- [ ] Add a script to generate the graphs from the CSV files.
- [ ] Add graphs.
