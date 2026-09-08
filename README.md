# Failure-Driven YOLO–MLLM Weed Identification

Official research code for **failure-driven integration of YOLOv8n and multimodal large language models (MLLMs) for interpretable aquatic weed identification**.

This repository accompanies the research study:

> **Failure-Driven Integration of YOLO and Multimodal Large Language Models for Interpretable Weed Identification**

The study investigates how an MLLM can complement a YOLO-based object detector by providing contextual and natural-language interpretation, particularly for detection cases identified through systematic failure analysis.

## Overview

Conventional object detection systems primarily provide class labels, bounding boxes, and confidence scores. Although these outputs can achieve high detection performance, they may provide limited contextual information for interpreting ambiguous or low-confidence predictions in field conditions.

This project implements a complementary pipeline in which:

1. **YOLOv8n** performs aquatic weed detection.
2. Detection outputs are evaluated on an independent test set.
3. **Failure cases** are identified based on predefined criteria.
4. Selected anomalous cases are passed to a **multimodal large language model (MLLM)**.
5. The MLLM provides natural-language interpretation and species verification.
6. The contribution of the interpretive layer is evaluated under different levels of training-data availability.

The MLLM is therefore used as an **interpretive component**, rather than as a replacement for the YOLO detector.

## Research Workflow

```text
Dataset Preparation
        │
        ▼
YOLOv8n Training
        │
        ▼
Independent Test Evaluation
        │
        ▼
Failure Analysis
        │
        ├── High-confidence detection
        │
        └── Anomalous detection
                │
                ▼
        MLLM Interpretation
                │
                ▼
       Species Verification
                │
                ▼
   Interpretability Analysis
                │
                ▼
     Limited-Data Robustness
```

## Target Weed Species

The system focuses on four aquatic weed species:

| Class | Common Name        | Scientific Name         |
| ----- | ------------------ | ----------------------- |
| 0     | Duckweed           | *Lemna minor*           |
| 1     | Water hyacinth     | *Eichhornia crassipes*  |
| 2     | False pickerelweed | *Monochoria korsakowii* |
| 3     | Water lettuce      | *Pistia stratiotes*     |

## Dataset

The research uses a hybrid dataset consisting of two data sources.

### 1. Merauke Aquatic Weed Dataset (MAWD)

The primary component consists of field images acquired directly by the authors at irrigation sites in **Tanah Miring District, Merauke Regency, South Papua, Indonesia**.

These images were collected in situ under natural field conditions and represent variations in background, vegetation density, object orientation, lighting, and plant growth stages.

### 2. WaterHyacinth Dataset

The secondary component uses the publicly available **WaterHyacinth Dataset** published by Kabir et al. (2024).

The original dataset should be retained under its original name and cited to its original publication.

### Data Provenance

```text
Primary field acquisition
        │
        ▼
Merauke Aquatic Weed Dataset (MAWD)
        │
        │
        ├──────────────┐
                       │
Public secondary data  │
        │              │
        ▼              │
WaterHyacinth Dataset  │
        │              │
        └──────┬───────┘
               ▼
       Hybrid Dataset
```

All images used in the study were annotated using the YOLO object-detection format with bounding boxes for the target weed objects.

## Experimental Configuration

The main experimental configuration described in the study includes:

* **Detector:** YOLOv8n
* **Pretrained weights:** COCO
* **Training epochs:** 15
* **Batch size:** 8
* **Input resolution:** 416 × 416 pixels
* **Training platform:** Google Colab
* **GPU:** NVIDIA Tesla T4
* **Initial learning rate:** 0.01
* **Learning-rate schedule:** Linear
* **Data augmentation:** Mosaic, horizontal flip, and HSV color-space jitter
* **Early stopping patience:** 10 epochs
* **Random seed:** Fixed for deterministic execution
* **MLLM:** Google Gemini
* **Dataset split:** 70% training, 15% validation, and 15% testing

## Failure-Driven Evaluation

The central methodological component of this repository is the failure-driven evaluation process.

After YOLOv8n inference on the independent test set, detection outputs are categorized into:

* **Normal/high-confidence detections**
* **Low-confidence predictions**
* **Misclassifications**
* **Missed detections**

In the reported experimental configuration, a confidence threshold of **0.95** was used to identify low-confidence predictions.

The anomalous cases are subsequently analyzed using the MLLM to determine whether multimodal reasoning can provide additional interpretive value.

## MLLM Interpretation

The MLLM is used as a complementary interpretive layer.

The detector provides:

* Class label
* Bounding box
* Confidence score

The MLLM is used to provide additional information such as:

* Species verification
* Visual characteristics
* Field-context interpretation
* Infestation considerations
* Management priorities
* Natural-language explanations

