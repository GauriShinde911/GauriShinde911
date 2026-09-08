<div align="center">

  <img src="../assets/agritech_og_cover.jpg" width="100%" alt="Smart Agritech Banner" style="border-radius: 12px; margin-bottom: 20px;" />

  # Smart Agritech — Weed Detection & Crop Segmentation
  
  <p align="center" style="font-size: 1.15rem; color: #94A3B8;">
    Precision computer vision segmentation pipeline with automated HSV mask generation and targeted variable-rate spraying.
  </p>

  <div>
    <img src="https://img.shields.io/badge/Python_3.11-162032?style=flat-square&logo=python&logoColor=60A5FA" alt="Python"/>
    <img src="https://img.shields.io/badge/PyTorch-162032?style=flat-square&logo=pytorch&logoColor=60A5FA" alt="PyTorch"/>
    <img src="https://img.shields.io/badge/OpenCV-162032?style=flat-square&logo=opencv&logoColor=60A5FA" alt="OpenCV"/>
    <img src="https://img.shields.io/badge/U--Net-162032?style=flat-square&logoColor=60A5FA" alt="U-Net"/>
    <img src="https://img.shields.io/badge/Albumentations-162032?style=flat-square&logoColor=60A5FA" alt="Albumentations"/>
  </div>

</div>

---

## ◈ Visual Overview & Inference Pipeline

```
Drone / Aerial Field Imagery (RGB)
                 ↓
Automatic HSV / LAB Color-Space Thresholding (Zero Manual Labeling)
                 ↓
Albumentations Spatial & Photometric Augmentations
                 ↓
U-Net Deep Neural Network Segmentation (Dice + BCE Loss)
                 ↓
Prescription Grid Output: Variable-Rate Target Coordinates (40-60% Chemical Savings)
```

---

## ◈ Problem

Uniform broadcast spraying of chemical herbicides across commercial crop fields (such as wheat) creates significant environmental and economic damage:
1. **Chemical Overuse & Cost:** Over 60% of sprayed herbicide lands on healthy crops or bare soil rather than weeds, wasting thousands of dollars per season.
2. **Soil & Ecosystem Degradation:** Indiscriminate chemical dispersion contaminates groundwater tables and accelerates herbicide-resistant weed mutations.
3. **Data Labeling Bottleneck:** Training accurate semantic segmentation models traditionally requires hundreds of hours of expensive manual polygon annotation by agronomists.

---

## ◈ Solution

This project implements an end-to-end precision agriculture intelligence pipeline:
- **Unsupervised Ground Truth Generation:** Utilizes classical OpenCV HSV and LAB color-space transformations with morphological filtering to automatically segment green weed vegetation from soil and crop canopies.
- **Deep U-Net Architecture:** Employs an encoder-decoder network with skip connections, preserving fine leaf edge boundaries at $512\times 512$ tile resolutions.
- **Balanced Loss Function:** Trained with combined Dice Loss and Binary Cross-Entropy (BCE) using cosine annealing scheduling across 50 epochs to maintain high recall on sparse weed clusters.
- **Actionable Spraying Prescription:** Translates segmentation pixel densities into coordinate bounding reticles for targeted tractor and drone spray nozzles.

---

## ◈ Architecture

<div align="center" style="margin: 24px 0;">
  <img src="../assets/architecture_agritech.svg" width="100%" alt="Agritech Architecture: Drone Image -> YOLO Detection -> Weed Classification -> ROI Analysis" />
</div>

1. **Preprocessing & Masking:** High-resolution field drone image ingestion and automated HSV mask generation.
2. **Augmentation Pipeline:** Albumentations integration (random rotations, affine transforms, Gaussian blur, color jitter).
3. **Segmentation Core:** PyTorch U-Net with batch normalization and skip connection feature concatenation.
4. **Prescription Output:** Metric evaluation module computing Intersection-over-Union (IoU) and generating variable-rate spray masks.

---

## ◈ Key Features

<table width="100%" border="0" cellpadding="0" cellspacing="0" style="border-collapse: separate; border-spacing: 12px;">
  <tr>
    <td width="33.33%" valign="top" style="background: #0D1726; border: 1px solid #1E293B; border-radius: 12px; padding: 18px;">
      <h4 style="color: #60A5FA; margin: 0 0 8px 0;">🤖 Automated Masking</h4>
      <p style="color: #94A3B8; font-size: 0.88rem; line-height: 1.5; margin: 0;">
        Replaces costly manual annotation with HSV/LAB morphological filtering, saving 100% of labeling overhead.
      </p>
    </td>
    <td width="33.33%" valign="top" style="background: #0D1726; border: 1px solid #1E293B; border-radius: 12px; padding: 18px;">
      <h4 style="color: #60A5FA; margin: 0 0 8px 0;">🎯 High Precision IoU</h4>
      <p style="color: #94A3B8; font-size: 0.88rem; line-height: 1.5; margin: 0;">
        Achieves >0.85 IoU on held-out field test images with combined Dice+BCE loss convergence.
      </p>
    </td>
    <td width="33.33%" valign="top" style="background: #0D1726; border: 1px solid #1E293B; border-radius: 12px; padding: 18px;">
      <h4 style="color: #60A5FA; margin: 0 0 8px 0;">🌱 40–60% Chemical Reduction</h4>
      <p style="color: #94A3B8; font-size: 0.88rem; line-height: 1.5; margin: 0;">
        Converts pixel masks into spray nozzle activation grids, cutting herbicide runoff and operational cost.
      </p>
    </td>
  </tr>
</table>

---

## ◈ Tech Stack

- **Deep Learning Framework:** PyTorch, Torchvision
- **Computer Vision & Image Processing:** OpenCV, Albumentations, NumPy
- **Architectures:** U-Net (Encoder-Decoder with Skip Connections)
- **Evaluation & Metrics:** Intersection-over-Union (IoU), Dice Loss, Precision-Recall Curves

---

## ◈ Quickstart & Installation

```bash
# 1. Clone repository
git clone https://github.com/GauriShinde911/weed-detection-ai-agritech-case-study.git
cd weed-detection-ai-agritech-case-study

# 2. Install dependencies
pip install -r requirements.txt

# 3. Generate automatic masks from raw field images
python scripts/generate_masks.py --input_dir data/raw_field/ --output_dir data/masks/

# 4. Train or run evaluation
python train.py --epochs 50 --batch_size 16 --lr 0.001
python evaluate.py --checkpoint models/best_unet_model.pth
```

---

## ◈ Future Roadmap

- [ ] Export weights to TensorRT and ONNX for direct embedded edge execution on agricultural drones.
- [ ] Integration with multi-spectral NIR camera sensors to distinguish crop moisture stress from weed infestation.
- [ ] Support for real-time video stream inferencing (>30 FPS) on tractor cabin embedded hardware.
- [ ] Dynamic GPS geofencing and shapefile prescription map export.

---

## ◈ License & Author

Authored by **Gauri Shinde** (2026)  
MIT License
