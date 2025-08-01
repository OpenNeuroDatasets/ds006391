# Chen, Salvadore, & Blanco-Elorrieta (submitted)

This directory contains code used in the paper's analysis and data pre-processing.

This README is organized into two sections:

1. [**Usage**](#usage) describes how one can go about running the analyses used in Chen, Salvadore, & Blanco-Elorrieta (submitted).
2. [**Directories**](#directories) gives information on the file structure of the dataset.


## Usage

Before running python notebooks, install the packages from requirements.txt using "pip install -r requirements.txt". After that, one can simply go through each of the python notebooks in the **figures/** folder and rerun all analyses. It is suggested that you run the notebooks while going through the paper.

## Directories

### code
This directory contains python and R code used in the analysis of Chen, Salvadore, Blanco-Elorrieta (submitted), with each python notebook corresponding to a different part of the paper's analysis.

- ### figures
    Scripts used for the analysis in Chen, Salvadore, & Blanco-Elorrieta (submitted), their outputs, and utility files necessary in the analyses.

    - #### preprocessing.py
        Contains functions used in every script for preprocessing brain measure data.
    - #### figure_1.ipynb
        Generating the results from figure 1. This notebook is divided in two:
        1. **ROI report** – CSV identifying significant brain regions after running Ordinary Least Squares analyses
        2. **Brain Visualizations** – The brain volume visualizations used in figure 1 
    - #### figure_1_dti.ipynb
        Generating brain visualizations for the DTI section of figure 1.
    - #### figure_2a.ipynb
        Generating the results from figure 2A. This section is divided in two:
        1. **Heatmap visualization** – Recreates the heatmap visualization in figure 2A.
        2. **Internal Consistency Analysis** – Calculates the internal consistency analysis results featured in the paper.
    - #### figure_2b.ipynb
        Generating the results from figure 2B. Divided into two sections:
        1. **K-Means Visualizations** – Recreates the scatterplots and decision boundaries of K-means analysis in figure 2B.
        2. **Analysis** – Generates the table from figure 2B with information on K-means adjusted rand scores and SVM accuracy on different language groups. Comes in the form of a DataFrame.
    - #### figure_3a.ipynb
        Generating the results from figure 3A, which is the replication of Deluca et al. (2019).
    - #### figure_3b.r
        Generating the results from figure 3A, which is the replication of Deluca et al. (2024). In order to best replicate DeLuca (2024), replication is performed in R as is done in DeLuca (2024).

    - #### output
        Directory for outputting analyses and visualizations.

        - #### regions_of_interest.csv
            All significant brain regions, regardless of language filtering or bilingual overlap, identified in figure_1.ipynb

        - #### Brain Visualizations
            Brain visualizations found in figure 1 of Chen, Salvadore, & Blanco-Elorrieta (submitted).

            The first level directory is the measure used (VBM, SBM, or DTI), the second level is the predictor used in the OLS (binary or continuous), and each subdirectory at the final level corresponds to a step in the filtering process.

- ### utils
    Utility files necessary in many functions throughout analysis and visualizations.

- ### requirements.txt
    The python libraries and their versions used in the code.

### data
- #### participant_data
    This directory contains language data on each subject, including a composite multilingualism score from Chen & Blanco-Elorrieta (submitted), information on language knowledge, exposure, mixing, use in education, and family members’ language ability in the participants’ known languages from early childhood to the present day. For more information on the files and their fields, see the folder's metadata.xlsx.
- #### main_analyses
    This directory contains MRI data, both anatomical and functional, that is the final result of processing raw MRI data. This includes brain volumes, cortical thickness, fractional anisotropy values, and connectivity measures. For more information on the files within this directory, see the folder's metadata.xlsx.
- #### deluca_replication
    Data used in the replication of analyses from DeLuca et al. 2019 and DeLuca et al. 2024.







