# Neurodesk + FSL Basic Project (Skull Stripping + Overlay)

This repository contains a beginner-friendly Jupyter Notebook that demonstrates a basic neuroimaging workflow using **Neurodesk** and **FSL**.

##  What this notebook does
Using a BIDS-format dataset, the notebook performs:

- Loading **FSL** inside Neurodesk
- Selecting a **T1w anatomical MRI** scan (`sub-01`)
- Running **BET2** (Brain Extraction / Skull Stripping)
- Generating:
  - Brain-extracted image (`*_brain.nii.gz`)
  - Brain mask (`*_mask.nii.gz`)
- Exporting quick visualizations as PNG slices
- Creating an **overlay image** (mask highlighted on top of the original scan)

##  Output files (saved locally)
Outputs are saved to:


Example outputs:
- `sub-01_T1w_brain.nii.gz`
- `sub-01_T1w_brain.nii.gz_mask.nii.gz`
- `brain_slices.png`
- `mask_slices.png`
- `T1_with_mask_overlay.png`

##  How to run
1. Open Neurodesk
2. Launch JupyterLab
3. Open the notebook:
   - `fsl_basic_project.ipynb`
4. Run cells in order from top to bottom

## 🛠 Tools used
- **Neurodesk**
- **FSL 6.0.7.4**
- BET2 (`bet2`)
- Image math (`fslmaths`)
- Slice export (`slicer`)

##  Notes
This notebook is designed as a **lightweight beginner experiment** that works even in a headless environment (no GUI), by exporting PNG images directly from the terminal tools.

---
Made by Avanith Kanamarlapudi
