# Installation

The assignments require [Julia](https://julialang.org) and Python 3 to be installed (Python 2 will not work).

For Windows, I recommend to use docker as [Devito](https://www.devitoproject.org) does not support Windows.

## Julia

To install julia follow

[https://julialang.org/downloads/](https://julialang.org/downloads/)

And install Julia 1.5

## Python

The recommended installation is via conda to have a stable environment.

[https://conda.io/miniconda.html](https://conda.io/miniconda.html)


## Packages

For the assignments, you will need a few python and julia packages. Please follow these instructions to install all of the packages in the order described here.

First, install Devito using `pip` (or `pip3`), or see the [Devito's GitHub page](https://github.com/devitocodes/devito) for installation with Conda and further information. The current release of [JUDI](https://github.com/slimgroup/JUDI.jl) requires Python 3 and the current Devito version. Run all of the following commands from the (bash) terminal command line (not in the Julia REPL):

```bash
pip install --user git+https://github.com/devitocodes/devito.git
```

Then install matplotlib by

```bash
pip install matplotlib
```

If these commands don't work, please replace `pip` by `pip3` and try it again.

For reading and writing seismic SEG-Y data, JUDI uses the [SegyIO](https://github.com/slimgroup/SegyIO.jl) package and matrix-free linear operators are based the [Julia Operator LIbrary](https://github.com/slimgroup/JOLI.jl/tree/master/src) (JOLI), we can install these 2 packages via:

```bash
julia -e 'using Pkg; Pkg.add(url="https://github.com/slimgroup/SegyIO.jl.git")'
julia -e 'using Pkg; Pkg.add(url="https://github.com/slimgroup/JOLI.jl.git")'
```

Once Devito, SegyIO and JOLI are installed, you can install [JUDI](https://github.com/slimgroup/JUDI.jl) with Julia's `Pkg.add`.

```bash
julia -e 'using Pkg; Pkg.add(url="https://github.com/slimgroup/JUDI.jl")'
```

Once you have JUDI installed, you need to point Julia's PyCall package to the Python version for which we previously installed Devito. To do this, copy-paste the following commands into the (bash) terminal:

```bash
export PYTHON=$(which python)
julia -e 'using Pkg; Pkg.build("PyCall")'
```

Again, try `which python3` if `which python` does not work.

You can verify your installation by running:

```bash
julia -e 'using Pkg; using JUDI; example=joinpath(dirname(pathof(JUDI)),"..","examples/scripts/modeling_basic_2D.jl");include(example);'
```

This command should finish without errors.


## Docker (not necessary for homework but important for project)

Docker is a platform which builds a virtual machine/container for you in case some softwares above cannot be installed/processed in the environment on your local machine. Thus, we suggest you first try to install the softwares above and do the programming exercises on your local machine. The exercises should work well in apple/linux machines. If it renders problems on your machine (especially a windows one), you could install docker and follow the steps below to run julia sessions in a virtual environment.

First install docker for your system

[https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop)

Instead of having to install Python, Julia, Devito, JUDI and all the dependencies by yourself, you simply download the docker image and run it in a container. All you need to do is install docker and run:

```
docker run -p 8888:8888 philippwitte/judi:v1.1
```

This will download the image and launch a jupyter notebook that you can access from your internet browser. The command will display a link, which looks something like this:

```
Copy/paste this URL into your browser when you connect for the first time,
    to login with a token:
        http://0e27b13128d4:8888/?token=84a95cf4319e8e68534f20c7c6474d9875f13c70270f35f4&token=84a95cf4319e8e68534f20c7c6474d9875f13c70270f35f4
```

Copy-paste this link and replace the address `0e27b13128d4:8888` with `localhost:8888` (the link is created inside the docker container, which doesn't know that you mapped this port to your localhost w/ port no. 8888). Instead of a notebook, you can also launch an interactive session with a terminal by running:

```
docker run -it philippwitte/judi:v1.1 /bin/bash
```

This will give you access to a terminal, in which you can start Julia/Python, run things interactively or modify code. However, figures from PyPlot sometimes do not render well from interactive julia sessions. Therefore, jupyter notebooks on docker are recommended.

## Exercises

During the course you will work on the following exercises

1. A first look at seismic data. [Intro to julia](Assignments/introduction_to_julia.md) [Exercise 1](Assignments/Exercise1.md) (Due: 11AM Feb 3, 2021)
2. NMO correction and velocity analysis. [Exercise 2](Assignments/Exercise2.md) (Due: 11AM Feb 10, 2021)
3. Wavefield extrapolation and migration. [Exercise 3](Assignments/Exercise3.md) (Due: 11AM Feb 17, 2021)
4. Fourier, Radon and filtering. [Exercise 4](Assignments/Exercise4.md) (Due Date: 11AM Mar 15, 2021)
5. From processing to inversion I. [Exercise 5](Assignments/Exercise5.md) (Due Date: April 5,2020) 
6. From processing to inversion II. [Exercise 6](Assignments/Exercise6.md) (Due Date: April 19,2020)
7. Seismic imaging (mini-project). [Exercise 7](Assignments/Exercise7.md)

<!--
1. A first look at seismic data. [Intro to julia](Assignments/introduction_to_julia.md) [Exercise 1](Assignments/Exercise1.md) [[Solution]](https://www.slim.eos.ubc.ca/Teaching/EOSC454/exercise1_sol.html)

2. NMO correction and velocity analysis [Exercise 2](Assignments/Exercise2.md)

3. Wavefield extrapolation and migration. [Exercise 3](Assignments/Exercise3.md)

4. Fourier, Radon and filtering.[Exercise 4](Assignments/Exercise4.md)

5. From processing to inversion I.[Exercise 5](Assignments/Exercise5.md)

6. From processing to inversion II. [Exercise 6](Assignments/Exercise6.md)

7. Full Waveform inversion. [Exercise 7](Assignments/Exercise7.md)

These exercises will introduce you to the [Julia programming language](https://julialang.org), [Devito](https://www.devitoproject.org)-a Domain-specific Language (DSL) for automatic code generation for highly optimized finite differences, and [Judi](https://github.com/slimgroup/JUDI.jl)-a framework for large-scale seismic modeling and inversion and designed to enable rapid translations of algorithms to fast and efficient code that scales to industry-size problems.

-->

### Hand in

Please turn in your assignments as pdf files. The assignments should be send to [Ziyi (Francis) Yin](mailto:ziyi.yin@gatech.edu). Late hand ins are not accepted.

**Unless stated otherwise the labs are due one week after the assignments have been posted. For example, if a homework is posted before the lecture on Wednesday, you should submit your homework before the lecture on the next Wednesday in order for your homework to be considered as on-time. If you have difficulty on the homework and want to ask for extension, please email Dr. Felix Herrmann and cc TA in advance.**

### Feedback

We will give you feedback on the marking of the exercises.
