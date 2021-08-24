# If a Python interpreter is specified, then creates a virtualenv from it
# PYTHON := /usr/bin/python3.7
PYTHON := 
# The python version installed in the conda setup
PYTHON_VERSION := 3.7
CUDA_VERSION := 10.2
PYTORCH_VERSION := 1.6.0

# Both Miniconda2/3 can install any Python versions
CONDA_URL := https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
# PyTorch>=1.0.0 requires gcc>=4.9 when buliding the extensions
GCC_VERSION := $(shell gcc -dumpversion)

CONDA_PYTORCH := pytorch=$(PYTORCH_VERSION) cudatoolkit=$(CUDA_VERSION)
CUDA_DEPS := cupy.done

# Path to save tools (default: current directory)
TOOL :=
ifeq ($(strip $(TOOL)),)
	TOOL := $(PWD)/
endif
CONDA=$(TOOL)/miniconda

.PHONY: all clean

all: miniconda.done python
python: kaggle_env.done

# miniconda
miniconda.done:
	mkdir -p $(TOOL)
	if [ -e $(CONDA) ]; then rm -rf $(CONDA); fi
	test -f $(TOOL)/miniconda.sh || wget $(CONDA_URL) -O $(TOOL)/miniconda.sh
	test -d $(CONDA) || bash $(TOOL)/miniconda.sh -b -p $(CONDA)
	. $(CONDA)/bin/activate && conda config --show
	. $(CONDA)/bin/activate && conda update -y conda
	. $(CONDA)/bin/activate && conda install -y python=$(PYTHON_VERSION)
	. $(CONDA)/bin/activate && conda install -y pip setuptools
	. $(CONDA)/bin/activate && conda info -a
	touch miniconda.done

# python (including upgrade check)
kaggle_env.done:
	. $(CONDA)/bin/activate; python --version
	. $(CONDA)/bin/activate; pip list
	. $(CONDA)/bin/activate; pip install pip --upgrade
	. $(CONDA)/bin/activate; pip install numpy --upgrade
	. $(CONDA)/bin/activate; pip install torch==$(PYTORCH_VERSION)
	. $(CONDA)/bin/activate; pip install -e ..  # setup.py
	. $(CONDA)/bin/activate && conda install -y $(CONDA_PYTORCH) -c pytorch
	. $(CONDA)/bin/activate; pip list
	touch kaggle_env.done