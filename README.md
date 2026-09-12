# 🕵️ UNMASKING THE DEEPFAKE: EXPOSING THE TRUTH BEHIND SYNTHETIC MEDIA

**An AI/ML-powered deepfake image analysis and digital-forensics assistance system using ResNet18, LSTM, colour analysis, noise analysis, grayscale analysis, and suspicious-region visualization.**

---

## 📌 Project Overview

**Unmasking the Deepfake** is an AI/ML-based image analysis project developed to investigate whether an uploaded image is likely to be **REAL** or **DEEPFAKE**.

The system combines a deep-learning pipeline with multiple image-forensics techniques to provide both a model prediction and supporting visual evidence.

The primary deep-learning architecture uses a **pretrained ResNet18 CNN** for visual feature extraction followed by an **LSTM sequence classifier**.

In addition to deep-learning prediction, the system performs:

* 🎨 Colour-space analysis
* 🔊 Noise analysis
* 🌑 Grayscale/luminance analysis
* 🔍 High-frequency analysis
* 🔥 Suspicious-region heatmap generation
* 🟥 Evidence-overlay visualization

The project provides a **Flask-based web dashboard** that allows users to upload an image and view the resulting analysis.

---

# 🎯 Project Objectives

The major objectives of this project are:

* Detect potential deepfake images using deep learning.
* Extract meaningful visual representations using ResNet18.
* Process extracted features using an LSTM architecture.
* Analyze image characteristics across multiple colour spaces.
* Identify unusual noise and high-frequency patterns.
* Analyze grayscale and luminance inconsistencies.
* Generate suspicious-region heatmaps.
* Produce visual evidence overlays.
* Provide interpretable supporting forensic scores.
* Evaluate the trained model using standard machine-learning metrics.
* Create a simple web-based interface for image analysis.
* Establish a foundation for future multi-frame video deepfake detection.

---

# ✨ Key Features

## 🤖 1. Deep Learning-Based Detection

The core detection pipeline consists of:

```text
Input Image
     ↓
Image Preprocessing
     ↓
ResNet18 CNN
     ↓
Feature Extraction
     ↓
LSTM
     ↓
Fully Connected Layers
     ↓
Sigmoid
     ↓
REAL / DEEPFAKE
```

### ResNet18

ResNet18 acts as the visual feature extractor.

It learns representations related to:

* Edges
* Textures
* Shapes
* Patterns
* Image structures
* Visual inconsistencies

### LSTM

The extracted feature representation is passed through an LSTM.

Although the current image pipeline represents an image as a one-frame sequence, the architecture provides a foundation for future temporal/multi-frame analysis.

---

# 🎨 2. Colour Forensics

The colour-analysis module examines several colour representations:

* RGB
* HSV
* LAB
* BGR

The analysis considers factors such as:

* Colour balance
* Brightness
* Saturation
* Local saturation variation
* Colour transitions
* LAB residual information
* Exposure-related characteristics

The resulting score is intended as **supporting forensic evidence**, not as an independent deepfake classifier.

---

# 🔊 3. Noise Analysis

The noise-analysis pipeline investigates image-level noise and high-frequency characteristics.

It examines:

* High-frequency residuals
* Laplacian variance
* Local noise variation
* Blockiness/compression-grid signals

These characteristics can provide additional clues about unusual image processing or inconsistencies.

---

# 🌑 4. Grayscale Analysis

The grayscale analysis examines luminance structures independently of colour.

It considers:

* Fine-scale residuals
* Coarse-scale residuals
* Laplacian information
* Local noise patterns
* Luminance inconsistencies

This creates another supporting evidence score that can be combined with other forensic signals.

---

# 🔥 5. Suspicious-Region Heatmap

The system combines multiple image-analysis signals to create a suspiciousness map.

The heatmap incorporates information from:

```text
Colour Residual
      +
High-Frequency Evidence
      +
Laplacian Information
      +
Grayscale Evidence
      ↓
Suspiciousness Map
```

The application generates:

* Heatmap visualization
* Suspicious-region map
* Red evidence overlay

The strongest **relative inconsistencies** are highlighted.

> ⚠️ A red region does **not** prove that manipulation occurred. It represents an area with stronger relative forensic inconsistency.

## Objective and Architecture

This forensic detection system analyzes images and videos as **REAL MEDIA** or **DEEPFAKE** using a hybrid deepfake-detection pipeline combining deep neural networks with multi-scale digital forensics:

