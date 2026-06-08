# Fingerprint Analysis — Altered Fingerprint Classification
### Machine Learning Workflow for Forensic Biometric Analysis

![Python](https://img.shields.io/badge/Python-3.x-blue) ![scikit-learn](https://img.shields.io/badge/scikit--learn-1.0+-orange) ![OpenCV](https://img.shields.io/badge/OpenCV-4.x-green) ![Dataset](https://img.shields.io/badge/Dataset-SOCOFing-purple) ![Best Accuracy](https://img.shields.io/badge/Best%20Accuracy-53.3%25%20SVM-brightgreen)

> A classical machine learning workflow for classifying altered fingerprint patterns using the SOCOFing dataset, evaluating k-NN, SVM, and Decision Tree classifiers for forensic biometric applications.

---

## Overview

This project implements a complete machine learning pipeline for fingerprint classification, focusing on **altered fingerprint categories**. Three classical classifiers are trained and evaluated to distinguish between:

- **Altered-Easy** — Arch pattern fingerprints
- **Altered-Medium** — Loop pattern fingerprints
- **Altered-Hard** — Whorl pattern fingerprints

The study benchmarks classifier performance and discusses implications for biometric security and forensic investigation.

---

## Dataset

| Property | Details |
|----------|---------|
| Source | SOCOFing (Kaggle) |
| Total Images | 23,360 |
| Classes | Altered-Easy (Arch), Altered-Medium (Loop), Altered-Hard (Whorl) |
| Organization | Images stored in subfolders by class |
| Test Set | 30 images (10 per class) |

**Why SOCOFing?** Publicly available, well-structured, and suitable for fingerprint classification tasks — making it ideal for evaluating classical ML approaches.

---

## Preprocessing Pipeline

1. **Resize** — all images resized to 128×128 pixels
2. **Grayscale conversion** — strips color for uniformity
3. **Normalization** — pixel values scaled to 0–1 range
4. **Optional thresholding** — enhances ridge visibility
5. **Flattening** — each image converted to a 16,384-dimensional feature vector (128×128) for classifier input

---

## Features Used

- Raw pixel intensity values from normalized grayscale images
- Each image represented as a flattened vector of **16,384 values**
- Captures ridge flow and texture patterns
- Simple, interpretable, and compatible with classical classifiers

---

## Models

| Model | Description |
|-------|-------------|
| **k-NN (k=3)** | Classifies based on similarity to nearest neighbors |
| **SVM (linear kernel)** | Constructs optimal hyperplanes for class separation in high-dimensional space |
| **Decision Tree** | Splits data on feature thresholds — interpretable but prone to overfitting |

---

## Results

### Classifier Accuracy Comparison

| Model | Accuracy |
|-------|---------|
| k-NN (k=3) | 36.7% |
| **SVM (linear)** | **53.3%** ✅ Best |
| Decision Tree | 40.0% |

### Classification Report (Decision Tree)

| Class | Precision | Recall | F1-Score | Support |
|-------|-----------|--------|----------|---------|
| Altered-Easy | 0.45 | 0.50 | 0.48 | 10 |
| Altered-Medium | 0.33 | 0.33 | 0.33 | 9 |
| Altered-Hard | 0.40 | 0.36 | 0.38 | 11 |
| **Overall** | **0.40** | **0.40** | **0.40** | **30** |

### Key Observations
- **SVM** achieved the best accuracy (53.3%) due to its strength in high-dimensional feature spaces
- **Altered-Easy** fingerprints were classified most reliably across all models
- **Misclassifications** were concentrated between Altered-Medium and Altered-Hard — reflecting the difficulty of distinguishing subtle alteration

---

## Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/fingerprint-analysis.git
cd fingerprint-analysis

# Install dependencies
pip install -r requirements.txt
```

---

## Requirements

```
opencv-python>=4.5
scikit-learn>=1.0
numpy>=1.21
matplotlib>=3.5
seaborn>=0.11
pandas>=1.3
```

---

## Usage

### Preprocess Images
```python
from src.preprocess import preprocess_images

X, y = preprocess_images("data/", image_size=(128, 128))
```

### Train & Evaluate
```bash
python src/train.py --data_dir ./data --model svm
```

### Visualize Results
```bash
python src/visualize.py --results_path ./outputs/experiment_log.csv
```

---

## Experimental Logs

| Timestamp | Model | Parameters | Accuracy |
|-----------|-------|-----------|---------|
| 2026-03-17 21:23:09 | k-NN | n_neighbors=3 | 36.7% |
| 2026-03-17 21:23:10 | SVM | kernel=linear | 53.3% |

---

## Discussion

**Preprocessing:** Standardization improved classifier stability across all models.

**SVM** excelled in high-dimensional separation — raw pixel vectors (16,384 features) suit margin-based classifiers well.

**k-NN** was sensitive to local variations in ridge patterns, leading to the lowest accuracy.

**Decision Tree** was interpretable but overfit on the small test set.

---

## Limitations

- Small dataset size restricts generalization
- Raw pixel intensities used — advanced descriptors (Gabor filters, minutiae points) not implemented
- Only classical ML models tested — CNNs likely to yield significantly higher accuracy
- No cross-validation applied due to dataset size

---

## Future Work

- [ ] Advanced feature extraction (Gabor filters, minutiae-based descriptors)
- [ ] Deep learning approaches (CNN, ResNet)
- [ ] Dataset expansion and data augmentation
- [ ] Cross-validation for more robust evaluation
- [ ] Deployment as a biometric verification module

---

## Author

**Laiba Maqbool**

---

## License

MIT License © 2026 Laiba Maqbool

---

## References

- **Dataset:** SOCOFing — Sokoto Coventry Fingerprint Dataset, Kaggle
- **Libraries:** Python, OpenCV, scikit-learn, matplotlib, seaborn, pandas
- **Tool:** Google Colab
