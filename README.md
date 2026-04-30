# MOXAD_EarlyStageAD_Diagnosis_ADNI

This project focuses on early Alzheimer’s disease diagnosis using brain MRI scans from the **Alzheimer’s Disease Neuroimaging Initiative (ADNI)**. It builds a full deep learning pipeline for preprocessing MRI volumes, extracting multi-orientation slices, training CNN-based models, and exploring a hybrid **CNN-ViT** architecture for improved classification performance.

## Project Overview

The workflow starts with raw ADNI NIfTI MRI volumes and converts them into a structured dataset that is ready for deep learning. It supports three anatomical views of the brain:

- **Axial**
- **Coronal**
- **Sagittal**

The project is organized into multiple stages, from preprocessing to model training and interpretability:

1. **Data preprocessing and organization**
2. **ResNet50-based classification experiments**
3. **Multi-orientation CNN modeling**
4. **Hybrid CNN-ViT fusion with cross-attention**
5. **Grad-CAM and attention-based visualization**

## Key Features

- Preprocesses nested ADNI MRI folders into a clean training dataset
- Extracts slices from multiple anatomical orientations
- Supports 5 diagnostic classes:
  - CN
  - EMCI
  - MCI
  - LMCI
  - AD
- Applies intensity normalization and image resizing to 224 × 224
- Uses subject-level splitting to reduce data leakage
- Saves model-ready CSV and NumPy artifacts
- Includes visualization outputs for interpretability analysis

## Dataset

The project uses ADNI MRI scans and organizes them into the following class labels:

- **CN**: Cognitively Normal
- **EMCI**: Early Mild Cognitive Impairment
- **MCI**: Mild Cognitive Impairment
- **LMCI**: Late Mild Cognitive Impairment
- **AD**: Alzheimer’s Disease

The preprocessing pipeline generates a large multi-orientation dataset stored under:

- `Dataset and Output/ADNI_PHASE1_PROCESSED/`

## Workflow

### 1. Preprocessing
The preprocessing notebook scans the ADNI directory structure, selects valid MRI volumes, extracts slices from all three orientations, and saves class-organized PNG images and metadata files.

### 2. Baseline CNN Training
A ResNet50 baseline is trained on the preprocessed images to establish a strong reference model for Alzheimer’s classification.

### 3. Multi-Orientation Learning
Separate CNN feature extractors are trained for axial, coronal, and sagittal views. Their outputs can be ensembled for improved performance.

### 4. CNN-ViT Hybrid Modeling
The later phase combines multi-view CNN features with a Vision Transformer and cross-attention mechanism to fuse complementary information from different brain views.

### 5. Interpretability
Grad-CAM, Grad-CAM++, and attention-based methods are used to visualize which regions of the MRI contributed most to the model’s prediction.

## Reported Results

These are the saved results currently present in the repository outputs:

- **Phase 1 baseline ResNet50**: 92.57% test accuracy
- **Phase 2 multi-orientation ensemble**: 94.50% test accuracy
- **Phase 3 CNN-ViT cross-attention model**: 94.68% test accuracy

## Repository Structure

```text
01_preprocessing_FINAL.ipynb
02_resnet50_axial_full_production.ipynb
03-resnet50-multi-orientation.ipynb
04-cnn-vit-base-cross-attention.ipynb
05-visualization-gradcam-attention.ipynb
5-inference-demo-viva.ipynb
Dataset and Output/
```

## Notebooks

- **01_preprocessing_FINAL.ipynb**: ADNI MRI preprocessing, slice extraction, and dataset preparation
- **02_resnet50_axial_full_production.ipynb**: Baseline ResNet50 training on axial images
- **03-resnet50-multi-orientation.ipynb**: Multi-orientation CNN training and ensemble analysis
- **04-cnn-vit-base-cross-attention.ipynb**: CNN-ViT hybrid model with cross-attention fusion
- **05-visualization-gradcam-attention.ipynb**: Interpretability and visualization outputs
- **5-inference-demo-viva.ipynb**: Inference/demo notebook for the final model pipeline

## Output Artifacts

The repository includes several saved outputs under `Dataset and Output/`, including:

- Trained model checkpoints
- Feature extractor weights
- Train/validation/test metadata splits
- Metrics and evaluation summaries
- Visualization images and attention maps

## Requirements

Typical dependencies used in the notebooks include:

- Python 3.10+
- PyTorch
- NumPy
- Pandas
- OpenCV
- Nibabel
- Scikit-learn
- Matplotlib
- Seaborn
- Albumentations
- TQDM

## How to Run

1. Open the notebooks in Jupyter or Google Colab.
2. Run the preprocessing notebook first to generate the processed dataset.
3. Train the baseline or multi-orientation CNN models.
4. Run the CNN-ViT notebook for the final hybrid model.
5. Use the visualization notebook to inspect model attention and Grad-CAM outputs.

## Notes

- The preprocessing workflow is designed to handle large nested ADNI directory structures.
- The pipeline includes a resume feature for crash recovery during long preprocessing runs.
- Some notebooks are designed for Google Colab with access to Google Drive.

## License

This repository does not currently include a license file. Add one if you plan to share or distribute the project publicly.