1. **Learned Sequence Model (`model.py` & `models/deepfake_model.onnx`)**:
   - **ResNet-18 CNN** extracts 512-dimensional visual features from each image or video frame.
   - **LSTM sequence classifier** (hidden size 256) processes sequential frame feature vectors.
   - **Classifier Head**: `Linear(256→128) → ReLU → Dropout(0.25) → Linear(128→1) → Sigmoid`.
   - **High-Performance ONNX Runtime Engine**: The entire ResNet-LSTM pipeline is exported to ONNX (`models/deepfake_model.onnx`) for optimized, cross-platform inference.
2. **Sand-Pour Noise Blueprint & Overlay Forensics (`noise_analysis.py`)**:
   - **Sand-Pour Noise Blueprint**: Extracts multi-scale high-frequency noise residuals (median difference, Gaussian residual, Laplacian texture) and renders an architectural blueprint on a midnight Prussian navy substrate (`#030a16`). Granular sand stippling reveals generative synthesis artifacts and tampering boundaries.
   - **Pour-Sand Noise Overlay**: Simulates physical sand grains poured over the original image or frame, settling densely where local noise variance and high-frequency discrepancies concentrate.
3. **Multi-Perspective Forensics Suite**:
   - **Colour Forensics (`color_analysis.py`)**: RGB channel balance, HSV saturation/exposure, and LAB colour residuals.
   - **Grayscale Forensics (`grayscale_analysis.py`)**: Multi-scale luminance inconsistency and Laplacian edge responses.
   - **Suspicious Region Heatmap & Evidence Overlay (`heatmap.py`)**: OpenCV JET colormap and 92nd-percentile red evidence mask.
4. **Video Temporal Forensics (Max 30 FPS & 30 Separate Frames) (`preprocessing.py` & `video_forensics.py`)**:
   - Extracts up to 30 separate frames uniformly sampled across the video timeline, strictly capped at **30 FPS**.
   - Computes inter-frame temporal flickering, optical flow luminance shift, and noise variance jitter across adjacent frames.
   - Generates a frame-by-frame temporal forensic timeline.
5. **Dedicated Standalone Video Forensics Page (`/video-results/<job_id>`)**:
   - Video results are displayed on an independent, dedicated results page completely separate from the image analysis page.
   - Displays all 30 extracted frames separately in individual cards with full multi-view forensic thumbnails (Original, Sand Blueprint, Sand Overlay, Heatmap, Red Overlay) and detailed scores.
   - Interactive SVG temporal timeline chart and full-screen separate frame inspector modal with tab switching and chronological / suspicion sorting.

---

## Installation & Running

```powershell
# 1. Install dependencies
py -3.14 -m pip install -r requirements.txt

# 2. (Optional) Train or fine-tune detector on dataset/
py -3.14 train.py --epochs 10 --batch-size 8

# 3. Export model to ONNX format
py -3.14 export_onnx.py

# 4. Launch Flask web application
py -3.14 app.py

```
## CLI Inference

```powershell
# Image Analysis
py -3.14 inference.py fake/DF.jpeg

# Video Analysis (Max 30 FPS, 30 Separate Frames)
py -3.14 inference.py "video DF.mp4"

```
 
# 🌐 Web Dashboard

The project includes a **Flask web application**.

Users can:

1. Open the web dashboard.
2. Upload an image.
3. Validate the uploaded file.
4. Run the deep-learning model.
5. Perform forensic analysis.
6. View the prediction.
7. View supporting forensic scores.
8. Inspect generated visualizations.

Supported image formats include:

```text
PNG
JPG
JPEG
BMP
WEBP
```

---

# 🧠 Model Architecture

```text
                  ┌──────────────────┐
                  │    Input Image   │
                  └────────┬─────────┘
                           │
                           ▼
                  ┌──────────────────┐
                  │ Image Preprocess │
                  │   224 × 224      │
                  └────────┬─────────┘
                           │
                           ▼
                  ┌──────────────────┐
                  │     ResNet18     │
                  │  CNN Backbone    │
                  └────────┬─────────┘
                           │
                           ▼
                  ┌──────────────────┐
                  │ Visual Features  │
                  └────────┬─────────┘
                           │
                           ▼
                  ┌──────────────────┐
                  │      LSTM        │
                  │ Sequence Model   │
                  └────────┬─────────┘
                           │
                           ▼
                  ┌──────────────────┐
                  │ Fully Connected  │
                  │    Classifier    │
                  └────────┬─────────┘
                           │
                           ▼
                  ┌──────────────────┐
                  │     Sigmoid      │
                  └────────┬─────────┘
                           │
                           ▼
                  ┌──────────────────┐
                  │ REAL / DEEPFAKE  │
                  └──────────────────┘
```

