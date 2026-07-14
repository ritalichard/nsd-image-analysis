# NSD Image Analysis

This project studies whether natural-versus-synthetic stimulus information can be decoded from reduced fMRI response space and whether CNN image features can predict neural principal components. The workflow combines data preparation, PCA/factor analysis, supervised decoding, and image-to-neural encoding.

The analysis was developed for CSE 599N: Machine Learning for Neuroscience at the University of Washington.

## Highlights

- Builds memory-conscious trial-by-voxel matrices from NSD and NSD-Synthetic fMRI volumes.
- Reduces neural responses with PCA and compares their low-dimensional structure.
- Compares logistic regression and a multilayer perceptron for natural-versus-synthetic decoding.
- Extracts ResNet-18 image features and compares linear, ridge, and MLP encoders for predicting neural principal components.
- Finds that regularized linear models are strong baselines in this single-subject, class-imbalanced setting.

## Repository contents

```text
notebooks/
  01_data.ipynb        Data preparation and train/test construction
  02_pca.ipynb         PCA and factor-analysis exploration
  03_classifier.ipynb  Neural-response decoding experiments
  04_cnn.ipynb         CNN feature extraction and neural encoding
report/
  CSE_599_Project.pdf  Final project report
  source/              LaTeX source, bibliography, and generated figures
environment.yml        Conda environment specification
```

## Data access and redistribution

The Natural Scenes Dataset (NSD), NSD-Synthetic data, stimulus images, and generated data arrays are **not included** in this repository. NSD access requires accepting the dataset's Data Sharing and Usage Agreement, which prohibits redistributing the dataset or its components.

Request access and review the current terms at the [Natural Scenes Dataset website](https://naturalscenesdataset.org/). Store authorized local files under `data/` and `img/`; these paths and generated outputs are excluded from version control.

The notebooks expect the following local structure when run from the `notebooks/` directory:

```text
data/subj01/
  betas_nsdsynthetic.nii.gz
  betas_session01.nii.gz
  betas_session02.nii.gz
  betas_session03.nii.gz
  valid_nsdsynthetic.nii.gz
  valid_session01.nii.gz
  valid_session02.nii.gz
  valid_session03.nii.gz
  nsdsynthetic_expdesign.mat
  nsd_expdesign.mat
img/
  nat/
  syn/
outputs/processed/
```

## Environment

Create the Conda environment:

```bash
conda env create -f environment.yml
conda activate cse599n-nsd
```

Launch Jupyter from the repository root, open the `notebooks/` directory, and run the notebooks in numeric order. The workflow is computationally and memory intensive because the masked fMRI matrices contain hundreds of thousands of voxel features per trial.

## NSD references

- Allen, E. J., et al. (2022). *A massive 7T fMRI dataset to bridge cognitive neuroscience and artificial intelligence*. Nature Neuroscience, 25, 116-126. [https://doi.org/10.1038/s41593-021-00962-x](https://doi.org/10.1038/s41593-021-00962-x)
- Gifford, A. T., Cichy, R. M., Naselaris, T., & Kay, K. (2026). *A 7T fMRI dataset of synthetic images for out-of-distribution modeling of vision*. Nature Communications, 17, 1589. [https://doi.org/10.1038/s41467-026-69345-9](https://doi.org/10.1038/s41467-026-69345-9)

Additional methodological references are included in `report/source/references.bib`.

## Scope and limitations

This repository provides research code and a reproducible workflow, but not the licensed source data or large derived arrays. The reported experiments are primarily single-subject, use imbalanced natural and synthetic conditions, and were constrained by available compute and memory.

