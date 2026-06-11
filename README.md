# Image Classification for Autonomous Vehicles 🚗

🎓 **Academic Note:** This repository contains my completed submission for the Image Classifier project. The starter code template, foundational project guidelines, and dataset utilities are proprietary materials provided by and credited to Udacity. The implementation logic, custom CNN architecture, training pipeline configurations, and strategic analysis contained herein are my original work.

A deep learning project that builds a custom Convolutional Neural Network (CNN) using PyTorch to classify arbitrary roadside objects using the CIFAR-10 dataset.

## 📊 Project Performance Summary

* **In-House Custom CNN Test Accuracy:** **75.98%**
* **Vendor Baseline (Detectocorp) Accuracy:** 70.00%
* **Net Performance Increase:** **+5.98%**

### Architecture Breakdown

* **Convolutional Layers:** 3 layers with increasing filter depth (`16 ➔ 32 ➔ 64`) using $3 \times 3$ kernels and `ReLU` activation functions to capture hierarchical visual features.
* **Spatial Pooling:** `MaxPool2d` layers to downsample spatial dimensions and retain dominant structural features.
* **Regularization:** `nn.Dropout(0.2)` integrated into the fully connected layers to mitigate overfitting and ensure robust generalization.
* **Classifier:** 3 Dense (Fully Connected) layers mapping the flattened feature maps down to the final 10 object classes.

### Training Pipeline Configurations

* **Optimizer:** Adam ($\alpha = 0.001$)
* **Loss Function:** `CrossEntropyLoss`
* **Batch Size:** 128
* **Epochs:** 20
* **Data Augmentation:** `RandomHorizontalFlip` and `RandomCrop` applied during training to simulate varied environmental and driving conditions.