The MLLM is not intended to replace the object detector. Instead, it is activated for cases where the detection output requires additional interpretation.

## Robustness Under Limited Training Data

The repository also supports experiments with reduced training-data availability.

The study evaluates YOLOv8n using:

* 10% of the training data
* 25% of the training data
* 50% of the training data
* 100% of the training data

The same independent test subset is used across scenarios to enable consistent comparison.

This experiment is designed to investigate how the relative contribution of the MLLM changes as the amount of detector training data decreases.

## Reported Results

Under the executed runtime configuration reported in the manuscript:

* YOLOv8n achieved **99.47% mAP@50** on the independent test set.
* Class-label accuracy reached **99.26%**.
* The independent test set contained **269 images**.
* Eight detection anomalies were identified.
* The anomalies consisted of six low-confidence predictions and two misclassifications.
* No missed detections were observed.
* The MLLM recovered the correct ground-truth species in all eight flagged anomaly cases.

The limited-data experiment showed the largest difference between YOLO and MLLM at the 10% training-data level.

## Repository Structure

A recommended project structure is:

```text
failure-driven-yolo-mllm-weed-identification/
│
├── README.md
├── requirements.txt
├── environment.yml
│
├── configs/
│   ├── dataset.yaml
│   └── training.yaml
│
├── data/
│   └── README.md
│
├── notebooks/
│   ├── 01_dataset_preparation.ipynb
│   ├── 02_yolov8_training.ipynb
│   ├── 03_test_evaluation.ipynb
│   ├── 04_failure_analysis.ipynb
│   ├── 05_mllm_interpretation.ipynb
│   └── 06_limited_data_robustness.ipynb
│
├── src/
│   ├── dataset/
│   ├── detection/
│   ├── evaluation/
│   ├── failure_analysis/
│   ├── mllm/
│   └── visualization/
│
├── scripts/
│   ├── train.py
│   ├── evaluate.py
│   ├── failure_analysis.py
│   └── robustness.py
│
├── results/
│   ├── metrics/
│   ├── failure_cases/
│   └── figures/
│
└── LICENSE
```

## Installation

Clone the repository and install the required dependencies.

```bash
git clone https://github.com/<username>/failure-driven-yolo-mllm-weed-identification.git
cd failure-driven-yolo-mllm-weed-identification

pip install -r requirements.txt
```

The exact dependency versions should be specified in `requirements.txt` to support reproducibility.

## Dataset Preparation

Because the dataset contains both primary field-acquired images and a publicly available secondary source, users should obtain and organize the data according to the data-provenance documentation.

The primary field dataset is not redistributed in this repository unless explicitly permitted.

The public secondary dataset should be obtained from its original source and used according to its original licensing and attribution requirements.

After preparation, the dataset should follow the expected YOLO directory structure:

```text
data/
└── weed/
    ├── images/
    │   ├── train/
    │   ├── val/
    │   └── test/
    │
    └── labels/
        ├── train/
        ├── val/
        └── test/
```

## Reproducibility

The experimental workflow uses deterministic execution with a fixed random seed.

For reproducibility, users should keep the following configuration consistent:

* Dataset split
* Random seed
* YOLO model version
* Training hyperparameters
* Image resolution
* Batch size
* Number of epochs
* Data augmentation
* Evaluation threshold
* MLLM model and runtime configuration

Because MLLM outputs can depend on model versions, runtime configuration, prompts, and service updates, exact reproduction of generated natural-language explanations may require recording the model version and prompt configuration used during each experiment.

## Citation

If you use this code or the associated research workflow in academic work, please cite the accompanying publication:

```text
Latif, A., Jati, H., & Surjono, H. D.
Failure-Driven Integration of YOLO and Multimodal Large Language Models
for Interpretable Weed Identification.
Journal of Information Systems Engineering and Business Intelligence.
```

Please replace the bibliographic information above with the final published citation and DOI once available.

## Data Availability

The manuscript states that the data and source code supporting the findings are available from the corresponding author upon reasonable request.

The complete dataset and source code are not stored in a public repository at the time of manuscript preparation.

## Acknowledgment

This research was supported by the academic and institutional environment of the Doctoral Program of Engineering Science, Faculty of Engineering, Universitas Negeri Yogyakarta, and Universitas Musamus.

## License

The source-code license should be specified according to the authors' intended distribution terms.

Dataset licensing and attribution requirements are separate from the software license and must be respected for each external dataset used in the project.

## Disclaimer

This repository is intended for research and experimental purposes. The MLLM-generated interpretations should not be considered a substitute for expert agronomic assessment. The research specifically identifies species-level verification as the evaluated MLLM contribution, while the factual reliability and quality of agronomic recommendations require further expert validation.
