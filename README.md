# Neurodesk + FSL Basic Project (Skull Stripping + Overlay)

This repository contains a beginner-friendly Jupyter Notebook that demonstrates a basic neuroimaging workflow using **Neurodesk** and **FSL**.

## ✅ What this notebook does
Using a BIDS-format dataset, the notebook performs:

- Loading **FSL** inside Neurodesk
- Selecting a **T1w anatomical MRI** scan (`sub-01`)
- Running **BET2** (Brain Extraction / Skull Stripping)
- Generating:
  - Brain-extracted image (`*_brain.nii.gz`)
  - Brain mask (`*_mask.nii.gz`)
- Exporting quick visualizations as PNG slices
- Creating an **overlay image** (mask highlighted on top of the original scan)

## 📂 Output files (saved locally)
Outputs are saved to:

