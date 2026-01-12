Real-Time Anomaly Detection in Stellar Spectra
This project implements a **real-time, unsupervised anomaly detection pipeline** for stellar spectra using deep learning and real astronomical survey data.  
The goal is to automatically identify **unusual or rare stellar spectra** without relying on predefined labels, enabling scalable analysis for modern astronomical surveys.

Project Overview
Modern sky surveys collect millions of stellar spectra, making manual inspection impractical.  
This project addresses that challenge by building an AI system that:
- Learns **normal stellar spectral behavior** from data
- Flags **unusual or anomalous spectra** automatically
- Operates in a **real-time streaming-like pipeline**
- Scales beyond small toy datasets

The pipeline is inspired by real survey workflows used in astronomy.

---
Dataset

- **Source:** Sloan Digital Sky Survey (SDSS)
- **Data type:** Optical stellar spectra
- **Wavelength range:** ~3800 Å – 9200 Å
- **Labels:** Not required (fully unsupervised)

Only real telescope data is used — no synthetic or toy datasets.

---

##  Methodology

The pipeline consists of the following stages:

### 1. Data Ingestion
- Spectra are queried directly from SDSS using `astroquery`
- Data is processed in batch and streaming-style modes

### 2. Spectral Preprocessing
- Resampling to a fixed wavelength grid
- Flux normalization to remove brightness scaling
- Conversion to machine-learning–ready tensors

### 3. Representation Learning
- A deep **autoencoder** is trained to learn compact latent representations
- Each spectrum is compressed from 2000 dimensions to a 32-dimensional embedding

### 4. Anomaly Detection
Two complementary anomaly criteria are used:
- **Isolation Forest** on latent embeddings (detects structurally rare spectra)
- **Reconstruction error** from the autoencoder (detects poorly modeled spectra)

These scores are combined to rank anomalous candidates.

### 5. Real-Time Streaming Simulation
- Spectra are processed one-by-one
- Anomalies are flagged immediately
- Alerts are logged as in a real survey pipeline

### 6. Scaling and Stability Analysis
- The system is run across multiple simulated observation cycles
- Only **stable, repeatedly detected anomalies** are retained as candidates
---

## Why This Matters

This project demonstrates how AI can:
- Reduce human inspection effort in large surveys
- Surface rare or interesting stellar objects automatically
- Assist astronomers in both **discovery** and **data quality control**

The approach is applicable to future large-scale surveys such as SDSS-V and LSST.

---

##  Limitations

- Limited dataset size (demonstration scale)
- No physical confirmation via follow-up spectroscopy
- No cross-matching with external catalogs (e.g., SIMBAD, Gaia)

These are intentional and realistic constraints for a project-scale study.

---

## Future Work

- Scale to hundreds or thousands of spectra
- Apply to Gaia XP spectrophotometry
- Integrate transformer-based encoders
- Cross-match anomaly candidates with astronomical catalogs
- Deploy as a persistent survey monitoring service

---


## 👤 Author

**Ninad Nagaraj Naik**  
Undergraduate Student, Gitam University 
Interests: AI/ML, Scientific Computing, Astronomy  
