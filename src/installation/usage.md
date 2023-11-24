# Usage

> **WARNING**: The program will execute the algorithm for all the matrix sizes \\(2^x\ \forall\ x \in [n, m]\\). For values of \\(n\\) and \\(m\\) greater than 11, the execution time will be very long. For example, for \\(n=11\\) and \\(m=12\\), the execution time will be approximately 1 hour. 

> `python3` is for linux/unix OS based, if you have windows use `python` instead.

<!-- toc -->

## Help

```bash
python3 src/main.py --help
```

Output

```bash
Usage: main.py [OPTIONS]                        
                                                 
╭─ Options ─────────────────────────────────────╮
│ --help          Show this message and exit.   │
╰───────────────────────────────────────────────╯
╭─ Matrix order range ──────────────────────────╮
│ --min-exp        INTEGER  Exponent of base 2  │
│                           matrix order (2^)   │
│                           [default: 6]        │
│ --max-exp        INTEGER  Exponent of base 2  │
│                           matrix order (2^)   │
│                           [default: 13]       │
╰───────────────────────────────────────────────╯
╭─ MPI options ─────────────────────────────────╮
│ --threads        INTEGER  Number of cores to  │
│                           use                 │
│                           [default: 4]        │
╰───────────────────────────────────────────────╯
```
## Default execution

```bash
python3 src/main.py
```

The execution will be done for the matrix of size \\(2^6\\) with 4 threads.

## Multiple matrix multiplication by range

```bash
python3 src/main.py --min-exp 6 --max-exp 13
```

The charts with the results will be created in the `charts` folder.

## Specify threads number

```bash
python3 src/main.py --threads 4
```

> You can find out the number of threads available on your computer using `top` command.
