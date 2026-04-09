# DEM-Generation-SAR

## Data Selection for DEM Generation

Digital Elevation Model (DEM) generation using Interferometric SAR (InSAR) requires stable surface conditions between image acquisitions. Areas with minimal water bodies and low vegetation density are preferred because they provide more coherent radar backscatter. Environments with high humidity or significant atmospheric moisture can reduce interferometric coherence and negatively affect elevation accuracy.

To minimize atmospheric effects such as humidity and precipitation, SAR scenes were selected from hot and dry periods of the year. In the case of Nevada, the driest months typically occur between May and September, which represent the primary dry season. Based on these conditions, SAR images acquired in May and August were used for this project.


## Study Area

`Delamar Mountain Wilderness, Nevada, US:` With its low humidity and an average relative humidity around 30%–38%, Nevada is considered the driest state in the U.S. It features an arid desert climate where moisture levels remain low year-round, making hot temperatures feel more comfortable but requiring consistent hydration. The elevation of the Delamar Mountains Wilderness is unique for its dramatic range, spanning approximately 790 to 1800 feet. This significant vertical relief creates a diverse landscape featuring deep, twisting canyons, high rocky peaks, spectacular cliffs, and long sloping bajadas.


## Data Source & Acquisition

The SAR data used in this project were obtained from Copernicus Programme and correspond to Sentinel-1 acquisitions in SLC IW (Single Look Complex – Interferometric Wide Swath) mode. All selected Sentinel-1 SLC IW scenes were downloaded directly from the Copernicus data hub and subsequently processed in SNAP for interferometric DEM generation. The specidfic images and study boundaries can be found in the `helplist.txt` file.


## Image Selection Criteria

To generate a reliable interferometric pair for DEM extraction in ESA SNAP, the following criteria were applied when selecting images:

### 1. Identical Orbit Direction
Both scenes must be acquired from the same orbit direction (Ascending) to maintain consistent acquisition geometry.

### 2. Perpendicular Baseline Constraint
The perpendicular baseline must be greater than 150 m to ensure sufficient interferometric sensitivity to topography. Baseline information was verified using ASF Vertex.


## Methodology (Using SNAP)

1. Check, update, and download required plugins.
2. Reinstall SNAPHU after changing the output file path.
3. Import the images
4. Using S-1 TOPS Split (under the radar tab, select the desired subswath, polarization, and burst), select only the study area.
5. Apply Orbit file
6. Co-registration using S-1 Back Geocoding
7. Perform enhanced spectral diversity
8. Perform Interferogram formation
9. Perform TOPS Deburst
11. Perform Goldstein Phase filtering to smoothen the image
12. Perform Multilooking (5x1, azimuth=1)
13. Perform Phase Unwrapping:
- SNAPHU Export: stat cost mode=TOPO, row and col overlap=300 using 4×4 tiling
- SNAPHU unwrapping
- SNAPHU import
14. Perform Phase to Elevation
15. Save output dem file.
16. Perform Geometric correction (Terrain correction)
17. Save Final dem as KMZ file.

## Result

<img src="dem/dem_demo.gif" alt="" width="600">


## Challenges
- High computational load required for the SNAPHU Unwrapping. Thus using 4x4 tilling resulted to small bounding line in the unwrapped interferogram.


## Tools

- ESA SNAP
- Google Earth Pro (Visualization)

