# 🌊 Ocean Debris Detection — Sentinel-2 + Google Earth Engine

A machine learning pipeline that detects ocean debris using satellite imagery from **Sentinel-2** and **Google Earth Engine**, combined with a **U-Net deep learning model** for debris segmentation.

---

## 🔧 Tech Stack

- **Language:** Python
- **Satellite Data:** Sentinel-2 Level-2A via Google Earth Engine
- **ML Framework:** PyTorch (U-Net segmentation model)
- **Libraries:** `earthengine-api`, `geemap`, `rasterio`, `albumentations`, `scikit-learn`, `torchvision`
- **Environment:** Google Colab (GPU — T4 recommended)

---

## ✨ How It Works

The pipeline runs in 7 steps:

1. **Connect to Google Earth Engine** — authenticates and initialises the GEE project
2. **Fetch Sentinel-2 imagery** — cloud-filtered imagery over South-East Asian seas (2024)
3. **Build ocean mask** — combines LSIB land polygons + NDWI water index to isolate ocean pixels
4. **Compute spectral indices** — calculates FDI, NDWI, and PI to identify floating debris signatures
5. **Visualise on interactive map** — renders debris candidates as a heatmap using `geemap`
6. **Export image patches** — saves 10-band GeoTIFF patches to Google Drive for training
7. **Train U-Net model** — trains a deep learning segmentation model to classify debris vs water

### Spectral Indices Used

| Index | Purpose | Bands |
|-------|---------|-------|
| **FDI** | Floating Debris Index — detects floating plastic | NIR, Red, SWIR |
| **NDWI** | Water mask — separates sea from land | Green, NIR |
| **PI** | Plastic Index — plastic vs organic matter | NIR, Red |

---

## 🚀 How to Run

1. Open the notebook in **Google Colab** (GPU runtime recommended)

2. Install dependencies — run **Step 1** cell:
   ```bash
   pip install earthengine-api geemap segmentation-models-pytorch rasterio torch torchvision albumentations scikit-learn tqdm
   ```

3. Authenticate Google Earth Engine:
   ```python
   import ee
   ee.Authenticate()
   ee.Initialize(project='your-gee-project-id')
   ```

4. Run all cells in order — estimated time: **30–45 minutes** on first run

5. Exported GeoTIFF patches will appear in your **Google Drive** under `ocean_debris_patches/`

---

## 👥 Team

This project was collaboratively developed by a team of 4 members. All members contributed equally to the research, development, and testing of the pipeline.

| Name | GitHub |
|------|--------|
| Shruti Khisa | [@Shruti-570](https://github.com/Shruti-570) |
| Shaira Akhter Diba | [@ShairaDiba](https://github.com/ShairaDiba) |
| Farhan Tanvir | [@Tanvir868X](https://github.com/Tanvir868X) |
| Farhan Noor | [@frnoor](https://github.com/frnoor) |

> **Note:** This project was developed collaboratively offline and committed to GitHub after completion. All team members contributed equally to the codebase.

---

## 📌 Project Status

✅ Completed

---

## 📄 License

This project was made for academic purposes.
