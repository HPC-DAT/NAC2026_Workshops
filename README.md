# Interactive (geospatial) data analysis at HPC scales with RS-DAT and Python
Workshops at NAC 2026, Noordwijk, on 9th and 10th April 2026

## Introduction

This repository hosts the material for the workshops entitled "Interactive (geospatial) data analysis at HPC scales with RS-DAT and Python" taught at NAC 2026 in Noordwijk on 09-04-2026 and 10-04-2026 in the context of the HPC-DAT project funded by NWO through TDCC-NES. 

This workshop will acquaint participants with the use of the RS-DAT framework to deploy [Jupyter](https://docs.jupyter.org/en/latest/) on an HPC system, as well as with the fundamentals of the use of the [Dask](https://docs.dask.org/en/stable/index.html) and Xarray libraries in the Python ecosystem for geospatial analysis

The workshop will:

* Introduce the RS-DAT framework used to start Jupyter on a HPC system, with specific attention to SURF's systems
* Introduce how to connect to the dCache mass storage system at SURF
* Showcase a (basic) geospatial analysis workflow
* (Run through a short introduction to Dask and Xarray and discuss best practices)


The workshop will make use of the [Spider](https://doc.spider.surfsara.nl/en/latest/Pages/about.html) cluster, a high-throuput data processing platform hosted by [SURF](https://www.surf.nl/).

## Repository structure

* [`notebooks/`](./notebooks/) contains the Jupyter notebooks that implement the teaching material/use case(s).
* [`scripts/`](./scripts/) contains the batch job script to start a Jupyter session on Spider.
* [`.github/`](./github) contains the scripts that take care of building and publishing a container image with the required dependencies.
* [`environment.yml`](./environment.yml) is the environment file that define all the project dependencies.

<!--
## Data

The data used in this workshop is available on the Spider system in the following directory:
```
/project/remotesensing/Data/eo-summer-school/
```
The dataset is also published on Zenodo: [link](https://zenodo.org/records/17044819)

-->

## Setup
Given the limited time available, the workshop will focus on demonstrating usage and conveying relevant knowledge enabling participants to employ the framework later on their own.
Provided a participant has an existing account at SURF to use the SPIDER system, they can also choose to actively code/follow along.

In order to follow along with the instructor, you will need a laptop with the following software installed:

* OpenSSH client: should already be installed on macOS/Linux, it can be installed from Windows Apps on Windows 10+. Installation instructions can also be found [here](https://www.sshhandbook.com/installing-ssh/). Verify it works by typing the following command in a terminal window (it should return the OpenSSH version):
  ```shell
  ssh -V
  ```

* Python: Any recent Python version (3.10+) should work. It can be installed from [python.org](https://www.python.org/downloads/). Verify it works by typing the following command in a terminal window (it should return the Python version):
  ```shell
  python --version
  ```

Once this software is installed, follow the following setup steps:

1. Create a Python virtual environment. You can use any environment manager you are comfortable with (`venv`, `virtualenv`, `conda`, ...). Using `venv`, you can create the "myenv" environment with the following commands:
   ```shell
   python -m venv myenv
   source myenv/bin/activate
   ```

2. Install the Python tool hosted in [this repository](https://github.com/RS-DAT/JupyterDaskOnSLURM/tree/main/tools/jupyterdask):
   ```shell
   pip install -e "git+https://github.com/RS-DAT/JupyterDaskOnSLURM.git#egg=jupyterdask&subdirectory=tools/jupyterdask"
   jupyterdask --version  # check the command line tool is correctly installed
   ```

3. Download the following batch job script and save it to a known path (e.g. on your Desktop): [jupyterdask-spider.slurm](https://raw.githubusercontent.com/HPC-DAT/NAC2026_Workshops/main/scripts/jupyterdask-spider.slurm)

Note: Should you choose to clone this repository to your local system the script is located in the `/scripts` subdirectory.

## Run

Start the Jupyter session on Spider with the following command:

```shell
jupyterdask -i /path/to/ssh/key --template /path/to/jupyterdask-spider.slurm --run <YOUR_USERNAME>@spider.surf.nl
```

replacing the path to your ssh key (for SPIDER), the script, and your username (for SPIDER)