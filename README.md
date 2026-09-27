# Urban Flood Susceptibility Assessment

A simplified hybrid CNN-Transformer proof-of-concept for pixel-wise urban flood susceptibility mapping using a synthetic geospatial dataset inspired by the supplied research paper.

## Overview

This project compares:
- CNN baseline for local spatial feature extraction
- CNN + Transformer for spatial context modeling

The model uses 9 environmental feature layers and predicts a flood/non-flood mask for each pixel.

## Dataset

The synthetic dataset follows the 9-channel structure described in the reference paper:

- Elevation
- Slope
- NDVI
- NDWI
- LULC
- Soil Type
- Impervious Surface
- Rainfall
- TWI

Input shape: `9 × 64 × 64`  
Output shape: `64 × 64`

The dataset is synthetic and is not real Sharjah GIS or satellite data.

## Approach

```text
9 Environmental Layers
        ↓
   Preprocessing
        ↓
   ┌───────────────┐
   │               │
   CNN        CNN + Transformer
   │               │
   │          CNN Feature Extraction
   │               ↓
   │          16 × 16 Tokens
   │               ↓
   │          Transformer
   │               │
   └───────┬───────┘
           ↓
    Flood Prediction
           ↓
       Evaluation
```

The CNN learns local spatial patterns. The hybrid model adds a Transformer encoder to model relationships between spatial feature tokens.

## Results

| Metric | CNN | CNN + Transformer |
|---|---:|---:|
| Accuracy | 0.9083 | 0.9139 |
| Precision | 0.8705 | 0.8535 |
| Recall | 0.7902 | 0.8359 |
| F1 Score | 0.8284 | 0.8446 |
| IoU | 0.7070 | 0.7310 |

In this experiment, the CNN + Transformer model achieved higher Accuracy, Recall, F1 Score, and IoU, with a small decrease in Precision.

## Technologies

Python, PyTorch, NumPy, Pandas, Scikit-learn, Matplotlib, Jupyter Notebook

## Project Files

```text
Flood_Susceptibility_Assessment.ipynb
requirements.txt
architecture_diagram.png
README.md
```

The synthetic dataset is included in the source-code ZIP submitted with the assessment.

## How to Run

```bash
pip install -r requirements.txt
jupyter notebook Flood_Susceptibility_Assessment.ipynb
```

Place `sharjah_synthetic_flood_dataset.npz` in the required location before running the notebook.

## Limitations

This is a simplified proof-of-concept using synthetic data. It does not reproduce the complete research architecture, real Sharjah data, hydro-aware attention, or SHAP analysis.

## Reference

Chakrabortty, R. et al. (2026). *Urban Flood Susceptibility Assessment in Arid Environment Using a Novel Hybrid Deep Learning Approach*. Earth Systems and Environment.
