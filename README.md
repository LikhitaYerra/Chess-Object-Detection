
# Chess Piece Detection with YOLOv5 ♟️🤖

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![PyTorch](https://img.shields.io/badge/PyTorch-1.8+-orange.svg)
![YOLOv5](https://img.shields.io/badge/YOLOv5-s-red.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen.svg)

---

## 🌟 Project Overview

**Chess Piece Detection with YOLOv5** is a computer vision project by **Likhita Yerra**, **Baptiste**, and **Shafiya**, aimed at building a robust system to detect and classify 12 distinct chess pieces (6 types × 2 colors) using the YOLOv5 model. Trained on a dataset of 1,592 images with 30,400 annotated instances, our model achieved an impressive **mAP@0.5 of 0.993**, showcasing high accuracy and reliability for chess analysis applications.

---

## ✨ Features

- **Piece Detection**: Identifies all 12 chess pieces (pawns, knights, bishops, rooks, queens, kings) in black and white.
- **High Accuracy**: Achieves >98% precision and recall across all classes.
- **Efficient Model**: Compact (14.5 MB) with fast inference (1.63 it/s).
- **Robust Training**: 100 epochs with early stopping, optimized on CUDA-enabled GPU.
- **Visual Insights**: Detailed metrics, loss curves, and class-specific performance analysis.

---

## 🚀 Installation

### Prerequisites

- **Python**: 3.8+
- **CUDA-enabled GPU**: For training/inference (optional but recommended)
- **Roboflow API Key**: For dataset access
- **Dependencies**: Listed in `requirements.txt`

### Dependencies

```plaintext
torch>=1.8.0
torchvision>=0.9.0
roboflow>=1.1.50
opencv-python-headless>=4.10.0
matplotlib>=3.8.0
pandas>=2.2.2
numpy>=1.26.4
pyyaml>=6.0.2
tqdm>=4.67.1
```

### Setup Steps

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/[YourUsername]/Chess-Piece-Detection-YOLOv5.git
   cd Chess-Piece-Detection-YOLOv5
   ```

2. **Install Dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

3. **Set Up YOLOv5**:
   ```bash
   git clone https://github.com/ultralytics/yolov5
   cd yolov5
   pip install -r requirements.txt
   cd ..
   ```

4. **Download Dataset**:
   - Use Roboflow to fetch the dataset:
     ```python
     from roboflow import Roboflow
     rf = Roboflow(api_key="YtltN9DWSK5AO0rygbyg")
     project = rf.workspace("chess-piece-detection-lydqy").project("chess-piece-detection-5ipnt")
     dataset = project.version(2).download("yolov5")
     ```

5. **Verify Environment**:
   ```python
   import torch
   print(f"CUDA available: {torch.cuda.is_available()}")
   ```

---

## 🎮 Usage

### Training the Model

Run the training script with the provided configuration:
```bash
python yolov5/train.py --img 640 --batch 16 --epochs 100 --data {dataset.location}/data.yaml --weights yolov5s.pt --cache --name chess_yolov5s --patience 30
```

### Testing the Model

Detect pieces in an image:
```bash
python yolov5/detect.py --weights runs/train/chess_yolov5s/weights/best.pt --img 640 --conf 0.25 --source path/to/image.jpg
```

### Dataset Details

- **Images**: 1,592
- **Instances**: 30,400
- **Classes**: 12 (Black/White: Pawn, Knight, Bishop, Rook, Queen, King)
- **Distribution**:
  - Black Pawns: 7,351 | White Pawns: 7,387
  - Black Knights: 1,861 | White Knights: 1,985
  - Black Bishops: 1,854 | White Bishops: 1,041
  - Black Rooks: 1,823 | White Rooks: 1,969
  - Black Queens: 988 | White Queens: 1,098
  - Black Kings: 1,836 | White Kings: 1,107

---

## 📊 Performance

### Overall Metrics
- **mAP@0.5**: 0.993
- **Precision**: 0.991
- **Recall**: 0.991
- **Model Size**: 14.5 MB
- **Inference Speed**: 1.63 it/s

### Class-Specific Performance

| Class         | Precision | Recall |
|---------------|-----------|--------|
| Black Bishop  | 0.992     | 0.989  |
| Black King    | 0.994     | 0.993  |
| Black Knight  | 0.991     | 0.992  |
| Black Pawn    | 0.997     | 0.995  |
| Black Queen   | 0.984     | 0.983  |
| Black Rook    | 0.991     | 0.991  |
| White Bishop  | 0.996     | 0.996  |
| White King    | 0.991     | 0.989  |
| White Knight  | 0.994     | 0.996  |
| White Pawn    | 0.996     | 0.997  |
| White Queen   | 0.985     | 0.983  |
| White Rook    | 0.994     | 0.992  |

---

## 🛠️ Technical Details

### Training Configuration
- **Base Model**: YOLOv5s
- **Image Size**: 640×640 pixels
- **Batch Size**: 16
- **Epochs**: 100 (early stopping at 30)
- **Training Time**: 14.651 hours
- **Hardware**: CUDA-enabled GPU

### Loss Evolution
- **Training Losses**:
  - Box: 0.06 → 0.02
  - Class: 0.04 → 0.005
  - Object: 0.10 → 0.06
- **Validation Losses**:
  - Box: 0.07 → 0.02
  - Class: 0.05 → 0.004
  - Object: 0.08 → 0.05

### Key Findings
- **Strengths**:
  - >98% accuracy across all pieces
  - Robust detection for both colors
  - Strong pawn and royal piece performance
- **Areas for Improvement**:
  - Queen detection slightly lower (0.984-0.985)
  - Edge/corner positions need refinement

---

## 🌈 Future Directions

- **Dataset Expansion**: Add more queen and edge-position samples.
- **Fine-Tuning**: Optimize for corner cases.
- **Real-Time Tracking**: Enable live chessboard analysis.
- **Speed Optimization**: Boost inference for real-world use.

---

## 📂 Project Structure

```
Chess-Piece-Detection-YOLOv5/
├── yolov5/             # YOLOv5 repository
├── train.py            # Training script
├── detect.py           # Inference script
├── requirements.txt    # Dependencies
├── dataset/            # Downloaded dataset (via Roboflow)
├── runs/              # Training outputs (weights, logs)
├── LICENSE            # MIT License
└── README.md          # This file
```

---

## 🤝 Contributing

Contributions are welcome! To get started:
1. Fork the repo 🍴
2. Create a branch:
   ```bash
   git checkout -b feature-branch
   ```
3. Commit changes:
   ```bash
   git commit -m "Add feature"
   ```
4. Push:
   ```bash
   git push origin feature-branch
   ```
5. Open a Pull Request 📬

---

## 📜 License

Licensed under the MIT License. See [LICENSE](LICENSE) for details:


---


Happy chess detecting! ♟️🚀
