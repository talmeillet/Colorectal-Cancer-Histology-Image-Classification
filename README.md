# Colorectal Cancer Histology Image Classification

## Project Overview
The project focuses on the automated identification of tissue textures in histological images of colorectal cancer. Manual classification by pathologists is a time-consuming process that requires extensive expertise. Our goal is to develop machine learning models to automatically classify eight types of histological textures to support medical diagnosis and assessment of disease progression.

## 📊 Dataset
The project uses the public **Colorectal Histology** dataset available via TensorFlow Datasets.
- **Total Images:** 5,000 color histological images (RGB).
- **Resolution:** $150 \times 150$ pixels.
- **Categories:** 8 distinct tissue types (500 images per category).
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
<img width="1484" height="308" alt="image" src="https://github.com/user-attachments/assets/f529fa06-db02-47d0-a76c-2c60b6ee1074" />

### The Winning Model (Experiment #10)
By fine-tuning the VGG-16 model (unfreezing the last 4 layers), applying data augmentation, and adding dropout/batch normalization, we achieved:
- **Final Test Accuracy:** **94.8%**
- **Final F1-Score (Macro):** **0.948**
