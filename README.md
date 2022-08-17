# DAKIdoc

This is repository containing the documentation for the DAKI-FWS's project (https://www.hhi.fraunhofer.de/en/departments/ai/projects/daki-fws.html)

This documentation is written using [Jupyter Book](https://jupyterbook.org/intro.html).

## Installation

Get source from GitHub:
```
$ git clone https://github.com/FREVA-CLINT/DAKIdoc
$ cd DAKIdoc
```

Create conda environment:
```
$ conda env create -f environment.yml
$ conda activate DAKIdoc
```

## Build docs

Build HTML pages locally:
```
$ jupyter-book build book
```

Open generated docs in firefox:
```
$ firefox book/_build/html/index.html
```
