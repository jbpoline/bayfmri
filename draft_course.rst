##############################
Neuroimaging foundation course
##############################

Draft schedule

Introduction to neuroimaging ideas with working code.

Developing into analysis stream for full FMRI dataset.

Some introduction to working practice, mainly through example:

* Version control
* Testing
* +- github
* IPython notebooks (when to use and when not to use)

Reading images
Writing images
Format issues (nifti, DICOM)
Visualization (images and timeseries)
DICOM conversion
Quality control / diagnostics
Slice timing correction
(Dealing with bad data points)
Realignment with runs
Realignment across runs
Coregistration within subject across modality
(Distortion correction)
Spatial normalization (matching between subjects)
Diagnostics again
(Smoothing)
(Adjusting for global scaling)
Statistical modeling with the GLM
Modeling within run
Modeling across runs within subject
Modeling across subjects
Mixed effects models (combining within and across subjects)
Asking questions of a GLM with contrast matrices
Inference / multiple comparison correction
Family wise error and false discovery rate
Permutation / non-parametric inference
Region of interest analysis
(Machine learning)

*************
Getting ready
*************

Require:

* python
* numpy
* scipy
* matplotlib
* ipython notebook (>=0.13.1)
* sympy
* nibabel
* pydicom
* nipy

*****
Day 1
*****

Read a 3D image as a numpy array
Show image slices with matplotlib

Read a 4D image as a numpy array
Show image slices with matplotlib
Get and plot timeseries

Load affine from Nifti file
Find 0, 0, 0 (real space) voxel
(Visualize image with non-trivial affine)
(Show registration of two images with non-trivial affine)
(Futz with affine to improve registration)

Plot the timeseries for that voxel using matplotlib

Finding information in the nifti header
(e.g. get slice, frequency, phase)

Writing a 3D image
Set negative voxels to zero?
Set background voxels to zero?
Set NaN or Inf voxels to zero?
Applying a binary mask to an image?
Doing math on images (+ - / *) (covered by mean, std etc below?)

Reading image data from a DICOM image
Getting information from the DICOM header
DIOCM formats - Siemens, Philips

Basic diagnostics

* mean image
* standard deviation image
* min / max images
* global signal plots
* time series differences a la tsdiffana
* Detecting some common artifacts (RF, slice dropout - with examples)
* (automated spike detection?)
* PCA plots / images with nipy?

Slice timing correction

* Extract timeseries from first slice and middle slice
* Plot on same plot
* Time-series interpolation (NN, linear, spline, sinc) and resampling
* Some nasty timeseries (spikes) (and what happens with different
  interpolations)

Realignment

* On 2D slices
* The idea of a cost function
* The idea of 2D resampling
* Trying different transformations to reduce the cost function (combining cost
  function and resampling)
* Finding a best X translation
* Finding a best X and a best Y translation
* The idea of the local minimum
* Extrapolating to 3D
* Using the best images for realignment
  * Mean image to time point images for within-run
  * Mean image to mean image between runs

Distortion correction

* (the problem at least)

Order of steps

* Problem of slice timing and realignment
* Problem of distortion correction relative to both

Spatial normalization

* Visualizing native space (what is 0, 0, 0)
* Compare native space between brains
* Find the central sulcus, calcarine sulcus, Heschl's gyrus) on two brains
* (Freesurfer surface here?  PySurfer?)
* The idea of MNI space
* The MNI templates
* (?The Juelich cytoarchitecture data?)
* How best to match our two subject's brains?
* How best to match the brains to the MNI template?
* (Purpose of normalization)
* Cost functions for normalization
* Methods of normalization (shape matching, matching sulci)
* An affine normalization in nipy (find the best parameters for cost-function,
  optimization method)
* (?Lesions and cost-functions?)

Diagnostics

Getting ready for the statistical analysis
PCA with nipy again
(is there still movement artifact?)
(is there still slice-timing artifact?)

Statistics part I: Modelling and testing one voxel / one region

A) First recall simple linear regression
an example with simple regression and independant noise
* fitting the model : finding the model's parameters 
* Noise : properties of the noise - what is a good versus a bad fit ?
* Testing the parameters: t-test, F-test

B) Correlated noise : first level analyses  

Going from neural events to BOLD responses
Several experimental conditions: multiple regression 
    - modeling one run with two or three conditions
    - nuisance variable (eg mvt parameters)
    - event related models : one hrf
    - event related : several basis functions - F-test testing

C) Second level analyses:  
    - Modelling factors and interactions, associated contrast and t or F tests
    - Mixed effects analyses: within and between factors

Statistics part II: multiple comparison issues

Family wise error concept: correcting for the number of tests
detection at the voxel level, at the cluster level
Techniques for correction : GRF and Permutation 
False discovery rate correction: sensibility and specificity 

Other analyses

- machine learning
- connectivity
- ...


*********
Questions
*********

What should we use for volumetric visualization?

* A crummy matplotlib viewer (we have a few lying around)
* Eleftherios' fancy new viewer?  (need to review) (probably needs Qt / PySide)
* fslview
* SPM :)
