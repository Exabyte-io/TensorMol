# &#9658;<img src="doc/images/TensorMol.png" width="400">
![](doc/images/newtitle.png)
-Title signature by Alex Graves' handwriting LSTM https://arxiv.org/abs/1308.0850

[![PyPI version](https://badge.fury.io/py/TensorMol.svg)](https://badge.fury.io/py/TensorMol)
![](https://img.shields.io/badge/Python-2.7-brightgreen.svg)
![](https://img.shields.io/badge/Python-3.6-brightgreen.svg)
[![Documentation Status](https://readthedocs.org/projects/tensormol/badge/?version=latest)](http://tensormol.readthedocs.io/en/latest/?badge=latest)


## Authors:
 Kun Yao (kyao@nd.edu), John Herr (jherr1@nd.edu),
 David Toth (dtoth1@nd.edu), Ryker McIntyre(rmcinty3@nd.edu), Nicolas Casetti,
 [John Parkhill](http://blogs.nd.edu/parkhillgroup) (john.parkhill@gmail.com)

## Model Chemistries:
 - Behler-Parrinello with electrostatics
 - Many Body Expansion
 - Bonds in Molecules NN
 - Atomwise Forces
 - Inductive Charges

## Simulation Types:
 - Optimizations
 - Molecular Dynamics (NVE,NVT Nose-Hoover)
 - Monte Carlo
 - Open/Periodic Boundary Conditions
 - Meta-Dynamics
 - Infrared spectra by propagation
 - Infrared spectra by Harmonic Approximation.
 - Nudged Elastic Band
 - Path integral simulations via interface with [I-PI](https://github.com/i-pi/i-pi) MD engine.

## News: 
 This fork of TensorMol is being maintained by [Team Exabyte](exabyte.io). Check back 
 periodically for new features and other improvements!

## License: GPLv3
By using this software you agree to the terms in COPYING

## Installation:

Works on OSX, Ubuntu, and Windows subsystem for Linux.

1. Install [PyEnv](https://github.com/pyenv/pyenv#installation)

2. If you are installing on **Python 2** (not recommended, as Python 2 is no longer maintained),
   ensure you have a version of 2.7 available via PyEnv by:

    ```bash
    pyenv install 2.7.18
    ```

    Likewise, if you plan to install on **Python 3**  (recommended):

    ```bash
   pyenv install 3.6.12
    ```

    You can verify the installation occurred `pyenv versions` to print a list of available Python versions.

2. Create a fresh virtual environment for your chosen Python version. If you are running **Python 2**:

    ```bash
   pyenv virtualenv 2.7.18 .tensormol_env
    ```
   
    Likewise, for **Python 3**:

    ```bash
    pyenv virtualenv 3.6.12 .tensormol_env
    ```
   
    You can call these environments whatever you like, we just choose `.tensormol_env` as the name for the
    purposes of this tutorial
   
2. Activate your PyEnv environment:

    ```bash
   pyenv activate .tensormol_env
    ```

   TensorMol will be installed only to this environment, so whenever you want to run TensorMol,
   you should run this command. To exit the environment, you can always  run `pyenv deactivate`.
   
3. Clone repository:
    
    ```bash
    git clone git@github.com:Exabyte-io/TensorMol.git    
    ```

    or, if SSH connectivity with GitHub is not set up, use HTTPS:

    ```bash

    git clone https://github.com/Exabyte-io/TensorMol.git    

    ```

4. Complete the Installation

    Older versions of `pip` (the canonical Python package manager) will have trouble installing the `grpcio`
    package, which is a dependency of TensorMol. Make sure your version of `pip` is up to date:

    ```bash
   pip install --upgrade pip 
   ```
    Enter the TensorMol directory:

    ```bash
    cd TensorMol

   ```
   
    Pip install TensorMol:
    ```bash
    pip install -e .
   ```



5. Test the installation:

    ```bash
    cd samples
    python test.py
    ```

## Demo of training a neural network force field using TensorMol:
 - Copy the training script into the tensormol folder:```cp samples/training_sample.py  .``` Run the script: ```python training_sample.py ``` This will train a network force field for water.  

## Test example for TensorMol01:
 - Download our pretrained neural networks (network.tar.gz). [Networks for water and molecules that only contains C, H, O, N](https://drive.google.com/drive/folders/1IfWPs7i5kfmErIRyuhGv95dSVtNFo0e_?usp=sharing) (The file is about 6 Gigabyte. This may take a while)
 - Copy the zipped trained networks file (network.tar.gz) into TensorMol folder. Unzip it. The networks should be in './networks' folder.
 - Copy the test script into the tensormol folder:```cp samples/test_tensormol01.py .``` Run the script: ```python test_tensormol01.py``` The test sample contains geometry optimization, molecular dynamic, harmonic IR spectrum and realtime IR spectrum.  

## Timing Information
TensorMol is robust and fast. You can get an BP+electrostatic energy and force of this monstrous cube of 24,000 atoms
in less than 100 seconds on a 2015 MacbookPro (Core i7 2.5Ghz, 16GB mem). Periodic simulations are about 3x
more expensive.  

<img src="doc/images/monster.png" width="400">
<img src="doc/images/Timings.png" width="400">
<img src="doc/images/PeriodicTimings.png" width="400">

## Usage:
 - ```import TensorMol as tm```
 - We are working on /doc/Tutorials, but it's sparse now. We've done a lot of re-writing, and so if you are looking for good examples, look for /samples files with recent commits.
 - A collection of tests are located in samples/test_tensormol01.py but this requires first downloading the trained networks from the Arxiv paper.
 - `python samples/test_tensormol01.py`
 - IPI interface: start server: ~/i-pi/i-pi samples/i-pi_interface/H2O_cluster.xml > log &; run client: python test_ipi.py


## Sample Results

### Biological molecules
Because Neural network force fields do not rely on any specific atom typing or bond topology, the agony of setting up  simulations of biological molecules is greatly reduced. This gif is a periodic optimization of PDB structure 2EVQ, in explicit polarizable TensorMol solvent.

<img src="doc/images/2evq.gif" width="300">

### Chemical Reactions
Converged nudged elastic band simulations of the cyclization cascade of endiandric acid C (c.f. K. C. Nicolaou, N. A. Petasis, R. E. Zipkin, 1982, The endiandric acid cascade. Electrocyclizations in organic synthesis. 4. Biomimetic approach to endiandric acids A-G. Total synthesis and thermal studies, J. Am. Chem. Soc. 104(20):5560–5562).

<img src="doc/images/cascade.gif" width="300">

This reaction path can be found in a few minutes on an ordinary laptop. Relaxation from the linearly interpolated guess looks like this:

<img src="doc/images/neb.png" width="300">

The associated energy surface is shown below.

<img src="doc/images/pes.png" width="300">

### Dynamic Properties
- Tyrosine Harmonic IR spectrum

<img src="doc/images/tyrosine.png" width="300">

## Publications and Press:
 - John E. Herr, Kun Yao, David W. Toth, Ryker Mcintyre, John Parkhill.Metadynamics for Training Neural Network Model Chemistries: a Competitive Assessment. [Arxiv](https://arxiv.org/abs/1712.07240)
- Kun Yao, John E. Herr, David W. Toth, Ryker Mcintyre, John Parkhill. The TensorMol-0.1 Model Chemistry: a Neural Network Augmented with Long-Range Physics. [Chemical Science](http://pubs.rsc.org/en/content/articlelanding/2014/SC/C7SC04934J#!divAbstract)
 - Writeup in [Chemistry World](https://www.chemistryworld.com/news/neural-network-predicts-bond-energies-like-a-pro/3007598.article)
 - Kun Yao, John E. Herr, Seth N. Brown, & John Parkhill. Intrinsic Bond Energies from a Bonds-in-Molecules Neural Network. Journal of Physical Chemistry Letters (2017). DOI: [10.1021/acs.jpclett.7b01072](http://pubs.acs.org/doi/abs/10.1021/acs.jpclett.7b01072)
 - Kun Yao, John Herr, & John Parkhill. The Many-body Expansion Combined with Neural Networks. Journal of Chemical Physics (2016). DOI:  [10.1063/1.4973380](http://aip.scitation.org/doi/abs/10.1063/1.4973380?journalCode=jcp)
 - Kun Yao, John Parkhill. The Kinetic Energy of Hydrocarbons as a Function of Electron Density and  Convolutional Neural Networks. Journal of Chemical Theory and Computation (2016). DOI: [10.1021/acs.jctc.5b01011](http://pubs.acs.org/doi/abs/10.1021/acs.jctc.5b01011)

## Requirements:
- Minimum Pre-Requisites: Python2.7x, TensorFlow  ```sudo pip install tensorflow ```
- Also now works in Python3.6.    
- Useful Pre-Requisites: CUDA7.5, PySCF
- To Train Minimally: ~100GB Disk 20GB memory
- To Train Realistically: 1TB Disk, GTX1070++
- To Evaluate: Normal CPU and 10GB Mem

## Acknowledgements:
 - Google Inc. (for TensorFlow)
 - NVidia Corp. (hardware)
 - von Lilienfeld Group (for GBD9)
 - Chan Group (for PySCF)

## Common Issues:
- nan during training due to bad checkpoints in /networks (clean.sh)
- Also crashes when reviving networks from disk.
- if you have these issues try re-installing or:

```
sh clean.sh
```
