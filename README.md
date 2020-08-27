# How to apply the Morphologist pipeline in Docker?

This page explain how to apply the Morphologist pipeline of the Brainvisa toolbox (www.brainvisa.info) in a Docker container.
It will allow you to apply the version of the pipeline based on deep learning described in the following article:

Borne L., Rivière D., Mancip M. and Mangin J.F., 2020. Automatic labeling of cortical sulci using patch-or CNN-based segmentation techniques combined with bottom-up geometric constraints. *Medical Image Analysis*

Note that this version is not available in the last Release (4.6.1.) of the BrainVISA toolbox.

The sulci nomenclature used is described [here](nomenclature.jpg), and its translation in english is [here](nomenclature_translation.pdf).

## Instructions

1. Install Docker (https://www.docker.com/) 
2. To apply the pipeline on a T1 MPRAGE MRI scan, run the following command (it should take around 10min):
```
sudo docker run -v <PATH>:<PATH>: leonieborne/morphologist-deepsulci:latest /bin/bash -c ". /home/brainvisa/build/bug_fix/bin/bv_env.sh /home/brainvisa/build/bug_fix && python ./morphologist.py -s <SUBJECT_NAME> -d <DATABASE_PATH> -m <T1MRI_PATH>"
```
* `<PATH>` is a directory in your computer where your T1 MPRAGE MRI scans are stored.
* `<SUBJECT>` is the subject name/ID that will be attributed to the MRI scan in the Brainvisa database.
* `<DATABASE_PATH>` is the directory to the Brainvisa database (already existing or not).
* `<T1MRI_SCAN>` it the path to the MRI scan. It should be a NII file (.nii or .nii.gz). You can use the [dcm2niix](https://github.com/rordenlab/dcm2niix) command to convert a DCM file to NII.

Note that `<DATABASE_PATH>` and `<T1MRI_PATH>` should be in `<PATH>`. For example:
```
sudo docker run -v /tmp:/tmp: leonieborne/morphologist-deepsulci:latest /bin/bash -c ". /home/brainvisa/build/bug_fix/bin/bv_env.sh /home/brainvisa/build/bug_fix && python ./morphologist.py -s me -d /tmp/brainvisa -m /tmp/LEONIE_BORNE.nii.gz"
```
3. You've succeeded, congratulations!

## Access sulcal morphometry measurements
If you are interested in knowing the sulcal width (or opening), the cortical thickness, the length, the depth, etc. of each sulcus, you should search for the following CSV file in the `<DATABASE_PATH>`:
```
<DATABASE_PATH>/subjects/<SUBJECT>/t1mri/default_analysis/folds/3.1/default_session_auto/<SUBJECT>_default_session_auto_sulcal_morphometry.csv
```
