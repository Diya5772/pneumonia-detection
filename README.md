# Pneumonia Detection from Chest X-rays

This repository contains a notebook-based deep learning project that classifies chest X-ray images as **Pneumonia** or **Normal**. It includes a trained model artifact and a project report.

> **Disclaimer:** This project is for educational/research use only and is **not** intended for clinical diagnosis.

## Repository Contents

- `pneumonia.ipynb` — end-to-end notebook (data loading, preprocessing, training, evaluation).
- `best_model.keras` — best checkpoint saved during training.
- `Pneumonia Detection Report.pdf` — detailed report with methodology and results.
- `README.md` — project documentation.

## Dataset

The notebook expects the **Chest X-Ray Pneumonia** dataset (commonly from Kaggle). The expected directory structure is:

```
chest_xray/
  train/
    PNEUMONIA/
    NORMAL/
  val/
    PNEUMONIA/
    NORMAL/
  test/
    PNEUMONIA/
    NORMAL/
```

In the notebook, the default Colab paths are `/content/chest_xray/train`, `/content/chest_xray/val`, and `/content/chest_xray/test`. Update these paths if you run locally (for example: `/home/user/data/chest_xray/train`).

## Approach Summary (from `pneumonia.ipynb`)

**Preprocessing**
- Grayscale images resized to **150x150**.
- Pixel values normalized to `[0, 1]`.

**Data Augmentation**
- Rotation, shifts, shear, zoom, horizontal flip.

**Model Architecture (CNN)**
- Conv blocks with filters: **32 → 64 → 128 → 256 → 512**
- Batch normalization + max pooling after each block
- Dropout (0.2, 0.3)
- Dense(256) + Dense(1, sigmoid)
- Optimizer: **RMSprop**
- Loss: **binary cross-entropy**

**Training**
- Batch size: **16**
- Epochs: **25**
- Callbacks: `ReduceLROnPlateau`, `EarlyStopping`, `ModelCheckpoint` (saves `best_model.keras`)

**Evaluation**
- Accuracy, precision, recall, F1, ROC-AUC
- Confusion matrix and learning curves

For detailed results and plots, see **Pneumonia Detection Report.pdf**.

## Getting Started

### Option A: Run in Google Colab
1. Upload `pneumonia.ipynb` to Colab.
2. Mount Google Drive and place the dataset zip (as used in the notebook).
3. Run the notebook cells in order.

### Option B: Run Locally
1. Create and activate a virtual environment.
2. Install dependencies (from notebook imports):
   - `tensorflow`
   - `keras`
   - `numpy`, `pandas`
   - `matplotlib`, `seaborn`
   - `scikit-learn`
   - `opencv-python`
3. Update dataset paths in the notebook to match your local folder structure.
4. Run the notebook.

## Using the Trained Model

`best_model.keras` is saved via `ModelCheckpoint` in the notebook. You can load it with:

```python
from tensorflow import keras
model = keras.models.load_model("best_model.keras")
```

## Notes & Limitations

- The notebook mixes data preparation, training, and evaluation in a single file.
- The validation set in the notebook is extended by concatenating the test set; adjust this if you want a strict hold-out test set.
- Results depend on dataset version and preprocessing choices.


