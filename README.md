# CIFAR-10 Image Classifier 🚗

🎓 **Academic Note:** This repository contains my completed submission for the Image Classifier project. The starter code template, foundational project guidelines, and dataset utilities are proprietary materials provided by and credited to Udacity. The implementation logic, custom CNN architecture, training pipeline configurations, and strategic analysis contained herein are my original work.

A deep learning project that builds custom Convolutional Neural Networks (CNNs) in PyTorch to classify the 10 object classes of the CIFAR-10 dataset, framed as a build-vs-buy decision for an autonomous vehicle team.

## 📊 Project Performance Summary

| Model | Notebook | Test Accuracy |
|---|---|---|
| Vendor Baseline (Detectocorp) | — | 70.00% |
| v1: 3-layer CNN (course submission) | [`CIFAR-10_Image_Classifier-STARTER.ipynb`](CIFAR-10_Image_Classifier-STARTER.ipynb) | 75.98% |
| **v2: VGG-style CNN with BatchNorm** | [`CIFAR-10_Image_Classifier-Improved.ipynb`](CIFAR-10_Image_Classifier-Improved.ipynb) | **91.64%** |

v2 improves on v1 by **15.7 points** and on the vendor baseline by **21.6 points**, training in 8.6 minutes on a GTX 1650.

## v2: Improved Model

### Architecture Breakdown

* **Convolutional Layers:** 6 layers in 3 VGG-style blocks (`64 ➔ 128 ➔ 256` filters), each `Conv2d ➔ BatchNorm2d ➔ ReLU`.
* **Spatial Pooling:** `MaxPool2d` after each block, then global average pooling in place of large fully connected layers.
* **Regularization:** Dropout after each block (`0.1 ➔ 0.2 ➔ 0.3`) and weight decay (`5e-4`).
* **Classifier:** A single linear layer mapping 256 features to the 10 classes (1.15M parameters in total).

### Training Pipeline Configurations

* **Optimizer:** SGD with Nesterov momentum (0.9)
* **Learning Rate Schedule:** OneCycle, peaking at 0.1
* **Loss Function:** `CrossEntropyLoss`
* **Batch Size:** 128
* **Epochs:** 30
* **Data Augmentation:** `RandomCrop` and `RandomHorizontalFlip`, normalized with the CIFAR-10 channel mean and standard deviation.
* **Precision:** fp32. Mixed precision (fp16) was about 6× slower on the GTX 1650 and returned NaN outputs at evaluation time.

### Per-Class Test Accuracy

The hardest classes are the visually similar animals: cat (81.2%), bird (86.8%) and dog (87.7%). All vehicle classes and ships score above 94%.

## v1: Course Submission

### Architecture Breakdown

* **Convolutional Layers:** 3 layers with increasing filter depth (`16 ➔ 32 ➔ 64`) using $3 \times 3$ kernels and `ReLU` activation functions to capture hierarchical visual features.
* **Spatial Pooling:** `MaxPool2d` layers to downsample spatial dimensions and retain dominant structural features.
* **Regularization:** `nn.Dropout(0.2)` integrated into the fully connected layers to mitigate overfitting and ensure robust generalization.
* **Classifier:** 3 Dense (Fully Connected) layers mapping the flattened feature maps down to the final 10 object classes.

### Training Pipeline Configurations

* **Optimizer:** Adam ($\alpha = 0.001$)
* **Loss Function:** `CrossEntropyLoss`
* **Batch Size:** 64
* **Epochs:** 20
* **Data Augmentation:** `RandomHorizontalFlip` and `RandomCrop` applied during training to simulate varied environmental and driving conditions.
