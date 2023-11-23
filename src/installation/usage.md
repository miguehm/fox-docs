# Usage

> **WARNING**: The program will execute the algorithm for all the matrix sizes \\(2^x\ \forall\ x \in [n, m]\\). For values of \\(n\\) and \\(m\\) greater than 11, the execution time will be very long. For example, for \\(n=11\\) and \\(m=12\\), the execution time will be approximately 1 hour. 

## Help

```bash
python3 src/main.py --help
```

## Multiple matrix multiplication

```bash
python3 src/main.py --min-exp 6 --max-exp 13
```

## Specify threads number

```bash
python3 src/main.py --threads 4
```

