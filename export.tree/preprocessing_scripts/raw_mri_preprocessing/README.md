# Chen, Salvadore, & Blanco-Elorrieta (submitted)

Scripts used to create files some files in **./derviatives** folder from raw MRI data in **./sub-EBE{XXXX}**.

## Directories

### cat12
This directory contains MATLAB code used for the preprocessing and extraction of VBM volume measures from the CAT12 toolbox.

To use, one should download necessary dependencies specified in the dataset's main README, then run CAT12_segmentation.m in MATLAB.

### fdt
This directory contains bash and python code used for the preprocessing of diffusion-weighted MR data using the FDT toolbox. To replicate the exact preprocessing steps and analyses, the scripts should be ran in the following order for each participant.

- ### fdt_preprocess_topup.sh
    This script takes the raw DWI data and runs topup for the b=0 volumes. Skull strip was done with the more recent mri_synthstrip function in freesurfer.

- ### fdt_preprocess_eddy.sh
    This script takes the outputs from the above topup script and runs the eddy current correction and fitting diffusion tensors. It outputs maps of the three eigenvalues and eigenvectors of the diffusion tensor as well as the mean diffusivity (MD) and fractional anistropy (FA) for each voxel.
    
- ### wmparc_to_dwi.sh
    This script takes the wmparc parcellation from the freesurfer output and transform the parcellation into the native space of the DWI data. 
