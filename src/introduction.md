# MPI Fox Algorithm

> Implementation of the Fox algorithm for square matrix multiplication using MPI

![Fox algorithm](./media/fox.gif) 

The objective of this project is to show the **execution time and RAM usage** of the algorithm for different matrix sizes and number of processes. 

The program will run the algorithm for all the matrix sizes \\( 2^x\ \forall\ x \in [n, m] \\) five times and will calculate the average execution time and RAM usage. The results will be used to generate a graph that will be saved in the `graphs` folder.

Developed by:

- José Felipe Marcial Rojas. [Github](https://github.com/Felamar) 
- Miguel Ángel Hernández Moreno. [Github](https://github.com/miguehm) 

## TO DO
- [ ] Add RAM measurement for Windows.
- [x] Create CSV files with the results.
- [x] Add a script to generate the graphs from the CSV files.
- [ ] Add graphs to docs page.

## References

- Dean, N. (2017). Matrix Multiplication. [https://www.cs.csi.cuny.edu/~gu/teaching/courses/csc76010/slides/Matrix%20Multiplication%20by%20Nur.pdf](https://www.cs.csi.cuny.edu/~gu/teaching/courses/csc76010/slides/Matrix%20Multiplication%20by%20Nur.pdf)
- mpi4py. (2023). [https://mpi4py.readthedocs.io/en/stable/](https://mpi4py.readthedocs.io/en/stable/) 
- Matplotlib (2023) [https://matplotlib.org/](https://matplotlib.org/) 
- Manim (2023) [https://docs.manim.community/en/stable/](https://docs.manim.community/en/stable/) 
