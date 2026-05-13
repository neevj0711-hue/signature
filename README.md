# Signature Presence Detection — YOLOv8

## Description
This project detects the **presence or absence of a signature** in document images using a YOLOv8 object detection model. It can be used to automatically verify whether a document has been signed, making it useful for:
- Document verification pipelines
- Automated form processing
- Digital signature validation
- Administrative workflows

The model is trained on the **Rugwed Neev Signature Presence dataset (v3)** and exported to TFLite for mobile deployment via the Ultralytics YOLO app.

---

## Installation

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

## Usage

### Detect signature in a single image
```bash
python detect.py --input your_document.jpg
```

### Detect signature in a folder of images
```bash
python detect.py --input ./documents/
```

### Example Python usage
```python
from ultralytics import YOLO

model = YOLO('best.pt')

results = model.predict(
    source='document.jpg',
    conf=0.5,
    save=True
)

for result in results:
    if len(result.boxes) > 0:
        print(f"✅ Signature FOUND! Confidence: {result.boxes.conf[0]:.2f}")
    else:
        print("❌ No signature detected")
```

---

## Project Structure

```
signature-detection/
│
├── best.pt                  # Trained YOLOv8 model weights
├── best_float32.tflite      # TFLite model for mobile deployment
├── data.yaml                # Dataset configuration
├── detect.py                # Detection script
├── requirements.txt         # Python dependencies
└── README.md                # This file
```

---

## Model Details

This project uses a **YOLOv8n (nano)** model fine-tuned for signature presence detection.

### Dataset
- **Name:** Rugwed Neev Signature Presence
- **Version:** v3
- **Source:** [Roboflow Universe](https://universe.roboflow.com/rugwed/rugwed-neev-signature-presence/dataset/3)
- **Classes:** 1 (`signature`)
- **License:** CC BY 4.0

### Training Parameters

| Parameter | Value |
|-----------|-------|
| Base Model | `yolov8n.pt` |
| Epochs | 50 |
| Image Size | 640 x 640 |
| Batch Size | 16 |
| Optimizer | AdamW (auto) |
| Framework | Ultralytics YOLOv8 |

### Performance Metrics

| Metric | Value |
|--------|-------|
| **Precision** | 0.749 |
| **Recall** | 0.755 |
| **mAP50** | **0.805** |
| **mAP50-95** | 0.611 |
| **Fitness Score** | 0.610 |

### Exported Models

| Format | File | Size | Use Case |
|--------|------|------|----------|
| PyTorch | `best.pt` | ~6 MB | PC / Server |
| TFLite | `best_float32.tflite` | 11.7 MB | Mobile / Edge |

---

## Mobile Deployment

The TFLite model can be used with the **Ultralytics YOLO mobile app**:

1. Upload `best.pt` to [Ultralytics HUB](https://hub.ultralytics.com)
2. Download the **YOLO app** on Android or iOS
3. Sign in and select your signature model
4. Point camera at any document to detect signatures in real time!

---

## License

This project is licensed under the **MIT License** — see the [LICENSE.md](LICENSE.md) file for details.

Dataset is licensed under **CC BY 4.0** by Rugwed (Roboflow Universe).

---

## Acknowledgements
- [Ultralytics YOLOv8](https://github.com/ultralytics/ultralytics)
- [Roboflow](https://roboflow.com) for dataset management
- Dataset by [Rugwed on Roboflow Universe](https://universe.roboflow.com/rugwed/rugwed-neev-signature-presence/dataset/3)
