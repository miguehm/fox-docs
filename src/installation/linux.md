# Linux Installation

For this installation we used:

- Arch Linux 2023.11.1 and Ubuntu 20.04 LTS
- Python 3.11.5
- pip 23.3.1

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
