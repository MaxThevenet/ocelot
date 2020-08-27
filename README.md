Accelerator, radiation and x-ray optics simulation framework

# An Introduction to Ocelot

Ocelot is a multiphysics simulation toolkit designed for studying FEL and storage ring based light sources. Ocelot is written in Python. Its central concept is the writing of python's scripts for simulations with the usage of Ocelot's modules and functions and the standard Python libraries.

Ocelot includes following main modules:
* **Charged particle beam dynamics module (CPBD)**
    - optics
    - tracking
    - matching
    - collective effects (description can be found [here](http://accelconf.web.cern.ch/ipac2017/papers/wepab031.pdf) )
        - Space Charge (true 3D Laplace solver)
        - CSR (Coherent Synchrotron Radiation) (1D model with arbitrary number of dipoles) (under development).
        - Wakefields (Taylor expansion up to second order for arbitrary geometry).
    - MOGA (Multi Objective Genetics Algorithm). (under development but we have already applied it for a storage ring [application](http://accelconf.web.cern.ch/AccelConf/ipac2016/papers/thpmb034.pdf))
* **Native module for spontaneous radiation calculation**
* **FEL calculations: interface to GENESIS and pre/post-processing**
* **Modules for online beam control and online optimization of accelerator performances.** [Work1](http://accelconf.web.cern.ch/accelconf/IPAC2014/papers/mopro086.pdf), [work2](https://jacowfs.jlab.org/conf/y15/ipac15/prepress/TUPWA037.PDF), [work3](http://accelconf.web.cern.ch/AccelConf/ipac2016/papers/wepoy036.pdf), [work4](https://arxiv.org/pdf/1704.02335.pdf).

Ocelot extensively  uses Python's [NumPy (Numerical Python)](http://numpy.org) and [SciPy (Scientific Python)](http://scipy.org) libraries, which enable efficient in-core numerical and scientific computation within Python and give you access to various mathematical and optimization techniques and algorithms. To produce high quality figures Python's [matplotlib](http://matplotlib.org/index.html) library is used.

It is an open source project and it is being developed by physicists from  [The European XFEL](http://www.xfel.eu/), [DESY](http://www.desy.de/) (Germany), [NRC Kurchatov Institute](http://www.nrcki.ru/) (Russia).

We still have no documentation but you can find a lot of examples in ocelot/demos/


## Ocelot user profile

Ocelot is designed for researchers who want to have the flexibility that is given by high-level languages such as Matlab, Python (with Numpy and SciPy) or Mathematica.
However if someone needs a GUI  it can be developed using Python's libraries like a [PyQtGraph](http://www.pyqtgraph.org/) or [PyQt](http://pyqt.sourceforge.net/Docs/PyQt4/).

For example, you can see GUI for SASE optimization (uncomment and run next block)

## Tutorials
* Preliminaries: Setup & introduction
* Beam dynamics
* [Tutorial N1. Linear optics.](#tutorial1). [Web version](http://nbviewer.jupyter.org/github/iagapov/ocelot/blob/dev/demos/ipython_tutorials/1_introduction.ipynb).
    - Linear optics. Double Bend Achromat (DBA). Simple example of usage OCELOT functions to get periodic solution for a storage ring cell.
* [Tutorial N2. Tracking.](2_tracking.ipynb). [Web version](http://nbviewer.jupyter.org/github/iagapov/ocelot/blob/dev/demos/ipython_tutorials/2_tracking.ipynb).
    - Linear optics of the European XFEL Injector.
    - Tracking. First and second order.
* [Tutorial N3. Space Charge.](3_space_charge.ipynb). [Web version](http://nbviewer.jupyter.org/github/iagapov/ocelot/blob/dev/demos/ipython_tutorials/3_space_charge.ipynb).
    - Tracking through RF cavities with SC effects and RF focusing.
* [Tutorial N4. Wakefields.](4_wake.ipynb). [Web version](http://nbviewer.jupyter.org/github/iagapov/ocelot/blob/dev/demos/ipython_tutorials/4_wake.ipynb).
    - Tracking through corrugated structure (energy chirper) with Wakefields
* [Tutorial N5. CSR.](5_CSR.ipynb). [Web version](http://nbviewer.jupyter.org/github/iagapov/ocelot/blob/dev/demos/ipython_tutorials/5_CSR.ipynb).
    - Tracking trough bunch compressor with CSR effect.
* [Tutorial N6. RF Coupler Kick.](6_coupler_kick.ipynb). [Web version](http://nbviewer.jupyter.org/github/iagapov/ocelot/blob/dev/demos/ipython_tutorials/6_coupler_kick.ipynb).
    - Coupler Kick. Example of RF coupler kick influence on trajjectory and optics.
* [Tutorial N7. Lattice design.](7_lattice_design.ipynb). [Web version](http://nbviewer.jupyter.org/github/iagapov/ocelot/blob/dev/demos/ipython_tutorials/7_lattice_design.ipynb).
    - Lattice design, twiss matching, twiss backtracking

 ## Preliminaries

The tutorial includes 7 simple examples dediacted to beam dynamics and optics. However, you should have a basic understanding of Computer Programming terminologies. A basic understanding of Python language is a plus.

##### This tutorial requires the following packages:

- Python 3.4-3.6 (python 2.7 can work as well)
- `numpy` version 1.8 or later: http://www.numpy.org/
- `scipy` version 0.15 or later: http://www.scipy.org/
- `matplotlib` version 1.5 or later: http://matplotlib.org/
- `ipython` version 2.4 or later, with notebook support: http://ipython.org

**Optional** to speed up python
- numexpr (version 2.6.1)
- pyfftw (version 0.10)

The easiest way to get these is to download and install the (very large) [Anaconda software distribution](https://www.continuum.io/).

Alternatively, you can download and install [miniconda](http://conda.pydata.org/miniconda.html).
The following command will install all required packages:
```
$ conda install numpy scipy matplotlib ipython-notebook
```

##### Ocelot installation
1. you have to download from GitHub [zip file](https://github.com/iagapov/ocelot/archive/master.zip).
2. Unzip ocelot-master.zip to your working folder **/your_working_dir/**.
3. Rename folder **../your_working_dir/ocelot-master** to **/your_working_dir/ocelot**.
4. Add **../your_working_dir/** to PYTHONPATH
    - **Windows 7:** go to Control Panel -> System and Security -> System -> Advance System Settings -> Environment Variables.
    and in User variables add **/your_working_dir/** to PYTHONPATH. If variable PYTHONPATH does not exist, create it

    Variable name: PYTHONPATH

    Variable value: ../your_working_dir/
    - Linux:
    ```
    $ export PYTHONPATH=/your_working_dir/:$PYTHONPATH
    ```

#### To launch "ipython notebook" or "jupyter notebook"
in command line run following commands:

```
$ ipython notebook
```

or
```
$ ipython notebook --notebook-dir="path_to_your_directory"
```

or
```
$ jupyter notebook --notebook-dir="path_to_your_directory"
```
