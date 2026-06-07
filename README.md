# Multimodal Oil Spill Detection using SAR and Optical Image Fusion

## Overview

Oil spills pose a significant threat to marine ecosystems, coastal infrastructure, and global maritime activities. Traditional monitoring approaches are expensive, slow, and highly dependent on environmental conditions.

This project presents a **multimodal deep learning framework** for automated oil spill detection and segmentation by combining:

* **Synthetic Aperture Radar (SAR) Sentinel-1 imagery**
* **Optical Sentinel-2 imagery**

The framework leverages **U-Net-based semantic segmentation models** trained independently on SAR and Optical datasets and combines their predictions using fusion techniques to improve detection accuracy and reduce false alarms.

---

## Key Features

* Automated oil spill segmentation using Deep Learning
* Multimodal fusion of SAR and Optical satellite imagery
* U-Net based segmentation models
* Support for Sentinel-1 and Sentinel-2 datasets
* Pixel-wise probability and binary mask generation
* Quantitative performance evaluation
* Visualization and overlay generation
* Scalable framework for environmental monitoring

---

## Project Objectives

* Develop an automated oil spill monitoring system.
* Train segmentation models on SAR and Optical datasets independently.
* Generate oil spill probability maps and binary masks.
* Fuse predictions from multiple modalities.
* Improve segmentation accuracy compared to single-sensor approaches.
* Enable scalable marine disaster monitoring and response.

---

## Datasets Used

### 1. MADOS Dataset (Sentinel-2 Optical)

* Multi-spectral optical imagery
* Pixel-level oil spill annotations
* RGB composites generated from Sentinel-2 bands
* Used for Optical U-Net training

### 2. DARTIS Dataset (Sentinel-1 SAR)

* SAR image patches
* XML-based oil spill annotations
* Masks generated from annotations
* Used for SAR U-Net training

---

## Methodology

### Phase 1: Data Acquisition & Preprocessing

#### Optical Data

* RGB image generation
* Image resizing to 256 × 256
* Normalization to [0,1]
* Mask validation

#### SAR Data

* Sigma0 conversion
* Speckle noise reduction
* Percentile normalization
* Mask generation from XML annotations
* Image resizing to 256 × 256

---

### Phase 2: Segmentation Model Training

#### U-Net for Optical Images

The Optical model learns:

* Oil spill boundaries
* Spectral characteristics
* Shape information

#### U-Net for SAR Images

The SAR model learns:

* Surface texture variations
* Oil-induced dark formations
* Weather-independent spill patterns

#### Training Configuration

* Loss Function: BCE + Dice Loss
* Optimizer: Adam
* Learning Rate: 1e-3
* Early Stopping
* ReduceLROnPlateau Scheduler

---

### Phase 3: Multimodal Fusion

Predictions from SAR and Optical models are fused using probability averaging:

[
P_{fused} = \frac{P_{SAR} + P_{Optical}}{2}
]

Fusion Steps:

1. Generate probability maps
2. Align spatial dimensions
3. Average pixel-wise probabilities
4. Apply threshold (0.5)
5. Generate final binary segmentation mask

---

## Architecture

### High-Level Pipeline

Dataset Collection
↓
Preprocessing
↓
SAR U-Net Training
+
Optical U-Net Training
↓
Probability Map Generation
↓
Fusion Module
↓
Binary Mask Generation
↓
Performance Evaluation

---

## Evaluation Metrics

The framework is evaluated using:

* Intersection over Union (IoU)
* Dice Score
* Precision
* Recall
* F1 Score

---

## Results

| Model                 | IoU                 | Dice  | Precision | Recall |
| --------------------- | ------------------- | ----- | --------- | ------ |
| MADOS U-Net (Optical) | ~0.65               | ~0.75 | ~0.80     | ~0.65  |
| DARTIS U-Net (SAR)    | High Background IoU | ~0.60 | 0.98      | 0.99   |
| Fused Prediction      | ~0.80               | ~0.82 | ~0.70     | ~0.80  |

### Key Findings

* SAR performs well in all-weather conditions.
* Optical imagery provides accurate spill boundaries.
* Fusion improves segmentation completeness.
* Fused predictions outperform individual modalities.
* Recall and IoU increase significantly after fusion.

---

## Advantages of Multimodal Fusion

### SAR Strengths

* Day/Night operation
* All-weather capability
* Strong spill detection

### SAR Limitations

* Speckle noise
* False positives
* Wave shadow confusion

### Optical Strengths

* Clear boundaries
* Spectral discrimination
* Realistic spill shapes

### Optical Limitations

* Cloud cover sensitivity
* Lighting dependency
* Sunglint effects

### Fusion Benefits

* Reduced false positives
* Improved boundary accuracy
* Higher recall
* Better segmentation consistency

---

## Repository Structure

```text
├── data/
│   ├── MADOS/
│   └── DARTIS/
│
├── preprocessing/
│   ├── optical_preprocessing.py
│   └── sar_preprocessing.py
│
├── models/
│   ├── unet_optical.py
│   ├── unet_sar.py
│   └── trained_weights/
│
├── fusion/
│   ├── probability_fusion.py
│   └── hybrid_fusion.py
│
├── evaluation/
│   ├── metrics.py
│   └── visualization.py
│
├── results/
│   ├── predictions/
│   ├── overlays/
│   └── metrics/
│
└── README.md
```

---

## Applications

* Marine Environmental Monitoring
* Offshore Oil Spill Detection
* Coastal Surveillance
* Disaster Management
* Maritime Safety Systems
* Real-Time Monitoring Platforms

---

## Limitations

* Limited SAR training samples
* Severe class imbalance
* Lack of paired SAR-Optical datasets
* Simple averaging fusion strategy
* Sensor-specific noise and artifacts
* Limited deployment validation

---

## Future Work

* Feature-level multimodal fusion
* Attention-based fusion mechanisms
* Transformer-based architectures (SegFormer, Swin-UNet)
* Multi-temporal SAR analysis
* Hyperspectral data integration
* Real-time deployment pipelines
* Transfer learning on large-scale satellite datasets

---

## Technology Stack

* Python
* PyTorch
* TensorFlow / Keras
* OpenCV
* NumPy
* Matplotlib
* Rasterio
* GDAL

---

## Authors

* Chetana Gaitonde
* Dr. Vishwanath Karad's MIT World Peace University (MIT-WPU)

---

## Citation

If you use this work in your research, please cite:

Gaitonde, C. (2025).  
*Multimodal Oil Spill Detection using SAR and Optical Image Fusion*.  
Capstone Project, MIT World Peace University (MIT-WPU), Pune, India.

---