---

# 🔬 Forensic Analysis Architecture

The deep-learning prediction is supplemented with independent image-level analysis:

```text
                         Input Image
                              │
              ┌───────────────┼───────────────┐
              │               │               │
              ▼               ▼               ▼
        Colour Analysis  Noise Analysis  Grayscale Analysis
              │               │               │
              └───────────────┼───────────────┘
                              │
                              ▼
                    Evidence Combination
                              │
                              ▼
                    Suspiciousness Map
                              │
                  ┌───────────┴───────────┐
                  ▼                       ▼
              Heatmap              Red Overlay
```

---

# 📂 Project Structure

```text
Unmasking_Deepfake/
│
├── app.py
├── train.py
├── inference.py
├── model.py
├── preprocessing.py
├── utils.py
│
├── color_analysis.py
├── noise_analysis.py
├── grayscale_analysis.py
├── heatmap.py
│
├── requirements.txt
│
├── dataset/
│   ├── real/
│   └── fake/
│
├── models/
│   └── deepfake_model.pth
│
├── results/
│   ├── heatmaps/
│   └── reports/
│
└── static/
    └── uploads/
```

---

# 📊 Dataset

The project expects a locally supplied dataset organized as:

```text
dataset/
│
├── fake/
│   ├── fake_001.jpg
│   ├── fake_002.jpg
│   └── ...
│
└── real/
    ├── real_001.jpg
    ├── real_002.jpg
    └── ...
```

The training pipeline uses:

```python
torchvision.datasets.ImageFolder
```

The expected classes are:

```text
fake
real
```

The exact class mapping is displayed during training.

### ⚠️ Dataset Responsibility

Only use datasets that you are legally permitted to use.

Make sure to follow:

* Dataset licensing requirements
* Copyright requirements
* Consent requirements
* Research-use restrictions
* Privacy requirements

---

# 🛠️ Technologies Used

| Technology   | Purpose                                 |
| ------------ | --------------------------------------- |
| Python       | Core programming language               |
| PyTorch      | Deep-learning framework                 |
| Torchvision  | ResNet18 and image-processing utilities |
| Flask        | Web application                         |
| OpenCV       | Image/video processing                  |
| NumPy        | Numerical computation                   |
| Pillow       | Image loading and processing            |
| Scikit-learn | Model evaluation                        |

---

# ⚙️ Installation

## 1. Clone the Repository

```bash
git clone YOUR-GITHUB-REPOSITORY-URL
cd Unmasking_Deepfake
```

## 2. Install Dependencies

```bash
python -m pip install -r requirements.txt
```

---

# 🏋️ Training the Model

Place your dataset inside:

```text
dataset/
├── fake/
└── real/
```

Then run:

```bash
python train.py --epochs 10 --batch-size 8 --learning-rate 0.0001
```

The training process performs:

```text
Dataset Loading
      ↓
Train / Validation Split
      ↓
Image Augmentation
      ↓
ResNet18 Feature Extraction
      ↓
LSTM Processing
      ↓
Binary Classification
      ↓
Validation
      ↓
Best Model Saving
```

---

# 📈 Evaluation Metrics

The training pipeline calculates:

* Accuracy
* Precision
* Recall
* F1 Score
* Confusion Matrix
* Validation Loss

The project intentionally uses **actual training results** rather than publishing invented accuracy or performance values.

After training, the compatible model is saved to:

```text
models/deepfake_model.pth
```

---

# 🌐 Running the Web Application

After training the model:

```bash
python app.py
```

Open:

```text
http://127.0.0.1:5000
```

### Application Workflow

```text
Open Dashboard
      ↓
Upload Image
      ↓
Validate File
      ↓
Preprocess
      ↓
Deep Learning Prediction
      ↓
Forensic Analysis
      ↓
Generate Heatmap
      ↓
Generate Evidence Overlay
      ↓
Display Results
```

---

# 🔍 Command-Line Inference

An image can also be analyzed directly from the command line:

```bash
python inference.py image.jpg
```

The inference system provides information such as:

```text
Prediction
Confidence
CNN Score
LSTM Score
Colour Score
Noise Score
Grayscale Score
Suspicion Score
```

