# Analysis from Chen, Salvadore, & Blanco-Elorrieta (submitted)

This directory contains code used in the paper's analysis and data pre-processing. To run the paper's analysis, install the packages from requirements.txt using "pip install -r requirements.txt" and start runnning from script "figures/figure_1.ipynb".

Below is a description of the directory's file structure:

## figures/
Scripts used for the analysis in Chen, Salvadore, & Blanco-Elorrieta (submitted). Information regarding the files can be found below.

### figures/output
Directory for outputting analyses and visualizations.

#### figures/output/regions_of_interest.csv
All significant brain regions, regardless of language filtering or bilingual overlap, identified in figure_1.ipynb

#### figures/output/Brain Visualizations
Brain visualizations found in figure 1 of Chen, Salvadore, & Blanco-Elorrieta (submitted).

The first level directory is the measure used (VBM, SBM, or DTI), the second level is the predictor used in the OLS (binary or continuous), and each subdirectory at the final level corresponds to a step in the filtering process.

<br>

### figures/preprocessing.py
Contains functions used in every script for preprocessing brain measure data.
### figures/figure_1.ipynb
Generating the results from figure 1. This section is divided in two:
1. **ROI report** – CSV identifying significant brain regions after running Ordinary Least Squares analyses
2. **Brain Visualizations** – The brain volume visualizations used in figure 1.
### figures/figure_1_dti.ipynb
Generating brain visualizations for the DTI section of figure 1.
### figures/figure_2a.ipynb
Generating the results from figure 2A. This section is divided in two:
1. **Heatmap visualization** – Recreates the heatmap visualization in figure 2A.
2. **Internal Consistency Analysis** – Calculates the internal consistency analysis results featured in the paper.
### figures/figure_2b.ipynb
Generating the results from figure 2B. Divided into two sections:
1. **K-Means Visualizations** – Recreates the scatterplots and decision boundaries of K-means analysis in figure 2B.
2. **Analysis** – Generates the table from figure 2B with information on K-means adjusted rand scores and SVM accuracy on different language groups. Comes in the form of a DataFrame.
### figures/figure_3a.ipynb
Generating the results from figure 3A, which is the replication of Deluca et al. (2019).
### figures/figure_3b.r
Generating the results from figure 3A, which is the replication of Deluca et al. (2024). In order to best replicate DeLuca (2024), replication is performed in R as is done in DeLuca (2024).

<br>

## mri_preprocessing/

### mri_preprocessing/brain_data_preprocessing.ipynb
Generating csv files from the toolbox outputs for further statistical analyses. The resulting csv files have rows for each subject and columns for each brain measure. The generated csv files are saved in ../processed_mri_data.

### mri_preprocessing/fdt_tbss/
Customized scripts and commands for running fdt preprocessing and tbss for DTI analyses.


<br>

## utils/
Utility files necessary in many functions throughout analysis and visualizations.






