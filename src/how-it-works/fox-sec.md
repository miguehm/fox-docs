# Fox in Secuencial

<!-- toc -->

Sequential implementation of the Fox matrix multiplication algorithm. It initializes matrices, performs the multiplication, prints execution time and resource usage. The progress bar (`tqdm`) visualizes the iteration progress.

# Imports

```python
import os
import numpy as np
from sys import argv
from tqdm import tqdm
from time import perf_counter
```

We import necessary libraries, including `os`, `numpy`, `sys`, `tqdm` (for progress bar), and `time`.

# Check Operating System and Define Constants

```python
isLinux = os.name == 'posix'
if isLinux:
   from resource import getrusage, RUSAGE_SELF
```

Determines if the operating system is Linux and imports resource-related functions for measuring resource usage.

# Matrix Multiplication Function:**

```python
def fox_SEC(exponent: int, isInt: bool) -> float:
```

Defines a function `fox_SEC` that takes the exponent and a flag `isInt` as parameters and returns the execution time.

# Matrix Initialization

```python
MATRIX_SIZE = 2**exponent
matrix_A = ...
matrix_B = ...
matrix_C = np.zeros((MATRIX_SIZE, MATRIX_SIZE), dtype=int) if isInt else np.zeros((MATRIX_SIZE, MATRIX_SIZE))
```

Initializes square matrices \(A\), \(B\), and \(C\) of size \(2^{\text{exponent}} \times 2^{\text{exponent}}\) with random integers or floats based on the `isInt` flag.

# Matrix Multiplication Loop

```python
start_time = perf_counter()

for x in tqdm(range(MATRIX_SIZE)):
   for i in range(MATRIX_SIZE):
       y = (x + i) % MATRIX_SIZE
       matrix_C[i] += matrix_A[i, y] * matrix_B[y]
```

Performs matrix multiplication using nested loops. It calculates the product matrix \(C\) by iterating through rows and columns.

# Print Results

```python
print(perf_counter() - start_time)
print(getrusage(RUSAGE_SELF).ru_maxrss) if isLinux else print(0)
```

Prints the execution time and the RAM usage if the operating system is Linux.

# Main Execution

```python
if __name__ == '__main__':
   fox_SEC(int(argv[1]), bool(argv[2]))
```

Calls the `fox_SEC` function with command-line arguments for exponent and `isInt` flag if we want matrices with integers or float type number.
