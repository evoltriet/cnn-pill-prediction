# CNN Pill Prediction

A notebook-driven computer vision study for identifying pill types from pharmacy vial images, with a custom CNN baseline and transfer-learning experiments for comparison.

## Overview
This project explores how far a CNN can go on pill-image classification when the goal is operationally careful identification rather than a flashy demo. The notebook walks through loading the image set, cleaning duplicates, preprocessing images to a consistent shape, training models, and checking predictions on held-out data.

## Problem
Pharmacy vial photos are messy inputs: filenames encode the label, images can be duplicated, and the classifier needs to work with resized RGB images rather than curated examples. The core task here is to classify pill images reliably enough to support a precision-sensitive workflow.

## Approach
- Images are loaded from `data/All_VialImages/`, and the pill type is inferred from the filename prefix.
- Duplicate files are detected by MD5 hash before training so the model does not learn from repeated images.
- The data is split into train, validation, and test sets with stratification to preserve class balance.
- Images are resized to `224x224x3` and normalized before being passed into Keras models.
- The notebook trains a custom CNN from scratch, then also includes transfer-learning branches for `VGG16` and `ResNet50`.
- Helper functions such as `predict_pill_binary` and `predict_pill_categorical` print class confidence tables and display the source image for manual inspection.

## Outcome
The visible binary CNN result in the notebook reaches `97.6277%` test accuracy. The corresponding classification report shows strong class 0 performance and high precision on the positive class, with recall lower on the positive class than on the negative class. The notebook also includes VGG16 and ResNet50 experiments.

## How To Explore
1. Open `CNN_Pill_Prediction.ipynb` in Jupyter or a notebook-compatible editor.
2. Restore the original image dataset under `data/All_VialImages/`.
3. Make sure any generated folders referenced by the notebook exist, such as `saved_models/` and `bottleneck_features/`.
4. Run the notebook top to bottom to reproduce the preprocessing, training, and inference walkthrough.
5. Use the helper prediction cells near the end to test a single image or loop over sample test files.

## Repository Artifacts
- `CNN_Pill_Prediction.ipynb`
- `AIPV ML Overview.pptx`

## Limitations
- The repo does not include the original image dataset or the saved model artifacts, so reproduction depends on restoring those external files.
- The notebook mixes a binary target and a multiclass workflow, so a reader should follow the labeled sections carefully when interpreting results.
- The stack is legacy Keras/TensorFlow-era tooling, so environment setup may require older package versions.