Generated visualizations are stored under:

```text
results/heatmaps/
```

---

# 🖼️ Image Preprocessing

Input images are processed through the following pipeline:

```text
Original Image
      ↓
RGB Conversion
      ↓
Resize to 224 × 224
      ↓
Tensor Conversion
      ↓
ImageNet Normalization
      ↓
Model Input
```

The preprocessing module also contains reusable functionality for extracting multiple frames, providing a foundation for future video analysis.

---

# 🎥 Future Video Detection Architecture

The current project focuses primarily on image analysis.

However, the preprocessing architecture provides foundations for multi-frame analysis.

A future version can follow:

```text
Input Video
     ↓
Frame Extraction
     ↓
Frame Preprocessing
     ↓
ResNet18
     ↓
Frame-Level Features
     ↓
LSTM
     ↓
Temporal Analysis
     ↓
Video-Level Prediction
```

This can enable the system to analyze temporal inconsistencies across multiple frames.

---

# 📊 Prediction and Forensic Evidence

The project intentionally separates:

### Model Prediction

```text
REAL
or
DEEPFAKE
```

from:

### Supporting Evidence

```text
Colour Score
Noise Score
Grayscale Score
CNN/LSTM Signals
Suspicion Score
Heatmap
Evidence Overlay
```

This distinction is important because forensic signals can be affected by:

* Compression
* Lighting
* Resizing
* Image content
* Camera characteristics
* Normal editing
* Image quality

Therefore, forensic scores should not automatically be interpreted as proof of manipulation.

---

# ⚠️ Limitations

This project is an **AI/ML demonstration and forensic-assistance system**, not a definitive authenticity verification system.

Important limitations include:

* Reliable prediction requires compatible trained model weights.
* Colour analysis can be affected by lighting and compression.
* Noise characteristics vary between cameras and image-processing pipelines.
* Heatmaps indicate relative inconsistencies rather than confirmed manipulation.
* The current system is primarily designed for image analysis.
* Performance depends heavily on dataset quality and diversity.
* More extensive benchmark testing is required for real-world deployment.
* Predictions should not be treated as conclusive evidence in high-stakes situations.

When trained model weights are unavailable, the application should not present demonstration-mode output as a reliable trained-model prediction.

---

# 🚀 Future Improvements

Planned or potential improvements include:

### 🧑 Face-Aware Analysis

Focus analysis on detected facial regions rather than the entire image.

### 🎥 Multi-Frame Video Detection

Extend the system to aggregate evidence across video frames.

### 📊 Probability Calibration

Improve interpretation of model confidence.

### 🧪 Larger Benchmark Datasets

Evaluate the system on larger and more diverse datasets.

### 🔀 Source-Identity-Aware Splitting

Reduce potential data leakage by ensuring related identities/sources are separated between training and validation.

### 🔎 Explainability

Investigate and validate methods for explaining model decisions.

### ⚖️ Bias Analysis

Evaluate performance across different datasets, image conditions, and demographic or source variations where appropriate.

### 🧠 Advanced Architectures

Potential future versions could investigate stronger CNN/transformer-based architectures and temporal models.

---

# 🔐 Responsible Use

This project is intended for:

* 🎓 Educational purposes
* 🔬 Research experimentation
* 💻 AI/ML demonstrations
* 🧪 Computer-vision experimentation
* 📚 Academic project development

It should **not** be used as the sole basis for serious accusations or high-stakes decisions.

A high suspiciousness score does not necessarily mean an image is fake.

Similarly, a low suspiciousness score does not guarantee that an image is authentic.

Important conclusions should always be verified using appropriate evidence and reliable sources.

---

# 📸 Example Analysis Workflow

```text
                 UPLOAD IMAGE
                      │
                      ▼
              ┌───────────────┐
              │ File Validation│
              └───────┬───────┘
                      │
                      ▼
              ┌───────────────┐
              │ Preprocessing │
              └───────┬───────┘
                      │
          ┌───────────┴───────────┐
          │                       │
          ▼                       ▼
    Deep Learning          Forensic Analysis
          │                       │
          ▼               ┌───────┼────────┐
       ResNet18            │       │        │
          │             Colour   Noise   Grayscale
          ▼               │       │        │
         LSTM              └───────┼────────┘
          │                       │
          ▼                       ▼
     Prediction            Suspicious Map
          │                       │
          └───────────┬───────────┘
                      ▼
              Final Analysis
                      │
            ┌─────────┴─────────┐
            ▼                   ▼
        Prediction           Visual Evidence
                              │
                       ┌──────┴──────┐
                       ▼             ▼
                    Heatmap       Overlay
```

