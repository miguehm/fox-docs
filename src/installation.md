# Installation

First, clone the [github repository](https://github.com/miguehm/fox-algorithm) :

```bash
git clone https://github.com/miguehm/fox-algorithm.git && cd fox-algorithm
```
or alternatively, download the zip file and extract it:

![](https://raw.githubusercontent.com/miguehm/fox-algorithm/graphsv2/media/zip_download.png) 

Then, install the dependencies:

```bash
pip install -r requirements.txt
```

You need to have MPI installed. If you are using Windows, you can [download the installer](https://www.microsoft.com/en-us/download/details.aspx?id=57467) from the microsoft official page. If you are using Linux, you don't need to install anything.

## Usage

In order to run the program you need to execute the following command:

Linux:
```bash
$ python3 src/main.py {n_processes} {n} {m}
```

Windows:
```bash
py src/main.py {n_processes} {n} {m} 
```

Where:
- **`n_processes`** is the number of processes that will be used to execute the algorithm.
- **`n`** is the exponent of the matrix size. The matrix size will be $2^n$.
- **`m`** is an optional parameter that indicates another exponent of the matrix size. The matrix size will be $2^m$.
- The program will execute the algorithm for all the matrix sizes $2^x\ \forall\ x \in [n, m]$.

> :warning: **WARNING:** The program will execute the algorithm for all the matrix sizes $2^x\ \forall\ x \in [n, m]$. For values of $n$ and $m$ greater than 11, the execution time will be very long. For example, for $n=11$ and $m=12$, the execution time will be approximately 1 hour. 

### Use Cases

> Linux python examples, for windows use `python`.

```bash
$ python3 src/main.py --help
```
<script async id="asciicast-SRMQaqkgUt89rChMdd07nG8m0" src="https://asciinema.org/a/SRMQaqkgUt89rChMdd07nG8m0.js"></script>
