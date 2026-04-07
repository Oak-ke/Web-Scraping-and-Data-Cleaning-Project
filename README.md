# Handwritten Digit Recognition (MNIST)

[](https://www.python.org/downloads/)
[](https://www.tensorflow.org/)
[](https://www.google.com/search?q=LICENSE)

An end-to-end deep learning project implementing and comparing neural network architectures for digit classification. This project achieves up to **99.2% accuracy** using Convolutional Neural Networks.

## Project Overview

This repository demonstrates a complete machine learning workflow—from raw data preprocessing to model deployment. We compare two primary architectures:

  * **Simple Dense Network:** A baseline fully connected model (98.0% accuracy).
  * **CNN:** A spatial-aware architecture optimized for image features (99.2% accuracy).

### Key Features

  * **Production-Ready:** Exported models in `.h5` and `.tflite` formats.
  * **Deep Analytics:** Comprehensive visualization of loss, accuracy, and confusion matrices.
  * **Robust Pipeline:** Includes normalization, one-hot encoding, and data augmentation.

-----

## Model Architectures

### 1\. Simple Dense Network

A lightweight, fully connected model for quick inference.

> **Total Params:** \~105,000
> `Input (784) → Dense(128, ReLU) → Dropout(0.2) → Dense(64, ReLU) → Output(10, Softmax)`

### 2\. Convolutional Neural Network (CNN)

The "Gold Standard" for image tasks, using spatial hierarchy.

> **Total Params:** \~1.2 Million
> `Input (28×28×1) → [Conv2D → MaxPool → BatchNorm] × 3 → Flatten → Dense(128) → Output(10)`

-----

## Performance Benchmarks

| Model | Accuracy | Loss | Parameters | Training Time |
| :--- | :--- | :--- | :--- | :--- |
| Simple Dense | 98.0% | 0.07 | 105K | \~2 min |
| **CNN (Winner)** | **99.2%** | **0.03** | **1.2M** | **\~5 min** |

### Visual Insights

**Common Misclassifications:**

  * **4 ↔ 9:** Curved vs. closed loops often confuse the feature maps.
  * **7 ↔ 1:** Dependent on the presence of a cross-stroke on the 7.

-----

## Quick Start

### 1\. Installation

```bash
# Clone the repo
git clone https://github.com/YOUR_USERNAME/mnist-digit-recognition.git
cd mnist-digit-recognition

# Install requirements
pip install -r requirements.txt
```

### 2\. Usage

```python
from tensorflow import keras
import numpy as np

# Load trained model
model = keras.models.load_model('models/mnist_cnn_classifier.h5')

# Predict
image = x_test[0].reshape(1, 28, 28, 1)
prediction = np.argmax(model.predict(image))
print(f"Predicted Digit: {prediction}")
```

-----

## Project Structure

```text
mnist-digit-recognition/
├── models/               # Saved .h5 and .tflite weights
├── images/               # Performance plots and sample visuals
├── mnist_recognition.ipynb # Main development notebook
├── requirements.txt      # Dependency list
└── LICENSE               # MIT License
```

-----

## Key Insights & Learnings

  * **Normalization:** Scaling pixel values to $[0, 1]$ improved convergence speed by nearly 3x.
  * **Regularization:** Dropout was essential in the CNN to prevent the 1.2M parameters from over-memorizing the training set.
  * **Real-world Use:** These models serve as the backbone for technologies like **postal mail sorting**, **bank check processing**, and **automated form digitization**.

-----

## Contributing

Contributions make the open-source community an amazing place to learn\!

1.  Fork the Project
2.  Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3.  Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4.  Push to the Branch (`git push origin feature/AmazingFeature`)
5.  Open a Pull Request
