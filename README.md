# README – Mineral Targeting AI Model 

## Overview
This project performs automated mineral prediction using AI/ML models based on geoscientific datasets from Karnataka and Andhra Pradesh. It integrates geochemical, geophysical, geological, and spatial data to train and deploy a mineral classification model.

---

## Files to Upload Before Running the Code
All files should be uploaded as `.zip` archives containing relevant shapefiles or CSVs.

| Type              | File Description                                     | Naming Expectation                            |
|-------------------|-------------------------------------------------------|------------------------------------------------|
| Geochemical CSV   | Stream sediment survey data                          | Contains "stream" in filename                 |
| Gravity CSV       | Ground gravity values (if available)                 | Contains "gravity" in filename                |
| Aeromagnetic Raster | Total magnetic intensity grid (DEM)                | Contains "TAIL_TMI_GE" in filename            |
| Gravity Raster    | Ground gravity raster                                | Contains "grav" in filename                   |
| Faults Shapefile  | Structural fault lines                               | Contains "fault"                              |
| Folds Shapefile   | Structural folds                                     | Contains "fold"                               |
| Oriented Planes   | Oriented structural planes                           | Contains "oriented_structure_plane"           |
| Exploration Points| Mineral exploration point shapefile                  | Contains "exploration"                        |
| Geomorphology     | Geomorphology polygons                               | Contains "geomorphology"                      |
| Geochronology     | Geochronological polygon features                    | Contains "geochronology"                      |
| Lineaments        | Lineament shapefile (for 3D map only)               | Contains "lineament"                          |

---

## Key Features of the Code

### 🔹 Data Processing
- Reads geochemical and spatial datasets
- Reprojects all layers to a common CRS (WGS84)
- Samples raster values from aeromagnetic and gravity rasters
- Calculates distances to nearby faults, folds, and other geological features
- Generates a synthetic depth estimate using magnetic intensity

### 🔹 Feature Engineering
- Builds a 22-feature matrix combining:
  - 13 geochemical features (element ppm/ppb)
  - 6 structural/spatial distances
  - 2 geophysical raster values
  - 1 synthetic depth feature

### 🔹 Mineral Labeling
- Assigns one of 13 mineral classes based on geochemical thresholds (Ce, La, Nd, Cu, Au, U, Th, Pb, Zn, Ni, Co, Li, Cr)

### 🔹 Model Training
- Applies `BorderlineSMOTE` for class balancing (k_neighbors=2)
- Trains both `MLPClassifier` and `RandomForestClassifier`
- Selects the best model based on macro ROC-AUC

### 🔹 Evaluation
- Computes confusion matrix, classification report, macro F1-score
- Generates multi-class ROC curves
- Plots Random Forest feature importances (for interpretability)

### 🔹 Output Generation
- Saves trained model (`.pth`), scaler (`.pkl`), and predictions (`.geojson`)
- Creates:
  - Interactive 2D prediction map (`.html` with Folium)
  - Mineral-wise abundance maps (`Ce_abundance_map.html`, etc.)
  - 3D terrain map with mineral predictions + lineaments (`enhanced_3d_map.html`)

### 🔹 Dependencies
Ensure the following Python libraries are installed:
pip install geopandas rasterio scikit-learn torch torchvision shapely matplotlib folium branca imbalanced-learn plotly

---

## Author
**Aswin Mohan**  
IndiaAI–GSI Hackathon 2025
