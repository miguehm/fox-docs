# Windows installation

For this installation we used:

- Windows 11 Nov 2023 update
- Python 3.11.5
- pip 23.3.1


> You need to have MPI installed, you can [download the installer](https://www.microsoft.com/en-us/download/details.aspx?id=57467) from the microsoft official page.

First, clone the [github repository](https://github.com/miguehm/fox-algorithm):

```bash
git clone https://github.com/miguehm/fox-algorithm.git && cd fox-algorithm
```
or alternatively, download the zip file and extract it:

![](https://raw.githubusercontent.com/miguehm/fox-algorithm/graphsv2/media/zip_download.png) 

Then, create a virtual environment

```bash
python -m venv venv
```

activate the virtual environment

```bash
.\venv\Scripts\Activate
```

and install requirements

```bash
pip install -r requirements.txt
```
