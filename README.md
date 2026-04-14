# Colorectal Cancer Histology Image Classification

## Project Overview
This project focuses on the automated classification of histological images from colorectal cancer (CRC) tissues using advanced Machine Learning and Computer Vision techniques. The system aims to support pathologists by providing an automated tool to identify and categorize different tissue types within high-resolution histological images, a critical step in cancer diagnosis and research.

## 📊 Dataset
The project uses the public **Colorectal Histology** dataset available via TensorFlow Datasets.
- **Total Images:** 5,000 color histological images (RGB).
- **Resolution:** 150*150 pixels.
- **Categories:** 8 distinct tissue types (625 images per category).
  *   Tumour epithelium
  *   Simple stroma
  *   Complex stroma
  *   Immune cells
  *   Debris
  *   Normal mucosal glands
  *   Adipose tissue
  *   Background
- **Data Split:** 80% Training (4,000 images) and 20% Testing (1,000 images).

## 🛠 Feature Extraction Methods
We experimented with three different approaches to extract features from the raw images:
1.  **Downsample + Flatten:** Resizing images to $32 \times 32$ and flattening into a 3,072-length vector.
2.  **PCA (Principal Component Analysis):** Flattening original images and reducing dimensions to 256 principal components.
3.  **VGG-16 Backbone:** Using a pre-trained VGG-16 network (without top layers) to extract a feature vector of length 8,192.

## Experiments & Results
We conducted 9 initial experiments combining the extraction methods with three classifiers: **SVM**, **Softmax**, and **Neural Networks (NN)**.

### Performance Summary:

| Exp # | Feature Extraction Method | Classifier | Training Accuracy | Test Accuracy |
| :---: | :--- | :--- | :---: | :---: |
| 1 | Downsample + Flatten | SVM | 0.440 | 0.435 |
| 2 | Downsample + Flatten | Softmax | 0.402 | 0.395 |
| 3 | Downsample + Flatten | Neural Network (NN) | 0.395 | 0.380 |
| 4 | PCA (256 Components) | SVM | 0.460 | 0.445 |
| 5 | PCA (256 Components) | Softmax | 0.415 | 0.400 |
| 6 | PCA (256 Components) | Neural Network (NN) | 0.420 | 0.410 |
| 7 | VGG-16 (Backbone Only) | SVM | 0.885 | 0.870 |
| 8 | VGG-16 (Backbone Only) | Softmax | 0.860 | 0.855 |
| 9 | VGG-16 (Backbone Only) | Neural Network (NN) | 0.875 | 0.865 |
| **10**| **Fine-tuned VGG-16 (+ Augmentation)** | **Neural Network (NN)** | **0.965** | **0.948** |



### The Winning Model (Experiment #10)
We used Transfer learning:
By fine-tuning the VGG-16 model (unfreezing the last 4 layers), applying data augmentation, and adding dropout/batch normalization, we achieved:
- **Final Test Accuracy:** **94.8%**
- **Final F1-Score (Macro):** **0.948**
