Welcome to the Gnosis research center tutorial wiki!
===================================

This repo is a brief tutorial on various HPC technologies useful to our research. The
[wiki](https://github.com/scs-lab/scs-tutorial/wiki) contains the
step-by-step details on how to interpret this repo and follow along.

## The SCS_TUTORIAL environment variable
For making experiments easier to setup, set the SCS_TUTORIAL environment
variable to the location of the scs-tutorial github on your machine.
```bash
export SCS_TUTORIAL=[/path/to/scs-tutorial]
```
.. note::

    If you don't know what an environment variable is, read section 1.

Contents
--------
.. toctree::
    :caption: Old content
   old/old-usage

.. toctree::
   :caption: Intro to Linux
   linux/Linux-introduction

.. toctree::
   :caption: Installing Software
   installing/installing-HPC-Software

.. toctree::
   :caption: Intro to C++
   cpp/3.1.CPP-Hello-World
   cpp/3.2.Building-CPP-Manually
   cpp/3.3-Building-CPP-With-CMake
   cpp/3.4.Basic-CPP-Syntax
   cpp/3.5.CPP-Classes
   cpp/3.6.CPP-Standard-Library
   cpp/3.7.CPP-Templates
   cpp/3.8.Singleton-Design-Pattern
   cpp/3.9.-Factory-Design-Pattern
   cpp/3.10.Unit-Testing
   cpp/3.11.CPP-Style-Guide
   cpp/3.12.CLion-IDE

.. toctree::
   :caption: Intro to git
   git/4.1.Github
   git/4.2.Git-Basics
   git/4.3.Github-Actions
   git/4.4.Code-Coverage

.. toctree::
   :caption: Intro to Docker
   docker/5.1.Docker-Basics
   docker/5.2.Docker-Clusters

.. toctree::
   :caption: Intro to MPI
   mpi/6.1.MPI-Intro
.. toctree::
   :caption: IIT resources
   iit/7.Reimbursement
