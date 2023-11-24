# Fox MPI

<!-- toc -->

We use MPI to parallelize the matrix multiplication of randomly generated squared matrices A and B, and it calculates the product matrix C. The matrices are distributed among processes, and each process computes a portion of the final result. The `MPI Allreduce` function is used to combine the partial results from all processes.

# Imports

```python
import os
import numpy as np
from sys import argv
from mpi4py import MPI
from time import perf_counter
```

The code imports necessary libraries, including `os`, `numpy`, `sys`, `mpi4py`, and `time`. `mpi4py` is used for MPI (Message Passing Interface) communication in parallel computing.

# Check Operating System and Define Constants

```python
isLinux = os.name == 'posix'
```

Determines if the operating system is Linux.

```python
if isLinux:
   from resource import getrusage, RUSAGE_SELF
```

On Linux, it imports resource-related functions to measure resource usage.

# Command Line Arguments

```python
exponent = int(argv[1])
isInt = bool(argv[2])
```

Reads command line arguments: `exponent` and `isInt`. These are used to define the size of the matrices and the type of matrix elements.

# MPI Initialization

```python
comm = MPI.COMM_WORLD  # get the communicator object
size = comm.Get_size() # total number of processes
rank = comm.Get_rank() # rank of this process
```

Initializes MPI communication, retrieves the total number of processes, and the rank of the current process.

# Matrix Initialization on Rank 0

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

# Broadcast Data to All Processes

```python
data = comm.bcast(data, root=0)  # broadcast the data to all processes
MATRIX_SIZE, matrix_A, matrix_B, matrix_C = data  # unpack the data
```

All processes receive the data using MPI broadcast.

# Matrix Multiplication Loop

```python
start_time = perf_counter()
for x in range(MATRIX_SIZE):
   if rank == x % size:
       for i in range(MATRIX_SIZE):
           y = (x + i) % MATRIX_SIZE
           matrix_C[i] += matrix_A[i, y] * matrix_B[y]
```

Each process calculates a row of the matrix C. The rows are distributed among processes, and the multiplication is performed locally.

# MPI Allreduce

```python
comm.Allreduce(MPI.IN_PLACE, matrix_C, op=MPI.SUM)
```

MPI Allreduce function is used to sum the rows of matrix C calculated by each process.

# Print Results

```python
if rank == 0:
   print(perf_counter() - start_time)
   print(getrusage(RUSAGE_SELF).ru_maxrss) if isLinux else print(0)
```

The master process prints the execution time and the RAM memory usage if the operating system is Linux.
