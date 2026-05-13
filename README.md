<div align="center">

# ✍️ Signature Presence Detection

### Real-time signature detection in documents using YOLOv8

![Python](https://img.shields.io/badge/Python-3.8+-blue?style=for-the-badge&logo=python&logoColor=white)
![YOLOv8](https://img.shields.io/badge/YOLOv8-Ultralytics-purple?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)
![mAP50](https://img.shields.io/badge/mAP50-88.5%25-orange?style=for-the-badge)

</div>

---

## 📌 Overview

This project automatically detects whether a **signature is present** in a document image using a fine-tuned **YOLOv8s** object detection model. It solves the problem of manually checking documents for signatures — useful in:

- 📄 Document verification pipelines
- 🏢 Administrative & HR workflows
- 🖊️ Automated form processing
- 📱 Mobile document scanning apps

The model is trained on the **Rugwed Neev Signature Presence dataset (v3)** and exported to **TFLite** for mobile deployment.

---

## 📊 Model Performance

| Metric | Value |
|--------|-------|
| 🎯 Precision | 0.873 |
| 🔁 Recall | 0.861 |
| ✅ **mAP50** | **0.885** |
| 📈 mAP50-95 | 0.724 |
| 💪 Fitness Score | 0.851 |

---

## 🚀 Installation

### Prerequisites
- Python 3.8+
- pip

### Clone & Install

```bash
git clone https://github.com/yourusername/signature-detection.git
cd signature-detection
pip install -r requirements.txt
```

### requirements.txt
```
ultralytics
opencv-python
Pillow
```

---

## 💻 Usage

### Detect signature in a single image
```bash
python detect.py --input your_document.jpg
```

### Detect signature in a folder
```bash
python detect.py --input ./documents/
```

### Python example
```python
from ultralytics import YOLO

# Load trained model
model = YOLO('best.pt')

# Run detection
results = model.predict(
    source='document.jpg',
    conf=0.5,
    save=True
)

# Check result
for result in results:
    if len(result.boxes) > 0:
        print(f"✅ Signature FOUND! Confidence: {result.boxes.conf[0]:.2f}")
    else:
        print("❌ No signature detected")
```

---

## 🗂️ Project Structure

```
signature-detection/
│
├── 📦 best.pt                  # Trained YOLOv8 model weights
├── 📱 best_float32.tflite      # TFLite model for mobile
├── ⚙️  data.yaml               # Dataset configuration
├── 🐍 detect.py                # Detection script
├── 📋 requirements.txt         # Python dependencies
└── 📖 README.md                # This file
```

---

## 🧠 Model Details

### Training Parameters

| Parameter | Value |
|-----------|-------|
| Base Model | `yolov8s.pt` |
| Epochs | 100 |
| Image Size | 640 × 640 |
| Batch Size | 8 |
| Optimizer | AdamW (auto) |
| Framework | Ultralytics YOLOv8 |

### Dataset

| Property | Value |
|----------|-------|
| Name | Rugwed Neev Signature Presence |
| Version | v3 |
| Classes | 1 (`signature`) |
| License | CC BY 4.0 |

### Exported Formats

| Format | File | Size | Use Case |
|--------|------|------|----------|
| PyTorch | `best.pt` | ~22 MB | PC / Server |
| TFLite | `best_float32.tflite` | 11.7 MB | Mobile / Edge |

---

## 📱 Mobile Deployment

Use the TFLite model with the **Ultralytics YOLO mobile app**:

1. Upload `best.pt` to [Ultralytics HUB](https://hub.ultralytics.com)
2. Download the **YOLO app** on Android or iOS
3. Sign in and select your signature model
4. Point your camera at any document — signatures detected in **real time!** 🎉

---

## 📄 License

This project is licensed under the **MIT License** — see [LICENSE.md](LICENSE.md) for details.

Dataset licensed under **CC BY 4.0** by Rugwed.

---

## 🙏 Acknowledgements

- [Ultralytics YOLOv8](https://github.com/ultralytics/ultralytics)
- Dataset by Rugwed — Signature Presence Dataset v3

---

<div align="center">
Made with ❤️ using YOLOv8
</div>
