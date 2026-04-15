<div align="center">

# 🌍 DEM Generation from InSAR Using Sentinel-1 & ESA SNAP

### *Interferometric Synthetic Aperture Radar (InSAR)-Based Terrain Reconstruction Workflow*

![Platform](https://img.shields.io/badge/Platform-Sentinel--1-blue?style=for-the-badge)
![Software](https://img.shields.io/badge/Software-ESA%20SNAP-green?style=for-the-badge)
![Tool](https://img.shields.io/badge/Phase%20Unwrapping-SNAPHU-orange?style=for-the-badge)
![Output](https://img.shields.io/badge/Output-Digital%20Elevation%20Model-red?style=for-the-badge)

</div>

---

## Table of Contents

- [Overview](#-overview)
- [Project Objective](#-project-objective)
- [Study Area](#-study-area)
- [Data Selection Strategy](#-data-selection-strategy)
- [Data Source & Acquisition](#-data-source--acquisition)
- [Image Selection Criteria](#-image-selection-criteria)
- [Required Software](#-required-software)
- [Methodology](#-methodology)
- [Workflow Summary](#-workflow-summary)
- [Results](#-results)
- [Challenges Encountered](#-challenges-encountered)
- [Reproducibility Notes](#-reproducibility-notes)
- [Tools Used](#-tools-used)
- [Future Improvements](#-future-improvements)
- [References](#-references)

---

## Overview

This project demonstrates the generation of a **Digital Elevation Model (DEM)** from **Sentinel-1 Synthetic Aperture Radar (SAR)** imagery using **Interferometric SAR (InSAR)** processing techniques in **ESA SNAP**.

By exploiting phase differences between two SAR acquisitions, terrain elevation was reconstructed for the **Delamar Mountain Wilderness, Nevada, USA**.

---

## Project Objective

To generate an accurate, terrain-corrected DEM from Sentinel-1 SLC imagery through interferometric processing and phase unwrapping while minimizing coherence loss and atmospheric distortions.

---

## Study Area

### **Delamar Mountain Wilderness, Nevada, USA**

Nevada was selected due to its favorable environmental conditions for InSAR processing:

- **Arid desert climate**
- **Sparse vegetation cover**
- **Minimal surface water bodies**
- **Low relative humidity (~30–38%)**

These conditions improve **interferometric coherence** and reduce atmospheric interference.

### Terrain Characteristics

| Feature | Description |
|--------|-------------|
| Elevation Range | **790 – 1800 ft** |
| Topography | Deep winding canyons |
| Landforms | Rocky peaks & steep cliffs |
| Slope Features | Long sloping bajadas |

---

## Data Selection Strategy

DEM generation using InSAR requires:

- **Stable surface reflectivity** between acquisitions  
- **Minimal vegetation-induced decorrelation**  
- **Low atmospheric moisture**  

To reduce atmospheric distortion, imagery was selected from Nevada’s dry season:

### **Dry Season Window**
**May – September**

### **Chosen Acquisition Months**
- **May**
- **August**

---

## Data Source & Acquisition

SAR imagery was obtained from the **Copernicus Programme**.

### Dataset Specifications

| Parameter | Value |
|----------|------|
| Satellite | Sentinel-1 |
| Product Type | SLC (Single Look Complex) |
| Acquisition Mode | IW (Interferometric Wide Swath) |
| Download Portal | Copernicus Data Hub |

> Additional image IDs and study boundaries are available in the `helplist.txt` file.

---

## Image Selection Criteria

To ensure reliable interferometric DEM generation:

### **1. Orbit Direction Consistency**
Both images must:

- Be acquired in **Ascending orbit**
- Maintain identical viewing geometry

### **2. Perpendicular Baseline Constraint**
To ensure sufficient topographic sensitivity:

- **Perpendicular Baseline > 150 m**

### Verification Tool

- **ASF Vertex**

---

## Required Software

| Software | Purpose |
|--------|--------|
| ESA SNAP | InSAR Processing |
| SNAPHU | Phase Unwrapping |
| Google Earth Pro | DEM Visualization |

---

## Methodology

### **1. Preprocessing**
- Update and install SNAP plugins  
- Reinstall SNAPHU after output path modification  
- Import Sentinel-1 SLC scenes  

### **2. Image Preparation**
- Apply **S-1 TOPS Split**
  - Select subswath  
  - Select polarization  
  - Select burst covering AOI  

- Apply **Precise Orbit File**

### **3. Co-registration**
- Perform **S-1 Back Geocoding**
- Apply **Enhanced Spectral Diversity**

### **4. Interferogram Generation**
- Perform **Interferogram Formation**
- Run **TOPS Deburst**

### **5. Filtering**
- Apply **Goldstein Phase Filtering**
- Perform **Multilooking**
  - Range = **5**
  - Azimuth = **1**

### **6. Phase Unwrapping**
- Export to SNAPHU with:
  - Cost Mode = **TOPO**
  - Row Overlap = **300**
  - Column Overlap = **300**
  - Tiling = **4×4**

- Run SNAPHU Unwrapping  
- Import unwrapped output back into SNAP  

### **7. DEM Extraction**
- Perform **Phase to Elevation**
- Save DEM output  

### **8. Final Correction**
- Perform **Terrain Correction**
- Export final DEM as **KMZ**

---

## Workflow Summary

```text
Import Data
   ↓
TOPS Split
   ↓
Apply Orbit File
   ↓
Back Geocoding
   ↓
Enhanced Spectral Diversity
   ↓
Interferogram Formation
   ↓
TOPS Deburst
   ↓
Goldstein Filtering
   ↓
Multilooking
   ↓
SNAPHU Export
   ↓
SNAPHU Unwrapping
   ↓
Phase to Elevation
   ↓
Terrain Correction
   ↓
Export DEM
```

---

## Results

### Generated DEM Preview

<div align="center">

<img src="dem/dem_demo.gif" alt="DEM Result" width="700">

</div>

---

## Challenges Encountered

### **High Computational Load**
SNAPHU phase unwrapping was computationally expensive.

#### Solution Implemented
- Used **4×4 tiling** during SNAPHU export.

#### Side Effect
- Introduced minor **bounding line artifacts** in the unwrapped interferogram.

---

## Reproducibility Notes

To reproduce this workflow accurately:

- Use **Sentinel-1 SLC IW** imagery only  
- Maintain **same orbit direction** for image pair  
- Ensure **baseline > 150 m**  
- Select dry-season acquisitions  
- Preserve all listed SNAP/SNAPHU parameters  
- Maintain identical filtering/multilooking settings  

---

## Improvements to DEM

Potential enhancements to improve DEM quality:

- [ ] Experiment with alternative filtering techniques  
- [ ] Test different baseline thresholds  
- [ ] Compare results using varied SNAPHU tiling configurations  
- [ ] Integrate Ground Control Points (GCPs) for validation  
- [ ] Quantitatively assess DEM accuracy using RMSE  

---

<div align="center">

### ⭐ If you found this project helpful, consider starring the repository!

</div>
