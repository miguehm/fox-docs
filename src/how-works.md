# How Works

<!-- toc -->

# Theoretical Explanation

The Fox matrix multiplication algorithm is an efficient approach for multiplying large matrices divided into blocks. It is based on the technique of block matrix multiplication and is designed to make the most of parallelism in distributed computing architectures. Here's a step-by-step explanation of how to use the Fox matrix multiplication algorithm:

Imagine you have two square matrices \\(A\\) and \\(B\\) of size \\(n \\times n\\), and you want to multiply them to obtain the matrix \\(C\\).

## Block Division of Matrices

Divide the square matrices \\(A\\), \\(B\\), and \\(C\\) into blocks. Suppose you decide to divide each matrix into blocks of size \\(b \\times b\\).

## Distribution of Blocks Among Processors

Assign blocks of matrices \\(A\\) and \\(B\\) to different processors. Each processor will handle a set of blocks.

## Initialization

Initialize matrix \\(C\\) on each processor with zeros.

## Main Loop

Perform a main loop consisting of several steps:

### Local Multiplication

Each processor multiplies its local blocks of \\(A\\) and \\(B\\) and accumulates the result in the corresponding blocks of \\(C\\).

### Communication Between Processors

Blocks of \\(A\\) and \\(B\\) are exchanged between processors in a circular fashion. This allows each processor to obtain the necessary blocks for local multiplications.

### Update Blocks of \\(A\\) and \\(B\\)

After each iteration, update the blocks of \\(A\\) and \\(B\\) to contain the necessary blocks for the next iteration.

## Completion of the Main Loop

Repeat the main loop until all blocks of matrix \\(C\\) have been calculated.

## Results Collection

After completing the main loop, each processor will have a portion of matrix \\(C\\). Use communication functions, such as MPI Allreduce, to combine and sum all parts of \\(C\\) across all processors.

## Final Result

The resulting matrix \\(C\\) contains the product of matrices \\(A\\) and \\(B\\).

This approach leverages parallelization in distributed systems, where each processor performs independent calculations in parallel. The results are then combined to obtain the complete output matrix. The performance of this algorithm is particularly notable for large matrices.

<!-- insert a graphs -->

# How the code works

We use MPI to parallelize the matrix multiplication of randomly generated squared matrices A and B, and it calculates the product matrix C. The matrices are distributed among processes, and each process computes a portion of the final result. The `MPI Allreduce` function is used to combine the partial results from all processes.

## Imports

```python
import os
import numpy as np
from sys import argv
from mpi4py import MPI
from time import perf_counter
```

The code imports necessary libraries, including `os`, `numpy`, `sys`, `mpi4py`, and `time`. `mpi4py` is used for MPI (Message Passing Interface) communication in parallel computing.

## Check Operating System and Define Constants

```python
isLinux = os.name == 'posix'
```

Determines if the operating system is Linux.

```python
if isLinux:
   from resource import getrusage, RUSAGE_SELF
```

On Linux, it imports resource-related functions to measure resource usage.

## Command Line Arguments

```python
exponent = int(argv[1])
isInt = bool(argv[2])
```

Reads command line arguments: `exponent` and `isInt`. These are used to define the size of the matrices and the type of matrix elements.

## MPI Initialization:**

```python
comm = MPI.COMM_WORLD  # get the communicator object
size = comm.Get_size() # total number of processes
rank = comm.Get_rank() # rank of this process
```

Initializes MPI communication, retrieves the total number of processes, and the rank of the current process.

## Matrix Initialization on Rank 0:**

```python
if rank == 0:
   MATRIX_SIZE = 2**exponent
   # generate two random matrices of size MATRIX_SIZE
   # initialize the matrices A, B, and C
   # matrices A and B contain random integers or floats based on 'isInt'
   matrix_A = ...
   matrix_B = ...
   matrix_C = np.zeros((MATRIX_SIZE, MATRIX_SIZE), dtype=int) if isInt else np.zeros((MATRIX_SIZE, MATRIX_SIZE))
   data = (MATRIX_SIZE, matrix_A, matrix_B, matrix_C)
else:
   data = None
```

On the master process (rank 0), it initializes matrices A, B, and C, and packs the data into a tuple (`data`). Other processes receive `None`.

## Broadcast Data to All Processes

```python
data = comm.bcast(data, root=0)  # broadcast the data to all processes
MATRIX_SIZE, matrix_A, matrix_B, matrix_C = data  # unpack the data
```

All processes receive the data using MPI broadcast.

## Matrix Multiplication Loop:**

```python
start_time = perf_counter()
for x in range(MATRIX_SIZE):
   if rank == x % size:
       for i in range(MATRIX_SIZE):
           y = (x + i) % MATRIX_SIZE
           matrix_C[i] += matrix_A[i, y] * matrix_B[y]
```

Each process calculates a row of the matrix C. The rows are distributed among processes, and the multiplication is performed locally.

## MPI Allreduce

```python
comm.Allreduce(MPI.IN_PLACE, matrix_C, op=MPI.SUM)
```

MPI Allreduce function is used to sum the rows of matrix C calculated by each process.

## Print Results

```python
if rank == 0:
   print(perf_counter() - start_time)
   print(getrusage(RUSAGE_SELF).ru_maxrss) if isLinux else print(0)
   format = '%d' if isInt else '%f'
```

The master process prints the execution time and, if on Linux, the RAM memory consumed.

# Graphs

pass
