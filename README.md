Dental X-ray Detection using YOLOv8 and ESRGAN
This project presents a two-stage deep learning pipeline for dental radiograph analysis. It enhances dental X-ray image quality using Enhanced Super-Resolution GAN (ESRGAN) and then detects multiple dental conditions using a YOLOv8 object detection model.

🧠 Key Features
Image Enhancement: Uses ESRGAN to improve the clarity and resolution of dental X-rays.

Object Detection: Employs YOLOv8 to detect and classify six dental conditions:

Caries

Crown

Root Canal Treated (RCT)

Restoration

Normal

Badly Decayed

Web Interface: Offers a simple frontend to upload and visualize predictions.

🗃️ Dataset
Name: Dental Periapical X-rays

Source: Kaggle - Nada Aglan

Format: JPEG images (640×640) with COCO annotations

🧰 Methodology
Stage 1: Super-Resolution Enhancement
Model: ESRGAN

Enhances detail and sharpens image features to improve detection accuracy.

Stage 2: Object Detection
Model: YOLOv8 (Ultralytics)

Trained on enhanced images to identify dental conditions using bounding boxes.

📊 Results

Model	Accuracy (%)
DenseNet-121	64
YOLOv8 (mAP@0.5)	56.9
Crown detection: mAP@0.5 = 95.2%

Caries detection: mAP@0.5 = 17.4% (area for improvement)

![1](https://github.com/user-attachments/assets/1035066b-6d9a-4bfb-a370-6177cf87440f)

![2](https://github.com/user-attachments/assets/7cb5d87b-b628-45ec-8057-62079fa1a19e)

📈 Future Work
Improve detection of subtle pathologies (e.g., early-stage caries)

Integrate explainability tools (e.g., Eigen-CAM)

Explore segmentation models like YOLO-DentSeg

🛠️ Tech Stack
Python, PyTorch, OpenCV

Ultralytics YOLOv8

ESRGAN (Enhanced Super-Resolution GAN)

Albumentations for data augmentation

🚀 Getting Started
bash
Copy
Edit
# Clone the repo
git clone https://github.com/yourusername/dental-xray-yolov8-esrgan.git](https://github.com/prajwalBirwadkar/Dental-X-ray-Anomaly-Detection-System.git


# Install dependencies
pip install -r requirements.txt

# Run ESRGAN preprocessing (sample)
python enhance_images.py

# Train YOLOv8
python train.py --img 640 --batch 16 --epochs 50 --data dental.yaml --weights yolov8n.pt
