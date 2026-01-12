
This document summarizes the experimental results obtained from the real-time, unsupervised anomaly detection pipeline for stellar spectra described in this repository. The focus here is on **what was found**, not on implementation details.
---

## 1. Experimental Setup

- **Dataset:** Real stellar spectra from the Sloan Digital Sky Survey (SDSS)
- **Data type:** Optical spectra (~3800 Å – 9200 Å)
- **Preprocessing:**  
  - Resampled to a common wavelength grid (2000 points)  
  - Per-spectrum normalization  
- **Model:**  
  - Deep autoencoder for representation learning  
  - Latent dimension: 32  
- **Anomaly Detection:**  
  - Isolation Forest applied to latent embeddings  
  - Reconstruction error from autoencoder  
  - Combined anomaly score for ranking  
- **Inference mode:**  
  - Batch processing  
  - Real-time streaming simulation  
  - Multi-cycle stability analysis  

---

## 2. Anomaly Detection Performance

### Initial Detection
When applied to a small set of SDSS stellar spectra, the pipeline successfully identified a small subset of spectra as anomalous, while the majority formed a coherent latent cluster.

Two complementary anomaly signals were observed:
- **Isolation-based anomalies:** Structurally rare spectra in latent space
- **Reconstruction-based anomalies:** Spectra poorly reconstructed by the autoencoder

This indicates that the pipeline is sensitive to multiple types of spectral irregularities.

---

## 3. Real-Time Streaming Results

The trained model was deployed in a simulated real-time setting, where spectra were processed sequentially as if arriving from a live survey.

Key observations:
- Anomalies were flagged immediately upon ingestion
- Streaming results were consistent with batch inference
- No instability or excessive false positives were observed

This demonstrates that the pipeline can operate reliably in a real-time or near-real-time environment.

---

## 4. Stability Across Observation Cycles

To test robustness, the system was run across **five simulated observation cycles**, re-processing the same spectral set multiple times.

### Stability Analysis Outcome

| Spectrum Index | Times Flagged (out of 5) | Interpretation |
|---------------|--------------------------|---------------|
| 3             | 5 / 5                    | Stable anomaly |
| 12            | 5 / 5                    | Stable anomaly |

All other spectra were either never flagged or flagged inconsistently.

**Interpretation:**  
Only spectra that were repeatedly identified as anomalous across multiple cycles were retained as high-confidence candidates. This significantly reduces the likelihood of spurious or noise-driven detections.

---

## 5. Candidate Spectrum Analysis

Visual inspection of the two stable candidates revealed two distinct anomaly regimes:

### Candidate Spectrum 3
- Smooth but systematically distinct spectral shape
- Consistent structure across the wavelength range
- Likely represents a **physically unusual or rare stellar spectrum**

This type of anomaly is of high interest for astrophysical follow-up.

### Candidate Spectrum 12
- Strong noise and instability at longer wavelengths
- Irregular flux behavior
- Likely represents a **data-quality or calibration-related anomaly**

Such detections are valuable for automated quality control in large surveys.

---

## 6. Summary of Findings

- The pipeline successfully identified **stable anomaly candidates** using unsupervised learning
- Anomalies were consistent across batch, streaming, and multi-cycle analysis
- The system differentiated between:
  - Physically distinct stellar spectra
  - Data-quality–related anomalies
- No manual labels or predefined classes were required at any stage

---

## 7. Limitations

- The dataset size was limited (demonstration scale)
- No external catalog cross-matching (e.g., SIMBAD, Gaia) was performed
- No physical confirmation via follow-up spectroscopy

These limitations are expected for a project-scale study and provide clear directions for future work.

---

## 8. Implications and Future Work

The results demonstrate the feasibility of using unsupervised AI models for automated anomaly detection in stellar surveys. With larger datasets and catalog integration, this pipeline could support:

- Rare object discovery
- Survey data quality monitoring
- Pre-filtering candidates for human or follow-up analysis

Future extensions may include scaling to larger surveys, transformer-based encoders, and catalog-aware validation.
