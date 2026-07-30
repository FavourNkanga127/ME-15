# ME15 — Healthy Tomato vs Tomato Late Blight Classifier

## Overview

This project trains a binary image classifier to distinguish **Healthy Tomato** leaves from
**Tomato Late Blight** using **transfer learning** with MobileNetV2 pre-trained on ImageNet.
The model is built with TensorFlow / Keras and follows a two-phase training strategy: a
feature-extraction phase (frozen base) followed by a fine-tuning phase (top 30 layers unfrozen).
The dataset ships as flat class folders with no pre-made splits, so the notebook builds a
stratified 70 / 15 / 15 train / val / test split at runtime from the `color/` image variant only.

---

## Running the App

```bash
cd ME15
streamlit run app.py
```

The app will open automatically at **http://localhost:8501**

**Streamlit Cloud URL:** **

---

## Dataset

A brief description of the dataset source is provided in [`dataset/README.md`](dataset/README.md).

**Dataset:** PlantVillage Dataset — Kaggle  
**Classes:** `Tomato_healthy`, `Tomato_Late_blight`  
**Split strategy:** 70% train · 15% val · 15% test (built at runtime from `color/`)

---

## Environment Setup

### Requirements

Python **3.12** is recommended. All dependencies are pinned in [`requirements.txt`](requirements.txt).

### Install locally

```bash
# 1. Create and activate a virtual environment
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate

# 2. Install dependencies
pip install -r requirements.txt

# 3. Run the app
streamlit run app.py
```

### Key packages

| Package | Version | Purpose |
|---|---|---|
| `tensorflow` | 2.19.0 | Model training |
| `keras` | 3.15.0 | High-level API |
| `scikit-learn` | 1.8.0 | Evaluation metrics |
| `matplotlib` | 3.10.0 | Plotting |
| `seaborn` | 0.13.2 | Confusion matrix heatmap |
| `streamlit` | 1.60.0 | Web UI |

> **Note:** For faster training, use Google Colab with a T4 GPU runtime
> (`Runtime → Change runtime type → T4 GPU`).

---

## Project Structure

```
ME15/
├── dataset/
│   └── README.md          # Dataset source description
├── model/                 # Saved .keras model files
├── notebooks/
│   └── ME15.ipynb         # Full training pipeline
├── results/               # Plots, confusion matrices, learning curves
├── ood.py                 # OOD detection utility
├── requirements.txt
├── CONTRIBUTORS.md
└── README.md              # This file
```

---

## Challenges & Solutions

| Challenge | Solution / Notes |
|---|---|
| Dataset has 3 image variants (color, grayscale, segmented) | Filtered by `parent == 'color'` to use only RGB images |
| 38 plant disease classes in one folder | Substring matching (`'tomato' in base and 'healthy' in base`) isolates the two target classes |
| No pre-made train/val/test splits | Built a stratified 70/15/15 split at runtime |
| Visually similar healthy vs diseased leaf patterns | Fine-tuning top 30 MobileNetV2 layers improves leaf lesion discrimination |

---

## Possible Improvements

- Extend to multi-class tomato disease classification (9 tomato classes available in PlantVillage)
- Experiment with **EfficientNetB0** as an alternative base model
- Export the model to **TensorFlow Lite** for field deployment on mobile devices

---

## Results

> Full learning curves and confusion matrices are saved in `results/`.

---

## Contributors

See [CONTRIBUTORS.md](CONTRIBUTORS.md) for the full list of names, GitHub usernames, and registration numbers.
