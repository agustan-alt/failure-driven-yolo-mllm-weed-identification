# Failure-Driven YOLO–MLLM Weed Identification

This repository contains the research artifacts for **Failure-Driven Integration of YOLO and Multimodal Large Language Models for Interpretable Weed Identification**.

The project investigates the complementary use of **YOLOv8n** and a **multimodal large language model (MLLM)** for aquatic weed identification, with particular emphasis on interpreting anomalous or low-confidence detection cases.

## Repository Contents

The repository currently contains the following research artifacts:

```text
FIX_FINAL_WaterHyacinth_YOLO8_LLM/
│
├── FIX_FINAL_WaterHyacinth_YOLO8_LLM.ipynb
├── FIX_FINAL_WaterHyacinth_YOLO8_LLM.html
└── FIX_FINAL_WaterHyacinth_YOLO8_LLM.pdf
```

### `FIX_FINAL_WaterHyacinth_YOLO8_LLM.ipynb`

The Jupyter Notebook contains the executable research workflow and experimental implementation used in the study.

It documents the processing and analysis associated with the YOLOv8n-based aquatic weed detection and the subsequent MLLM-based interpretation of selected detection cases.

### `FIX_FINAL_WaterHyacinth_YOLO8_LLM.html`

An HTML export of the research notebook.

This version is provided for convenient browser-based inspection of the documented workflow and experimental outputs without requiring Jupyter Notebook.

### `FIX_FINAL_WaterHyacinth_YOLO8_LLM.pdf`

A PDF version of the research notebook and experimental documentation.

It can be used as a static reference for reviewing the methodology, results, visualizations, and analysis.

## Research Overview

The study investigates how an MLLM can complement a YOLO-based object detector by providing contextual and natural-language interpretation, particularly for detection cases identified through systematic failure analysis.

The overall workflow is:

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

YOLOv8n is used as the primary object detector, while the MLLM functions as a complementary interpretive component rather than a replacement for the detector.

## Target Weed Species

The study focuses on four aquatic weed species:

| Class | Common Name        | Scientific Name         |
| ----- | ------------------ | ----------------------- |
| 0     | Duckweed           | *Lemna minor*           |
| 1     | Water hyacinth     | *Eichhornia crassipes*  |
| 2     | False pickerelweed | *Monochoria korsakowii* |
| 3     | Water lettuce      | *Pistia stratiotes*     |

## Dataset

The research uses a hybrid dataset consisting of two sources.

### Merauke Aquatic Weed Dataset (MAWD)

The primary component consists of field images acquired at irrigation sites in **Tanah Miring District, Merauke Regency, South Papua, Indonesia**.

The images represent natural field conditions, including variations in background, vegetation density, object orientation, lighting, and plant growth stages.

### WaterHyacinth Dataset

The secondary component uses the publicly available **WaterHyacinth Dataset** published by Kabir et al. (2024).

The original dataset should be retained under its original name and cited according to its original publication and licensing requirements.

## Experimental Configuration

The main experimental configuration reported in the study includes:

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

The central methodological component of the study is the failure-driven evaluation process.

After YOLOv8n inference on the independent test set, detection outputs are categorized into:

* Normal/high-confidence detections
* Low-confidence predictions
* Misclassifications
* Missed detections

A confidence threshold of **0.95** was used to identify low-confidence predictions in the reported experimental configuration.

Selected anomalous cases are subsequently analyzed using the MLLM to investigate whether multimodal reasoning can provide additional interpretive value.

## MLLM Interpretation

The MLLM is used as a complementary interpretive layer.

YOLOv8n provides:

* Class label
* Bounding box
* Confidence score

The MLLM is used to provide additional interpretation such as:

* Species verification
* Visual characteristics
* Field-context interpretation
* Infestation considerations
* Management priorities
* Natural-language explanations

The MLLM is not intended to replace the object detector. It is activated for cases where the detection output requires additional interpretation.

## Limited-Data Robustness

The study also evaluates the detection workflow under reduced training-data availability.

The evaluated training-data levels are:

* 10%
* 25%
* 50%
* 100%

The same independent test subset is used across scenarios to enable consistent comparison.

## Reported Results

Under the experimental configuration reported in the research artifacts:

* YOLOv8n achieved **99.47% mAP@50** on the independent test set.
* Class-label accuracy reached **99.26%**.
* The independent test set contained **269 images**.
* Eight detection anomalies were identified.
* The anomalies consisted of six low-confidence predictions and two misclassifications.
* No missed detections were observed.
* The MLLM recovered the correct ground-truth species in all eight flagged anomaly cases.

The limited-data experiment showed the largest difference between YOLO and MLLM at the **10% training-data level**.

## Reproducibility

The main executable research workflow is provided in:

```text
FIX_FINAL_WaterHyacinth_YOLO8_LLM.ipynb
```

The HTML and PDF files provide alternative formats for reviewing the documented workflow and experimental outputs.

For reproducibility, the following experimental settings should be kept consistent:

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

Because MLLM outputs may depend on model versions, prompts, runtime configuration, and service updates, exact reproduction of generated natural-language explanations may require recording the model version and prompt configuration used during the experiment.

## Data Availability

The primary field dataset is not redistributed in this repository.

The public secondary dataset should be obtained from its original source and used according to its original licensing and attribution requirements.

The manuscript states that the data and source code supporting the findings are available from the corresponding author upon reasonable request.

## Citation

If you use this research or its associated workflow in academic work, please cite the accompanying publication:

```text
Latif, A., Jati, H., & Surjono, H. D.
Failure-Driven Integration of YOLO and Multimodal Large Language Models
for Interpretable Weed Identification.
Journal of Information Systems Engineering and Business Intelligence.
```

Please replace the bibliographic information above with the final published citation and DOI once available.

## Disclaimer

This repository is intended for research and experimental purposes.

The MLLM-generated interpretations should not be considered a substitute for expert agronomic assessment. The research evaluates species-level verification as an MLLM contribution, while the factual reliability and quality of agronomic recommendations require further expert validation.
