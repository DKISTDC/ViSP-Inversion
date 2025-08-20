# DKIST Level 2 pipeline for inversion of ViSP data

## 1 Identify invertible data sets:

[Thunderbolts](https://thunderbolts.dev.dkistdc.nso.edu/proposals)


## 2 Pre-processing pipeline and tools

The pre-processing pipeline is contained in the file *ViSP_inversion.py*,
aided by tools in the *ViSP_tools.py* package.

### 2.1 Steps in the pre-processing pipeline include:

+ Specification of data sets to be inverted together, up to three arms.
+ Verification and analysis of the assiciated .asdf files.
+ Alignment of the datasets, scaling based on ViSP hairlines. Data are
   scaled to common spatial scace relative to a specified fiducial arm.
   Shifts between arms, including those due to differential refraction
   are corrected.
+ Wavelength calibration, based on initial guess of the dispersion,
   and position of the deepest line in the spectral range.
+ Determination of cosine of the heliocentric viewing angle, \mu
+ Calibration of intensities based on Atlas, heliocentric angle and
   theoretical center-to-limb behavior.
+ Rebin of data to achieve as close as possible "square pixels",
   determined by number of pixels along the slit relative to the slit width.
+ Adhoc removal of polarization cross-talk.
+ Determination of the spectral broadening by comparison with Atlas
   profiles at the corresponding \mu value.
+ Writing the data, one file per arm, in format for DeSIRe inversions
+ Write auxiliary files for wavelength grid and spectral PSF.

### 2.2 Fits files with theoretical line shape data as function of mu

The *Aux_data* directory holds fits file with calculated line shape profiles 
as a function of 100 mu values. This is used to estimate the pseudo continuum
in cases where the observed wavelength grid does not reach the actual continuum 
e.g., in the case of Ca II 854.2), and to aid in the estimate of the spectral PSF.

### 2.3 Setting up the Python environment

The ViSP preprocessing pipeline relies on tools in the
[dkist tools package](https://docs.dkist.nso.edu/projects/python-tools/en/latest/installation.html),
as supported by the DKIST data center. 

Here is a list of additional packages to install for the ViSP pre-processing pipeline. 
assume you have one of the anaconda variants installed for your package management.

+ conda create -n dkist python=3.11
+ conda activate dkist
+ pip install .

This will automatically set up and configure the necessary python packages, including numpy, pandas, dkist, etc. It will also automatically include https://github.com/dkistdc/RH/python/rhanalyze

You may also want to install the jupyter package, to make plots, run tests.

+ conda install -c conda-forge jupyter

## 3.0 Inversions with DeSIRe

### 3.1 Installing the DeSIRe inversion code

File *desire-v5.06.tgz* contains the DeSIRe inversion code. To install unpack the tar file and run *make FC=gfortran install*
in the src directory.

### 3.2 Python wrapper for parallel processing in DeSIRe

The file *parallel_master.tgz* contains python code to execute DeSIRe in parrallel. Unpack the tar file and compile the included DeSIRe code.


+ Apr 10,  2025 
