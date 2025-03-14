# Pedestrian-Pose-Estimation-and-Tracking-in-Occlusion-Prone-Environments 

### **Overview**  
This repository integrates **Pedestrian-Synthesis-GAN (PS-GAN)** with **AlphaPose** to enhance pedestrian pose estimation under occlusions and noise. The framework consists of two main components:  
1. **PS-GAN**: A Generative Adversarial Network that synthesizes occlusion-aware pedestrian images for training.  
2. **AlphaPose**: A state-of-the-art multi-person pose estimation model that utilizes the synthetic data from PS-GAN for improved keypoint detection.  

### **Repository Structure**  
```
📂 Pedestrian-Synthesis-GAN: Generating Pedestrian Data in Real Scene and Beyond  
 ├── 📂 PS-GAN/               # GAN for generating synthetic pedestrian data  
 │   ├── models/              # Generator and Discriminator architectures  
 │   ├── datasets/            # Training datasets and preprocessing scripts  
 │   ├── training.py          # GAN training script  
 │   ├── evaluation.py        # Model evaluation script  
 │   ├── utils.py             # Helper functions  
 │   ├── README.md            # Documentation for PS-GAN  
 │   ├── requirements.txt     # Dependencies for PS-GAN  
 │   └── ...  
 │  
 ├── 📂 AlphaPose/            # Multi-person pose estimation pipeline  
 │   ├── detector/            # Bounding box detection models (YOLO, Faster R-CNN)  
 │   ├── pose_estimator/      # Single-Person Pose Estimator (SPPE)  
 │   ├── transformer/         # Spatial Transformer Network (SSTN, SDTN)  
 │   ├── dataset/             # COCO, MPII dataset loading scripts  
 │   ├── train.py             # Training script for AlphaPose  
 │   ├── inference.py         # Inference and visualization script  
 │   ├── pose_nms.py          # Pose Non-Maximum Suppression (Pose NMS)  
 │   ├── README.md            # Documentation for AlphaPose  
 │   ├── requirements.txt     # Dependencies for AlphaPose  
 │   └── ...  
 │  
 ├── 📂 results/              
 │   ├── Dance output/               
 │   ├── Local Pedestrians/              
 │   ├── Pedestrian output/ 
 │   └── Running Race output/
```

---

### **Installation & Setup**  
#### **1. Clone the Repository**  
```bash
git clone https://github.com/Sam-Nathan/Pedestrian-Pose-Estimation-and-Tracking-in-Occlusion-Prone-Environments.git
cd Pedestrian-Pose-Estimation
```

#### **2. Install Dependencies**  
```bash
pip install -r requirements.txt
```

#### **3. Set Up Datasets**  
- Download the **COCO** and **MPII** datasets and place them in `AlphaPose/dataset/`.  
- Ensure training data for **PS-GAN** is available in `PS-GAN/datasets/`.  

---

### **Usage**  
#### **Train PS-GAN for Synthetic Pedestrian Data**  
```bash
cd PS-GAN
python training.py --dataset datasets/3dpw --epochs 100
```

#### **Train AlphaPose Using Generated Data**  
```bash
cd AlphaPose
python train.py --dataset dataset/coco --synthetic_data ../PS-GAN/results/
```

#### **Run Inference for Pose Estimation**  
```bash
python inference.py --input images/test.jpg --model checkpoint.pth
```

---

### **Results & Performance**  
The proposed model significantly improves pose estimation accuracy compared to the standard **AlphaPose framework**.  
- **COCO Dataset:**  
  - AlphaPose: **76.7 mAP**  
  - Our Model: **84.3 mAP**  
- **MPII Dataset:**  
  - AlphaPose: **80.3 mAP**  
  - Our Model: **86.9 mAP**  
