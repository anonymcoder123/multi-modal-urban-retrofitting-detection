# 🏙️ MURD-ViT: Multi-Modal Urban Retrofitting Detection

## Background on Urban Retrofitting

With large-scale urban expansion reaching saturation levels in many developed countries (Angel et al., 2020), cities increasingly rely on **urban retrofitting** — localized improvements in pre-existing infrastructures that elevate functionality and sustainability (Dixon et al., 2014).  
These small-scale retrofitting activities include **physical renovations**, **land use adaptations**, and **greening initiatives**, collectively enhancing a city's infrastructure, continuity, and livability.

Global cities have adopted diverse retrofitting strategies to improve urban livability, efficiency, and sustainability through five key approaches (Ma et al., 2025):

1. **Re-inhabitation** — Upgrading housing quality and socioeconomic conditions while promoting diversity.
2. **Re-building** — Optimizing existing structures for community purposes and increased density.
3. **Re-transportation** — Establishing interconnected, environmentally sustainable mobility networks.
4. **Re-capital** — Fostering sustainable socioeconomic development.
5. **Re-greening** — Incorporating natural environments within city infrastructure to provide environmental and cultural benefits.

---

## 🧠 MURD-ViT Architecture Overview

![Model Architecture](arch_diagram.png)

The **MURD-ViT** model leverages a **temporal Vision Transformer (ViT)** architecture combined with **temporal street view images and demographic features** to classify urban retrofitting types at the census block group level.

---

## 📂 Description of Files

### 🧩 Notebook Files

| Filename                                     | Description                                                                                                                                                                                                                    |
| -------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **baseline_model.ipynb**                     | Main program file for the baseline model used in this study. Includes dataset handling, model implementation, validation, visualization of predictions, and spatial distribution of model accuracy across census block groups. |
| **ablated_demographiccomponent_model.ipynb** | Ablation study removing the **demographic data component** to evaluate its contribution.                                                                                                                                       |
| **ablated_temporal_features_model.ipynb**    | Ablation study removing the **temporal image features** component to assess its effect.                                                                                                                                        |
| **utils.ipynb**                              | Contains helper scripts and utility functions used throughout the study for data preprocessing, metric computation, and visualization.                                                                                         |

---

### 🧱 Model Checkpoints

All model checkpoints are stored inside the **`ViT_Checkpoints/`** folder in the main directory.

| Filename                                         | Description                                                                         |
| ------------------------------------------------ | ----------------------------------------------------------------------------------- |
| **baseline_model_epoch_30.pth.pth**              | Baseline model checkpoint after 30 epochs.                                          |
| **ablated_demographic_model_epoch_30.pth**       | Ablated model checkpoint without the demographic data component (30 epochs).        |
| **ablated_temporal_features_model_epoch_30.pth** | Ablated model checkpoint without the temporal image features component (30 epochs). |

---

## 📊 Data

### 1. Street View Images

Street View images were collected following a hierarchical directory structure:

`Streetview_data/<Census Block Group>/<Latitude_Longitude_Direction>/<Month Year.png>`

The algorithm used to allocate random point locations and retrieve street view images is described in the manuscript.  
A detailed workflow for image sampling and acquisition is presented in the following reference:

- https://docs.lib.purdue.edu/cgi/viewcontent.cgi?article=1000&context=iguide

---

### 2. `labels.xlsx`

An Excel file that links the following attributes:

- Census Block Group
- Latitude
- Longitude
- Direction
- Temporal years
- Urban retrofitting category
- Population density change
- Population density change percentage

This file serves as the primary linkage between spatial locations, temporal image pairs, labels, and demographic change indicators.

---

### 3. Shapefiles

Boundary shapefiles were downloaded from the **U.S. Census Bureau** and used for spatial visualization and analysis across census block groups.

---

## 🔁 Guide to Reproduce Reported Findings

### Figure 1 — Distribution of Urban Retrofitting Categories and Sample Image Pairs

Four graduated-symbol maps were created in **ArcGIS Pro** to show the spatial distribution of different retrofitting categories across census block groups in Mecklenburg County, NC.  
Sample street view image pairs corresponding to specific retrofitting categories were mapped and annotated using **draw.io**.

- Map data source: `labels.xlsx`
- Image source: Street View Images folder for selected locations and time periods

---

### Figure 2 — Spatial Stratified Sampling for Training and Validation

Open `baseline_model.ipynb` and run cells from:

- `1. Installation and Setup`  
  through
- `8.3. Training Set Map Visualization`
- `8.4. Validation Set Map Visualization`

---

### Figure 3 — Model Architecture for Urban Retrofitting Detection

This figure was created using **https://draw.io**, but similar diagrams can be produced using tools such as PowerPoint, Canva, or other diagramming software.

---

### Table 2 — Evaluation Metrics for the Validation Dataset

Open `baseline_model.ipynb` and run cells from:

- `2. Package and Imports`  
  through
- `10.1. Classification Report and Confusion Matrix`

---

### Figure 4 — Training and Validation Accuracy and Loss Across Epochs

Open `baseline_model.ipynb` and run cells from:

- `2. Package and Imports`  
  through
- `10.2. Training Progress Visualization`

---

### Table 3 — Normalized Confusion Matrix Across Retrofitting Categories

Follow the same steps described for **Table 2 — Evaluation Metrics**.

---

### Figure 5 — True and False Predictions Across Retrofitting Categories

Open `baseline_model.ipynb` and run cells from:

- `2. Package and Imports`  
  through
- `10.3. Prediction Visualization`

---

### Figure 6 — Spatial Distribution of Model Performance Across Census Block Groups

Open `baseline_model.ipynb` and run cells from:

- `2. Package and Imports`  
  through
- `11.2. Accuracy Calculation per Census Block Group`

This process generates a shapefile named `latest_accuracy_per_census_block_group.shp`.

The shapefile contains per-category and overall accuracy values for each census block group.  
Use **ArcGIS Pro** to create graduated-symbol maps from this output.

---

### Table 4 — Evaluation Metrics for Ablation Studies

This table can be produced by running the following notebooks and collecting classification metrics:

1. `baseline_model.ipynb`
   - Run cells from `2. Package and Imports` to `10.1. Classification Report and Confusion Matrix`

2. `ablated_demographic_component_model.ipynb`
   - Run cells from `2. Package and Imports` to `10.1. Classification Report and Confusion Matrix`

3. `ablated_temporal_features_model.ipynb`
   - Run cells from `2. Package and Imports` to `10.1. Classification Report and Confusion Matrix`

---

## ⚠️ License and Usage

This repository and all associated materials are the intellectual property of **the authors**.  
The contents are provided **for academic and research reference only**.  
Copying, redistributing, reproducing, or using the files, models, or code in part or in whole **without prior written permission** from the author is strictly prohibited.

---
