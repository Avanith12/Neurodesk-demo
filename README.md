# Neurodesk + FSL Basic Project (Skull Stripping + Overlay)

This repository contains a beginner-friendly Jupyter Notebook that demonstrates a basic neuroimaging workflow using Neurodesk (Neurodesktop) and FSL on a BIDS-format dataset.

## What this notebook does
Using a T1-weighted (T1w) anatomical MRI scan, the notebook performs the following steps:
- Loads FSL inside Neurodesk
- Selects a T1w anatomical scan (example: sub-01, ses-test)
- Runs BET2 (Brain Extraction / Skull Stripping)
- Generates:
  - Brain-extracted image (*_brain.nii.gz)
  - Brain mask (*_mask.nii.gz)
- Exports quick visualizations as PNG slices
- Creates an overlay image (mask highlighted on top of the original T1 scan)

This project is meant to be a simple “getting started” workflow to understand how Neurodesk tools and datasets work.

## Environment requirement (Important)
This notebook is designed to run inside Neurodesk / Neurodesktop (Docker-based environment).

It will NOT run directly in Google Colab, because it depends on:
- the Neurodesk module loader: ml fsl/<version>
- FSL command-line tools such as: bet2, fslmaths, and slicer
...
##  Dataset Used

For this experiment, I used a public brain MRI dataset from **OpenNeuro**:

- **Dataset Name:** ds000114 (Finger Foot Lips)
- **Source:** OpenNeuro
- **Download Link:** https://openneuro.org/datasets/ds000114/versions/1.0.2/download

This dataset contains structural MRI (T1-weighted) brain scans in **BIDS format**, which were used to test FSL tools such as **BET2 (brain extraction)**, **FAST (tissue segmentation)**, and **FLIRT (registration)**.


Example input file used in the notebook:
sub-01/ses-test/anat/sub-01_ses-test_T1w.nii.gz

The dataset folder used in Neurodesk:
 /home/jovyan/neurodesktop-storage/test_neurodesk

## Output files (saved locally)
All outputs are saved to:
 /home/jovyan/fsl_out/

Example outputs generated:
- sub-01_T1w_brain.nii.gz
- sub-01_T1w_brain.nii.gz_mask.nii.gz
- brain_slices.png
- mask_slices.png
- T1_with_mask_overlay.nii.gz
- T1_with_mask_overlay.png

## How to run
1. Open Neurodesk / Neurodesktop
2. Open JupyterLab
3. Open the notebook: fsl_basic_project.ipynb
4. Run all cells from top to bottom

## Tools used
- Neurodesk / Neurodesktop
- FSL 6.0.7.4
- BET2 (bet2)
- fslmaths
- slicer

## Notes
- This notebook is intentionally lightweight and beginner-friendly.
- It also works in environments where GUI apps (like ITK-SNAP / FSLeyes) may not launch, since PNG outputs are exported directly using command-line tools.

Made by Avanith Kanamarlapudi


