# Checker

<!-- toc -->

This script loads matrices from files, checks the correctness of the result matrix obtained from the Fox algorithm by comparing it with the result of matrix multiplication using NumPy, and prints the result of the check. The check is based on the assumption that the matrices in the files represent the output of the Fox matrix multiplication algorithm generated previously via `main.py` execution.

# Load Matrices from Files

```python
matrix_A = np.loadtxt('results/matrix_A.data')
matrix_B = np.loadtxt('results/matrix_B.data')
matrix_C = np.loadtxt('results/matrix_C.data')
```
It loads three matrices, `matrix_A`, `matrix_B`, and `matrix_C`, from separate files. These matrices are assumed to be the result of some computation or algorithm, possibly the Fox matrix multiplication algorithm.

# Matrix Multiplication Check

```python
multiplication_check = (matrix_A @ matrix_B == matrix_C).all()
```
It checks the correctness of the result matrix (`matrix_C`) obtained from the Fox algorithm by comparing it with the result of matrix multiplication using NumPy. The expression `(matrix_A @ matrix_B == matrix_C)` performs element-wise equality comparison, and `.all()` checks if all elements are True.

# Print Result of Check

```python
print(multiplication_check)
```
It prints the result of the multiplication check, which is a boolean value. If the result is `True`, it means that the matrices obtained from the Fox algorithm and the NumPy matrix multiplication are equal, indicating the correctness of the Fox algorithm's result.