---

# 📁 Important Generated Files

The project uses dedicated directories for generated outputs.

```text
models/
└── deepfake_model.pth

results/
├── heatmaps/
└── reports/

static/
└── uploads/
```

---

# 🔧 Configuration

Important configurable parameters include:

### Training

```text
Epochs
Batch Size
Learning Rate
Validation Split
Random Seed
Image Augmentation
```

### Model

```text
ResNet18
LSTM Hidden Size
LSTM Layers
Dropout
Classifier Layers
```

### Forensic Analysis

```text
Colour Analysis
Noise Analysis
Grayscale Analysis
Suspiciousness Threshold
Heatmap Generation
```

### Flask Application

```text
Upload Directory
Allowed Extensions
Maximum Upload Size
Host
Port
```

---

# 🧪 Example Commands

### Install dependencies

```bash
python -m pip install -r requirements.txt
```

### Train

```bash
python train.py --epochs 10 --batch-size 8 --learning-rate 0.0001
```

### Run web application

```bash
python app.py
```

### Run command-line inference

```bash
python inference.py image.jpg
```

---

# 🏗️ Project Architecture Summary

The complete system can be summarized as:

```text
                    ┌────────────────────┐
                    │    User / Image    │
                    └──────────┬─────────┘
                               │
                               ▼
                    ┌────────────────────┐
                    │   Flask Dashboard  │
                    └──────────┬─────────┘
                               │
                               ▼
                    ┌────────────────────┐
                    │ Image Preprocessing│
                    └──────────┬─────────┘
                               │
                ┌──────────────┴──────────────┐
                │                             │
                ▼                             ▼
       ┌─────────────────┐          ┌──────────────────┐
       │ Deep Learning   │          │ Forensic Analysis│
       │     Pipeline    │          │     Pipeline     │
       └────────┬────────┘          └─────────┬────────┘
                │                             │
                ▼                    ┌────────┼────────┐
            ResNet18                 │        │        │
                │                  Colour   Noise   Grayscale
                ▼                    │        │        │
              LSTM                   └────────┼────────┘
                │                             │
                ▼                             ▼
           Classifier                 Suspicious Map
                │                             │
                ▼                    ┌────────┴────────┐
          REAL / FAKE                 │                 │
                │                  Heatmap          Overlay
                │                    │                 │
                └──────────────┬─────┴─────────────────┘
                               ▼
                       Analysis Dashboard
```

---

# 💡 What Makes This Project Different?

Instead of relying only on a binary classifier, this project attempts to provide **multiple complementary forms of evidence**.

```text
                 Deep Learning
                      │
                      ▼
                 ResNet18 + LSTM
                      │
                      │
       ┌──────────────┼──────────────┐
       │              │              │
       ▼              ▼              ▼
     Colour         Noise        Grayscale
    Analysis       Analysis      Analysis
       │              │              │
       └──────────────┼──────────────┘
                      ▼
              Suspicious Regions
                      │
             ┌────────┴────────┐
             ▼                 ▼
          Heatmap           Overlay
```

This makes the project more suitable for demonstrating the intersection of:

**Artificial Intelligence + Computer Vision + Image Forensics + Explainability**

---

# 📚 Learning Outcomes

Through this project, the following concepts are demonstrated:

* Python programming
* Deep learning
* Convolutional neural networks
* ResNet architectures
* Transfer learning
* LSTM networks
* Binary classification
* Image preprocessing
* Computer vision
* Colour-space transformations
* Image-noise analysis
* Grayscale image analysis
* Heatmap generation
* Model evaluation
* Flask web development
* Command-line inference
* Dataset organization
* Responsible AI considerations

---

# 👨‍💻 About the Developer

## ANNREDDY SAAKETH REDDY

B.Tech Artificial Intelligence & Machine Learning student interested in:

* 🤖 Artificial Intelligence
* 🧠 Machine Learning
* 👁️ Computer Vision
* 🐍 Python
* 📊 Data Science
* 🔬 Deep Learning
* 🌐 AI-powered applications

### 🔗 Connect With Me

If you are interested in AI/ML, computer vision, deepfake detection, or related projects, feel free to connect with me through my profiles below.

**GitHub:**
https://github.com/asreddy2209-arch

