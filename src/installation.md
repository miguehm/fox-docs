# Installation

<!-- toc -->

# How to Install

First, clone the [github repository](https://github.com/miguehm/fox-algorithm):

```bash
git clone https://github.com/miguehm/fox-algorithm.git && cd fox-algorithm
```
or alternatively, download the zip file and extract it:

![](https://raw.githubusercontent.com/miguehm/fox-algorithm/graphsv2/media/zip_download.png) 

Then, create a virtual environment

```bash
python3 -m venv venv
```

activate the virtual environment

```bash
source ./venv/bin/activate # for linux
```

and install requirements

```bash
pip install -r requirements.txt
```

You need to have MPI installed. If you are using Windows, you can [download the installer](https://www.microsoft.com/en-us/download/details.aspx?id=57467) from the microsoft official page. If you are using Linux, you don't need to install anything.

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

