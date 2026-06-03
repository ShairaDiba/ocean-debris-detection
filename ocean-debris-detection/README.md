# 🌊 Ocean Debris Detection — Sentinel-2 + U-Net

> Satellite-based ocean plastic and marine debris detection using Google Earth Engine spectral indices and a PyTorch U-Net segmentation model.

---

## 📌 Overview

This project uses **Sentinel-2 Level-2A** satellite imagery processed through **Google Earth Engine (GEE)** to detect floating marine debris in ocean environments. A **U-Net deep learning model** is trained on exported image patches and produces pixel-level debris probability heatmaps.

The default study area is the **South-East Asian seas** (Gulf of Thailand / South China Sea), a region with high known debris density — but the pipeline is fully configurable for any ocean region.

---

## 🛰️ Pipeline

```
Sentinel-2 SR imagery (GEE)
        ↓
Cloud masking + Ocean masking (LSIB + NDWI)
        ↓
Spectral Indices: FDI · NDWI · PI
        ↓
Export 256×256 patches → Google Drive (GeoTIFF)
        ↓
U-Net segmentation training (PyTorch)
        ↓
Inference → Debris heatmap + Monthly trend analysis
```

---

## ✨ Key Features

| Feature | Detail |
|---|---|
| **Imagery** | Sentinel-2 Level-2A (surface reflectance, atmospherically corrected) |
| **Spectral Indices** | FDI (Floating Debris Index), NDWI (water mask), PI (Plastic Index) |
| **Ocean Mask** | LSIB land polygons + NDWI second-pass to exclude small islands |
| **Model** | U-Net with `segmentation-models-pytorch`, tiled inference for large scenes |
| **Visualisation** | Interactive GEE map (geemap) + monthly debris area trend charts |
| **Export** | GeoTIFF patches to Google Drive, model weights, heatmaps |

---

## 📂 Repository Structure

```
ocean-debris-detection/
├── ocean_debris_detection_final_v2.ipynb   # Main notebook (all steps)
├── README.md
└── assets/                                 # (optional) example outputs
    ├── debris_heatmap.html
    ├── prediction_output.png
    └── debris_trend.png
```

---

## 🚀 Quick Start

### 1. Requirements

This notebook is designed to run on **Google Colab** (GPU runtime recommended — T4 or better).

All Python dependencies are installed automatically in **Step 1** of the notebook:

```bash
earthengine-api  geemap  segmentation-models-pytorch
rasterio  torch  torchvision  albumentations
scikit-learn  tqdm  numpy  pillow  matplotlib  folium
```

### 2. Google Earth Engine Authentication

A GEE account with a registered **Cloud Project** is required. Update the project ID in **Step 2**:

```python
PROJECT = 'your-gee-project-id'
ee.Initialize(project=PROJECT)
```

Sign up free at [earthengine.google.com](https://earthengine.google.com).

### 3. Run the Notebook

Open in Colab and run cells top-to-bottom. Estimated total runtime: **~30–45 min** on a T4 GPU.

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/YOUR_USERNAME/ocean-debris-detection/blob/main/ocean_debris_detection_final_v2.ipynb)

> Replace `YOUR_USERNAME` with your GitHub username after uploading.

---

## 📓 Notebook Steps

| Step | Description |
|---|---|
| 1 | Install all dependencies |
| 2 | Authenticate & initialise Google Earth Engine |
| 3 | Define ROI, fetch Sentinel-2 imagery, build ocean mask |
| 4 | Compute FDI, NDWI, and PI spectral indices |
| 5 | Visualise on an interactive GEE/geemap map |
| 6 | Export monthly GeoTIFF patches to Google Drive |
| 7 | Define U-Net model architecture |
| 8 | Build `DebrisDataset` PyTorch data loader |
| 9 | Train U-Net and plot learning curves |
| 10 | Run inference; generate debris probability heatmap |
| 11 | Export interactive HTML heatmap |
| 12–13 | Monthly time-series trend analysis |
| 14 | Save all outputs to Google Drive |

---

## 🗺️ Changing the Study Region

Edit `ROI_COORDS` in Step 3 to target any ocean area:

```python
ROI_COORDS = [
    [100.0, 5.0],
    [104.0, 5.0],
    [104.0, 9.0],
    [100.0, 9.0],
    [100.0, 5.0],
]
```

Update `START_DATE` / `END_DATE` and the `months` list in Step 6 accordingly.

---

## 📊 Spectral Indices Reference

| Index | Formula | Use |
|---|---|---|
| **FDI** | `NIR₈ₐ − (Red + (SWIR−Red) × λ_factor)` | Detects floating plastic/debris |
| **NDWI** | `(Green − NIR) / (Green + NIR)` | Water vs. land separation |
| **PI** | `NIR / (NIR + Red)` | Plastic vs. organic matter |

---

## 🙏 Acknowledgements

- [Google Earth Engine](https://earthengine.google.com) — satellite imagery and geospatial processing  
- [Copernicus / ESA](https://www.esa.int) — Sentinel-2 imagery  
- [segmentation-models-pytorch](https://github.com/qubvel/segmentation_models.pytorch) — U-Net implementation  
- [geemap](https://geemap.org) — interactive GEE mapping in Python  

---

## 📄 License

MIT License — see [LICENSE](LICENSE) for details.
