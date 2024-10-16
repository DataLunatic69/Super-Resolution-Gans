# Super Resolution Image Generation Project

## Overview
This project implements a Super Resolution Generative Adversarial Network (SRGAN) to enhance the quality of low-resolution images by generating high-resolution versions. The SRGAN architecture leverages deep learning techniques to improve image resolution while preserving details and minimizing artifacts.

## Table of Contents
- [Features](#features)
- [Installation](#installation)
- [Dataset](#dataset)
- [Usage](#usage)
- [Training](#training)
- [Evaluation](#evaluation)
- [Results](#results)
- [Contributing](#contributing)
- [License](#license)

## Features
- Super resolution using SRGAN architecture
- Custom PSNR metric for evaluation
- Random cropping for data augmentation
- Checkpoint saving for model training progress

## Installation

### Prerequisites
Ensure you have the following installed:
- Python 3.x
- TensorFlow
- OpenCV
- PIL (Pillow)
- NumPy
- Matplotlib
- scikit-image

### Clone the Repository
```bash
git clone https://github.com/yourusername/super-resolution-project.git
cd super-resolution-project
```

### Install Dependencies
```bash
pip install -r requirements.txt
```

## Dataset
The project uses the [DIV2K](https://data.vision.ee.ethz.ch/cvl/DIV2K/) dataset, which includes high-resolution (HR) and low-resolution (LR) images. The dataset structure is as follows:

```
dataset/
│
├── LR/
│   ├── DIV2K_train_LR_bicubic/
│   └── DIV2K_valid_LR_bicubic/
│
└── HR/
    └── DIV2K_valid_HR/
```

### Downloading the Dataset
To download the DIV2K dataset, visit the link above and place the images in the appropriate folders.

## Usage
### Load and Preprocess Data
Before training, ensure the images are preprocessed. Use the provided functions to load and crop images:
```python
from data_utils import random_crop

# Load images
lr_img, hr_img = load_images(...)
lr_crop, hr_crop = random_crop(lr_img, hr_img)
```

### Train the Model
Train the model using the provided training script:
```bash
python train.py --epochs 50 --batch_size 16
```

### Evaluate the Model
Evaluate the model’s performance on the validation set:
```bash
python evaluate.py
```

## Training
The model is trained using the following parameters:
- **Optimizer**: Adam
- **Loss Function**: Mean Squared Error (MSE)
- **Metrics**: Custom PSNR

### Save Checkpoints
Model checkpoints are automatically saved after each epoch. The training script includes a callback to manage checkpointing:
```python
from tensorflow.keras.callbacks import ModelCheckpoint

checkpoint_callback = ModelCheckpoint(filepath='weights/srganGenerator.h5', save_best_only=True)
```

## Evaluation
After training, evaluate the model using Peak Signal-to-Noise Ratio (PSNR) and Structural Similarity Index (SSIM) metrics. Average scores for the model and bicubic interpolation are calculated and displayed.

```python
print(f"Average SSIM for SRGAN is: {average_ssim}")
print(f"Average PSNR for SRGAN is: {average_psnr}")
```

## Results
The model produces improved high-resolution images compared to the original low-resolution inputs. The evaluation metrics are displayed in graphical form using Matplotlib.

```python
import matplotlib.pyplot as plt

# Plotting PSNR and SSIM results
plt.bar(labels, avg_PSNR_values, color='orange')
plt.title('PSNR Comparison')
plt.ylabel('PSNR Value')
plt.show()
```

## Contributing
Contributions are welcome! Please fork the repository and submit a pull request.

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

For more detailed instructions, check the [Wiki](https://github.com/yourusername/super-resolution-project/wiki) or reach out via issues for any questions.
