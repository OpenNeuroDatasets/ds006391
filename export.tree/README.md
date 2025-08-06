# MIND: Multilingual Imaging Neuro Dataset

This repository contains structural and functional MRI data of 126 monolingual and bilingual participants with varying language backgrounds and proficiencies.

This README is organized into two sections:

1. [**Usage**](#usage) describes how one can go about recreating data derivatives and brain measures from start to finish.
2. [**Directories**](#directories) gives information on the file structure of the dataset.

If you just want access to the processed brain and language data, go to [Quick Start](#quick-start).

# Usage
There are two ways that one can go about this dataset. If you want to jump immediately into analyzing participants and their language profiles, then go to [Quick Start](#quick-start). If instead you are looking to go from low-level MRI data to cleaned CSVs with various brain measure types, either to learn the process or double check our work, then go to [Data Replication](#data-replication).

## Quick Start
If you just want access to cleaned brain measure and language history data of 126 participants, they can be found in the following folders:

-  **Brain Data:** [processing_output](processing_output)
- **Language Data:** [language_background](language_background)

Each folder has a metadata.xlsx file that gives more information on the files and their fields. Have fun, go nuts.

## Data Replication

If you are looking to go through the steps required to create the data from start to finish, we first start with the raw structural and functional MRI data, which can be found in **./sub-EBE{XXXX}**. Information on the data in this folder, which follows BIDS, can be found [here](https://bids-specification.readthedocs.io/en/stable/appendices/entity-table.html).

The data in **./sub-EBE{XXXX}** is then inputted into various processing pipelines, the versions for which can be found at [Dependency versions](#dependency-versions). The following processing pipelines are used:

- ### fMRIprep
    fMRIprep is a neuroimaging procesing tool used for task-based and resting-state fMRI data. fMRIprep is not used directly to create brain measure CSVs used in analysis, but instead creates processed fMRI data used in the [CONN toolbox](#3-conn). For more information on fMRIprep and how to use it, click [here](https://fmriprep.org/en/stable/).

- ### CAT12
    We use the CAT12 toolbox, which stands for Computational Anatomy Toolbox, to calculate brain region volumes using voxel-based morphometry [(VBM)](https://en.wikipedia.org/wiki/Voxel-based_morphometry). CAT12 works through SPM12 and Matlab, and requires that both be [installed](#dependency-versions). We have included the Matlab scripts used to create the files in ./derivatives/CAT12 in [preprocessing_scripts/cat12](preprocessing_scripts/cat12). To use it, install necessary dependencies [(CAT12, SPM12, and Matlab)](#dependency-versions) and run [preprocessing_scripts/cat12/CAT12_segmentation_n2.m](preprocessing_scripts/cat12/CAT12_segmentation_n2.m) in Matlab. You will also need to update for your local path to Matlab on lines 12, 24, and 41. For more information on CAT12 and how to use it to calculate brain region volumes using VBM, click [here](https://neuro-jena.github.io/cat12-help/).

- ### CONN
    CONN is a functional connectivity toolbox, which we used to generate participant brain connectivity measures. CONN requires first that you run the [fMRIprep pipeline](#1-fmriprep), as it uses some of fMRIprep's outputs as input. Like CAT12, CONN works through SPM12 and Matlab and requires that both be [installed](#dependency-versions). For more information on CONN and how to use it, click [here](https://web.conn-toolbox.org/resources/conn-documentation).

- ### FDT
    We used FMRIB's Diffusion Toolbox (FDT) for extracting values from diffusion weighted images. For more information on FDT and how to use it, click [here](https://fsl.fmrib.ox.ac.uk/fsl/docs/#/diffusion/index).

- ### Freesurfer
    FreeSurfer is a software package for the analysis and visualization of structural and functional neuroimaging data, which we use to extract region volumes and cortical thickness through surface-based morphometry [(SBM)](https://en.citizendium.org/wiki/Surface-based_morphometry). For more information on Freesurfer and how to use it, click [here]((https://surfer.nmr.mgh.harvard.edu/fswiki)).

<br>

The results from these pipelines, which use the data in **./sub-EBE{XXXX}** as input, are then outputted into folders in **./derivatives**. For information on which folder stores each pipeline result, see [Directories](#directories).

After running these pipelines, we can take their outputs and convert them into CSVs for analysis. To do this, we use [preprocessing_scripts/brain_data_preprocessing.ipynb](preprocessing_scripts/brain_data_preprocessing.ipynb). This Python notebook takes the data in ./derivatives as input and outputs CSVs to [processing_output](processing_output). Outputted from this notebook are CSVs containing brain volumes, cortical thicknesses, fractional anisotropy values, and connectivity measures. Information on the outputted CSVs can be found at [processing_output/metadata.xlsx](processing_output/metadata.xlsx).

### Dependency versions

1. [MATLAB v. R2023a](https://www.mathworks.com/products/new_products/release2023a.html)
2. [SPM12](https://www.fil.ion.ucl.ac.uk/spm/software/spm12/)
3. [CAT12 v8.2](https://neuro-jena.github.io/cat/index.html#DOWNLOAD)
4. [CONN v22a](https://web.conn-toolbox.org/)
5. [FSL v6.0.2](https://fsl.fmrib.ox.ac.uk/fsl/docs/#/diffusion/index)
6. [Freesurfer v7.4.1](https://surfer.nmr.mgh.harvard.edu/fswiki/DownloadAndInstall)
7. [fMRIprep v23.0.2](https://fmriprep.org/en/stable/index.html) 

## Chen, Salvadore, & Blanco-Elorrieta Paper Replication

Also included in this dataset is code used in the analyses of Chen, Salvaore, & Blanco-Elorrieta (submitted). If you are interested in running analyses used in that paper, see the README in [chen_salvadore_elorrieta/code](chen_salvadore_elorrieta/README.md).

<br>

# Directories

-	**participants.tsv:** Subject demographic information.
-	**participants.json:** Describes *participants.tsv*.

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

- ## language_background
    Participant information is kept on the first level of the dataset and includes information on language history, demographics, and their composite multilingualism score. Below is a list of all participant information files.

    -	**language_background.csv:** Full subject language information and history.

    -	**metadata.xlsx:** Metadata on each file in this directory.

    -	**multilingual_measure.csv:** Each participant’s composite multilingualism score specified in Chen & Blanco-Elorrieta (in review).
    

- ## processing_output
    This directory contains processed brain measure data for brain volumes, cortical thickness, FA, and connectivity. The CSVs are created from scripts in the directory processing_scripts using files in the derivatives directory as input. Descriptions of each file can be found below.

    -	**connectivity_network.csv:** Contains 36 Network-to-Network connectivity values for each participant.

    -	**connectivity_roi.csv:** Contains 13,336 ROI-to-ROI connectivity values for each participant.

    -	**dti.csv:** Contains averaged white matter FA values for 76 brain regions for each participant based on Diffusion tensor imaging.

    -	**metadata.xlsx:** Metadata on each file in this directory.

    -	**sbm_thickness.csv:** Contains cortical thickness values for 68 brain regions for each participant based on Surface-based morphometry.

    -	**sbm_volume.csv:** Contains volume values for 165 brain regions for each participant based on Surface-based morphometry.

    -	**tiv.csv:** Contains two total intracranial volumes for each subject, calculated using SBM and VBM respectively

    -	**vbm_volume.csv:** Contains volume values for 153 brain regions for each participant based on Voxel-based morphometry.
`

- ## preprocessing_scripts
    Code involved in processing raw MRI data.
    - **brain_data_preprocessing.ipynb**
        Python notebook used to create CSVs with brain measure values used in analyses. For more information on the code and how to use it, read [Data Replication](#data-replication). 
    - ### raw_mri_preprocessing
        Scripts used to create files some files in **./derviatives** folder from raw MRI data in **./sub-EBE{XXXX}**. For more information on the scripts, read [Data Replication](#data-replication).  
    -  ### toolbox_outputs
        Intermediary files created and used by [analysis/processing_scripts/brain_data_preprocessing.ipynb](analysis/processing_scripts/brain_data_preprocessing.ipynb).

- ## chen_salvadore_elorrieta
    This dataset was originally created for analyses in the paper Chen, Salvadore, Blanco-Elorrieta (submitted), which is an investigation into bilingualism-specific neural adaptations. To ensure reproducibility and to provide users with options for methodology, we have included the code and data used in the analyses of this paper. This directory is organized into two sub-directories, code and data.

    - ### code
        This directory contains python and R code used in the paper, with each python notebook corresponding to a different part of the paper's analysis. For usage instructions, see the directory’s README.

    - ### data
        The directory data contains CSV files which were created to ease analyses. In most cases, they are derivations of data from contents of the directory processing_output. Descriptions of each file can be found below. 
        -	**participant_group_info.csv:** Fields used for participant lingualism grouping in the analysis of Chen, Salvadore, Blanco-Elorrieta

        -	**deluca_2019_replication.csv:** CSV containing participant language history and brain measure data relevant to replicating the methodology from DeLuca et al. 2019.

        -	**deluca_2024_replication.csv:** CSV containing participant language history and brain measure data relevant to replicating the methodology from DeLuca et al. 2024.

        - ### tbss:
            Directory containing data and scripts used to recreate DeLuca et al.’s tract-based spatial-statistic analysis. For information on how to use these scripts, see the directory’s README.
 




            

            

