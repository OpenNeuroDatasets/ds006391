# README

This repository contains raw MRI data of 127 subjects with varying language backgrounds and proficiencies. Below is a detailed outline of the file structure used:

<br>

# sub-EBE****
Each of these directories contain the BIDS formatted anatomical and functional MRI data, with the name of the directory corresponding to the subject's unique identifier.

For more information on the subdirectories, see BIDS information at https://bids-specification.readthedocs.io/en/stable/appendices/entity-table.html

<br>

# derivatives
This directory contains outputs of common processing pipelines run on the raw MRI data from "data/sub-EBE****".

## derivatives/CAT12
These are the results of the CAT12 toolbox, which stands for Computational Anatomy Toolbox, and is used to calculate brain region volumes using voxel-based morphometry (VBM). A few things are required to download for this process.

1. MATLAB v. R2023a (https://www.mathworks.com/products/new_products/release2023a.html)
2. SPM (https://www.fil.ion.ucl.ac.uk/spm/software/spm12/)
3. CAT12 (https://neuro-jena.github.io/cat/index.html#DOWNLOAD)


## derivatives/conn
CONN is used to generate data on functional connectivity from brain fMRI sequences. A few things are required to download for this process.

1. MATLAB v. R2023a (https://www.mathworks.com/products/new_products/release2023a.html)
2. SPM (https://www.fil.ion.ucl.ac.uk/spm/software/spm12/)
3. CAT12 (https://neuro-jena.github.io/cat/index.html#DOWNLOAD)
4. Conn – MATLAB toolbox for functional connectivity (https://web.conn-toolbox.org/)


## derivatives/fdt
We used FMRIB's Diffusion Toolbox (FDT) for extracting values from diffusion weighted images. To use FDT, you need to download the following modules through CLI:

1. module load fsl/6.0.2
2. module load freesurfer/7.4.1

For more information on the toolbox, visit https://fsl.fmrib.ox.ac.uk/fsl/docs/#/diffusion/index.


## derivatives/fMRIprep
fMRIprep is the preprocessing of task-based and resting-state functional MRI. We use it to generate data for connectivity.

We used fMRIprep v23.0.2. For more information, visit https://fmriprep.org/en/stable/index.html.

## derivatives/freesurfer
FreeSurfer is a software package for the analysis and visualization of structural and functional neuroimaging data, which we use to extract region volumes through surface-based morphometry (SBM).

We used freesurfer v7.4.1. For more information, visit https://surfer.nmr.mgh.harvard.edu/fswiki.


<br><br>

# analysis/
This directory contains data and code used in the analysis of Chen, Salvadore, Blanco-Elorrieta (submitted).

## analysis/code
This directory contains python and R code used in the analysis of Chen, Salvadore, Blanco-Elorrieta (submitted), with each python notebook corresponding to a different part of the paper's analysis. For more details on each file and subdirectories, see "analysis/code/README.md".
## analysis/participant_data
This directory contains language data on each subject, including a composite multilingualism score from Chen & Blanco-Elorrieta (submitted), information on language knowledge, exposure, mixing, use in education, and family members’ language ability in the participants’ known languages from early childhood to the present day. For more information on the files and their fields, see "analysis/participant_data/metadata.xlsx".
## analysis/processed_mri_data
This directory contains MRI data, both anatomical and functional, that is the final result of processing raw MRI data. This includes brain volumes, cortical thickness, fractional anisotropy values, and connectivity measures. For more information on the files within this directory, see "analysis/processed_mri_data/metadata.xlsx".

