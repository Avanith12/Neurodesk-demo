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

# Running the Workflow in Terminal

## Step 1: Navigate to the dataset directory

cd /home/jovyan/neurodesktop-storage/test_neurodesk
pwd

Expected output:

/home/jovyan/neurodesktop-storage/test_neurodesk

---

## Step 2: Load FSL

ml fsl/6.0.7.4

Verify installation:

which bet2

Expected output:

/neurodesktop-storage/containers/fsl_6.0.7.4_20231005/bet2

---

## Step 3: Check BET2 help

bet2 -h | head -n 5

Example output:

BET (Brain Extraction Tool) v2.1 - FMRIB Analysis Group, Oxford

Usage:
bet2 <input_fileroot> <output_fileroot> [options]

---

## Step 4: Define input and output paths

T1=./sub-01/ses-test/anat/sub-01_ses-test_T1w.nii.gz
OUT=/home/jovyan/fsl_out

mkdir -p $OUT

echo "T1 = $T1"
echo "OUT = $OUT"

Expected output:

T1 = ./sub-01/ses-test/anat/sub-01_ses-test_T1w.nii.gz
OUT = /home/jovyan/fsl_out

---

## Step 5: Run Skull Stripping

bet2 $T1 $OUT/sub-01_T1w_brain.nii.gz -m -f 0.5

This removes the skull from the MRI scan.

Parameters used:

-m  → generate brain mask  
-f 0.5 → fractional intensity threshold  

Output files created:

sub-01_T1w_brain.nii.gz  
sub-01_T1w_brain.nii.gz_mask.nii.gz  

---

## Step 6: Export brain slices as PNG

slicer $OUT/sub-01_T1w_brain.nii.gz -a $OUT/brain_slices.png

Output:

brain_slices.png

---

## Step 7: Export mask slices

slicer $OUT/sub-01_T1w_brain.nii.gz_mask.nii.gz -a $OUT/mask_slices.png

Output:

mask_slices.png

---

## Step 8: Make mask brighter

fslmaths $OUT/sub-01_T1w_brain.nii.gz_mask.nii.gz -mul 2000 $OUT/mask_highlight.nii.gz

Output file:

mask_highlight.nii.gz

---

## Step 9: Overlay mask on original MRI

fslmaths $T1 -add $OUT/mask_highlight.nii.gz $OUT/T1_with_mask_overlay.nii.gz

Output file:

T1_with_mask_overlay.nii.gz

---

## Step 10: Export overlay visualization

slicer $OUT/T1_with_mask_overlay.nii.gz -a $OUT/T1_with_mask_overlay.png

Output:

T1_with_mask_overlay.png

---

## Step 11: Check generated files

ls -lh $OUT

Expected output files:

sub-01_T1w_brain.nii.gz  
sub-01_T1w_brain.nii.gz_mask.nii.gz  
brain_slices.png  
mask_slices.png  
mask_highlight.nii.gz  
T1_with_mask_overlay.nii.gz  
T1_with_mask_overlay.png  

---

# Summary

This workflow demonstrates a simple neuroimaging pipeline using Neurodesk and FSL.

Steps performed:

1. Load FSL inside Neurodesk
2. Run BET2 for brain extraction
3. Generate a brain mask
4. Export visualization slices
5. Create overlay images













Made by Avanith Kanamarlapudi