**LinkedIn:**
https://www.linkedin.com/in/saaketh-reddy-annreddy-22434937b/

---

# 🌐 Developer Profiles

| Platform     | Profile                                                       |
| ------------ | --------------------------------------------------------------|
| 🐙 GitHub    | https://github.com/asreddy2209-arch                           |
| 💼 LinkedIn  | https://www.linkedin.com/in/saaketh-reddy-annreddy-22434937b/ |

---

# 📌 Project Links

| Resource                 | Link                                                                          |
| ------------------------ | ----------------------------------------------------------------------------- |
| 📦 GitHub Repository     | https://github.com/asreddy2209-arch/PROJECT.1_Unmasking-Deepfake_Forensic-AI/ |
| 💼 LinkedIn Project Post | https://www.linkedin.com/in/saaketh-reddy-annreddy-22434937b/                 |
| 🌐 Live Demo             | https://project1unmasking-deepfakeforensic-1ejgt0dih-forensic-ai.vercel.app/  |
| 🎥 Project Demo Video    | http://127.0.0.1:5000/video                                                   |
| 📄 Project Documentation | YOUR-DOCUMENTATION-URL                                                        |

---

Open `http://127.0.0.1:5000` in your web browser:
- **Image Forensics Lab**: `http://127.0.0.1:5000/`
- **Video Frame Lab (Max 30 FPS)**: `http://127.0.0.1:5000/video`
- **Dedicated Video Forensics Report**: Automatically redirected to `http://127.0.0.1:5000/video-results/<job_id>`

---

# ⭐ GitHub Project Highlights

```text
⭐ Deepfake Image Detection
⭐ ResNet18 CNN
⭐ LSTM Sequence Classification
⭐ Computer Vision
⭐ Digital Forensics
⭐ Colour Analysis
⭐ Noise Analysis
⭐ Grayscale Analysis
⭐ Suspicious Heatmaps
⭐ Evidence Overlays
⭐ Flask Web Dashboard
⭐ PyTorch
⭐ OpenCV
```

# 📜 License

Add the license that matches your project and dataset permissions.

For example:

```text
MIT License
```

> Before choosing a license, make sure it is compatible with any third-party datasets, pretrained models, or other components used in the project.

---

# 🤝 Contributing

Contributions, suggestions, and improvements are welcome.

A typical contribution workflow is:

```bash
git clone YOUR-GITHUB-REPOSITORY-URL
cd Unmasking_Deepfake
```

Create a branch:

```bash
git checkout -b feature/improvement
```

Make your changes and commit:

```bash
git add .
git commit -m "Add improvement"
```

Push the branch:

```bash
git push origin feature/improvement
```

Then open a Pull Request on GitHub.

---

# 🚀 Project Vision

The long-term goal of **Unmasking the Deepfake** is to develop a more comprehensive synthetic-media analysis platform capable of combining:

```text
Image Analysis
      +
Video Analysis
      +
Deep Learning
      +
Computer Vision
      +
Digital Forensics
      +
Explainability
      +
Responsible AI
```

The current implementation provides a foundation that can be extended toward **multi-frame video analysis, stronger benchmark evaluation, face-aware processing, calibrated predictions, and improved explainability**.

---

# 🏆 Final Project Summary

```text
                UNMASKING THE DEEPFAKE
                         │
          ┌──────────────┴──────────────┐
          │                             │
     Deep Learning                Image Forensics
          │                             │
     ┌────┴────┐              ┌─────────┼─────────┐
     │         │              │         │         │
  ResNet18   LSTM          Colour     Noise   Grayscale
     │         │              │         │         │
     └────┬────┘              └─────────┼─────────┘
          │                             │
          ▼                             ▼
     Prediction                 Suspicious Analysis
          │                             │
          └──────────────┬──────────────┘
                         ▼
                  Heatmap + Overlay
                         │
                         ▼
                Deepfake Analysis
```

### 🧠 Core Technologies

**PyTorch • ResNet18 • LSTM • OpenCV • Flask • NumPy • Pillow • Scikit-learn**

### 🎯 Core Concept

**Detect → Analyze → Visualize → Interpret**

---

# ⭐ Support the Project

If you find this project useful for learning or experimentation:

* ⭐ Star the repository
* 🍴 Fork the repository
* 🐛 Report issues
* 💡 Suggest improvements
* 🔗 Share the project
* 💼 Connect on LinkedIn

---

⭐ **If you found this project useful, consider giving the repository a star!**
