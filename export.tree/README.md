# BAD: Bilingual Adaptations Dataset

This repository contains structural and functional MRI data of 127 monolingual and bilingual participants with varying language backgrounds and proficiencies.

This README is organized into two sections:

1. [**Usage**](#usage) describes how one can go about recreating data derivatives and brain measures from start to finish.
2. [**Directories**](#directories) gives information on the file structure of the dataset.

If you just want access to the processed brain and language data, go to [Quick Start](#quick-start).

# Usage
There are two ways that one can go about this dataset. If you want to jump immediately into analyzing participants and their language profiles, then go to [Quick Start](#quick-start). If instead you are looking to go from low-level MRI data to cleaned CSVs with various brain measure types, either to learn the process or double check our work, then go to [Data Replication](#data-replication).

## Quick Start
If you just want access to cleaned brain measure and language history data of 127 participants, they can be found in the following folders:

-  **Brain Data:** [analysis/bilingual_structures/data/main_analyses](analysis/bilingual_structures/data/main_analyses)
- **Language Data:** [analysis/bilingual_structures/data/participant_data](analysis/bilingual_structures/data/participant_data)

Each folder has a metadata.xlsx file that gives more information on the files and their fields. Have fun, go nuts.

## Data Replication

If you are looking to go through the steps required to create the data from start to finish, we first start with the raw structural and functional MRI data, which can be found in **./sub-EBE{XXXX}**. Information on the data in this folder, which follows BIDS, can be found [here](https://bids-specification.readthedocs.io/en/stable/appendices/entity-table.html).

The data in **./sub-EBE{XXXX}** is then inputted into various processing pipelines, the versions for which can be found at [Dependency versions](#dependency-versions). The following processing pipelines are used:

- ### fMRIprep
    fMRIprep is a neuroimaging procesing tool used for task-based and resting-state fMRI data. fMRIprep is not used directly to create brain measure CSVs used in analysis, but instead creates processed fMRI data used in the [CONN toolbox](#3-conn). For more information on fMRIprep and how to use it, click [here](https://fmriprep.org/en/stable/).

- ### CAT12
    We use the CAT12 toolbox, which stands for Computational Anatomy Toolbox, to calculate brain region volumes using voxel-based morphometry [(VBM)](https://en.wikipedia.org/wiki/Voxel-based_morphometry). CAT12 works through SPM12 and Matlab, and requires that both be [installed](#dependency-versions). We have included the Matlab scripts used to create the files in ./derivatives/CAT12 in [analysis/processing_scripts/pre_processing/cat12](analysis/processing_scripts/pre_processing/cat12). To use it, install necessary dependencies [(CAT12, SPM12, and Matlab)](#dependency-versions) and run [analysis/processing_scripts/pre_processing/cat12/CAT12_segmentation_n2.m](analysis/processing_scripts/pre_processing/cat12/CAT12_segmentation_n2.m) in Matlab. You will also need to update for your local path to Matlab on lines 12, 24, and 41. For more information on CAT12 and how to use it to calculate brain region volumes using VBM, click [here](https://neuro-jena.github.io/cat12-help/).

- ### CONN
    CONN is a functional connectivity toolbox, which we used to generate participant brain connectivity measures. CONN requires first that you run the [fMRIprep pipeline](#1-fmriprep), as it uses some of fMRIprep's outputs as input. Like CAT12, CONN works through SPM12 and Matlab and requires that both be [installed](#dependency-versions). For more information on CONN and how to use it, click [here](https://web.conn-toolbox.org/resources/conn-documentation).

- ### FDT
    We used FMRIB's Diffusion Toolbox (FDT) for extracting values from diffusion weighted images. For more information on FDT and how to use it, click [here](https://fsl.fmrib.ox.ac.uk/fsl/docs/#/diffusion/index).

- ### Freesurfer
    FreeSurfer is a software package for the analysis and visualization of structural and functional neuroimaging data, which we use to extract region volumes and cortical thickness through surface-based morphometry [(SBM)](https://en.citizendium.org/wiki/Surface-based_morphometry). For more information on Freesurfer and how to use it, click [here]((https://surfer.nmr.mgh.harvard.edu/fswiki)).

<br>

The results from these pipelines, which use the data in **./sub-EBE{XXXX}** as input, are then outputted into folders in **./derivatives**. For information on which folder stores each pipeline result, see [Directories](#directories).

After running these pipelines, we can take their outputs and convert them into CSVs for analysis. To do this, we use [analysis/post_processing/mri_postprocessing/brain_data_preprocessing.ipynb](analysis/post_processing/mri_postprocessing/brain_data_preprocessing.ipynb). This Python notebook takes the data in ./derivatives as input and outputs CSVs to [analysis/bilingual_structures/data/main_analyses](analysis/bilingual_structures/data/main_analyses). Outputted from this notebook are CSVs containing brain volumes, cortical thicknesses, fractional anisotropy values, and connectivity measures. Information on the outputted CSVs can be found at [analysis/bilingual_structures/data/main_analyses/metadata.xlsx](analysis/bilingual_structures/data/main_analyses/metadata.xlsx).

### Dependency versions

1. [MATLAB v. R2023a](https://www.mathworks.com/products/new_products/release2023a.html)
2. [SPM12](https://www.fil.ion.ucl.ac.uk/spm/software/spm12/)
3. [CAT12 v8.2](https://neuro-jena.github.io/cat/index.html#DOWNLOAD)
4. [CONN v22a](https://web.conn-toolbox.org/)
5. [FSL v6.0.2](https://fsl.fmrib.ox.ac.uk/fsl/docs/#/diffusion/index)
6. [Freesurfer v7.4.1](https://surfer.nmr.mgh.harvard.edu/fswiki/DownloadAndInstall)
7. [fMRIprep v23.0.2](https://fmriprep.org/en/stable/index.html) 

## Chen, Salvadore, & Blanco-Elorrieta Paper Replication

Also included in this dataset is code used in the analyses of Chen, Salvaore, & Blanco-Elorrieta (submitted). If you are interested in running analyses used in that paper, see the README in [analysis/bilingual_structures/code](analysis/bilingual_structures/README.md).

<br>

# Directories

- ## sub-EBE{XXXX}
    Each of these directories contain the BIDS formatted anatomical and functional MRI data, with the name of the directory corresponding to the subject's unique identifier. For more information on the subfolders, see BIDS information [here](https://bids-specification.readthedocs.io/en/stable/appendices/entity-table.html).

- ## derivatives
    This directory contains outputs of common processing pipelines run on the raw MRI data from **./sub-EBE{XXXX}**.

    - ### CAT12
        Results of the [CAT12 toolbox](#cat12), which stands for Computational Anatomy Toolbox, and is used to calculate brain region volumes using voxel-based morphometry (VBM).

    - ### conn
        Results of the [CONN toolbox](#conn), used to generate data on functional connectivity from brain fMRI sequences.

    - ### fdt
        Results of the [FMRIB's Diffusion Toolbox (FDT)](#fdt), used for extracting values from diffusion weighted images.

    - ### fMRIprep
        Results from [fMRIprep](#fmriprep), a preprocessing pipeline for task-based and resting-state functional MRI data.

    - ### freesurfer
        Results from [FreeSurfer](#freesurfer), a software package for the analysis and visualization of structural and functional neuroimaging data.

- ## analysis

    - ### bilingual_structures
        Data and code used in the analysis of Chen, Salvadore, & Blanco-Elorrieta (submitted).

        - ### code
            This directory contains python and R code used in the analysis of Chen, Salvadore, Blanco-Elorrieta (submitted), with each python notebook corresponding to a different part of the paper's analysis. For more details on each file and subdirectories, see the folder's README.md.
        - ### data
            - #### participant_data
                This directory contains language data on each subject, including a composite multilingualism score from Chen & Blanco-Elorrieta (submitted), information on language knowledge, exposure, mixing, use in education, and family members’ language ability in the participants’ known languages from early childhood to the present day. For more information on the files and their fields, see the folder's metadata.xlsx.
            - #### main_analyses
                This directory contains MRI data, both anatomical and functional, that is the final result of processing raw MRI data. This includes brain volumes, cortical thickness, fractional anisotropy values, and connectivity measures. For more information on the files within this directory, see the folder's metadata.xlsx.
            - #### deluca_replication
                Data used in the replication of analyses from DeLuca et al. 2019 and DeLuca et al. 2024.

    - ### processing_scripts
        Code involved in processing raw MRI data.
        - ### brain_data_preprocessing.ipynb
            Python notebook used to create CSVs with brain measure values used in analyses. For more information on the code and how to use it, read [Data Replication](#data-replication). 
        - ### pre_processing
            Scripts used to create files some files in **./derviatives** folder from raw MRI data in **./sub-EBE{XXXX}**. For more information on the scripts, read [Data Replication](#data-replication).  
        -  ### toolbox_outputs
            Intermediary files created and used by [analysis/processing_scripts/brain_data_preprocessing.ipynb](analysis/processing_scripts/brain_data_preprocessing.ipynb).
            

            

