# Dataset — PlantVillage (Healthy Tomato vs Tomato Late Blight)

## Source

**Name:** PlantVillage Dataset  
**Provider:** Kaggle — [abdallahalidev/plantvillage-dataset](https://www.kaggle.com/datasets/abdallahalidev/plantvillage-dataset)  
**License:** CC0: Public Domain

## Description

The PlantVillage dataset contains **54,306** images of healthy and diseased plant leaves across
**38 classes** spanning 14 crop species. Images are provided in three variants:

| Variant | Description |
|---------|-------------|
| `color/` | Original RGB photographs |
| `grayscale/` | Greyscale version of the same images |
| `segmented/` | Background-removed version |

This project uses **only the `color/` variant** and filters for two classes:

| Class folder | Label | Description |
|---|---|---|
| `Tomato___healthy` | Healthy | Tomato leaf with no disease signs |
| `Tomato___Late_blight` | Late Blight | Tomato leaf infected with *Phytophthora infestans* |

## Split Strategy

The dataset provides no pre-made train/val/test splits. The notebook builds a
**stratified 70 / 15 / 15** split at runtime using `shutil.copy` into temporary
`/content/tomato_split/train|val|test/<class>` directories.

## Download (in notebook)

```python
import kagglehub
path = kagglehub.dataset_download("abdallahalidev/plantvillage-dataset")
```

> The dataset is **not** stored in this repository. Run the notebook cell above on Google Colab
> to download it automatically.
