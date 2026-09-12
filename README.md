```markdown
# Towards Interpretable Weed Identification through the Complementary Integration of YOLO and Multimodal Large Language Models: A Failure Analysis Perspective

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/agustan-alt/failure-driven-yolo-mllm-weed-identification/blob/main/FIX_FINAL_WaterHyacinth_YOLO8_LLM/FIX_FINAL_WaterHyacinth_YOLO8_LLM.ipynb)
[![Kaggle Dataset](https://kaggle.com/static/images/open-in-kaggle.svg)](https://www.kaggle.com/datasets/agustanlatif/merauke-aquatic-weed-dataset)
[![Kaggle Notebook](https://img.shields.io/badge/Kaggle%20Code-Interactive%20Notebook-blue?logo=kaggle)](https://www.kaggle.com/code/agustanlatif/merauke-aquatic-weed-detection-yolov8-mllm)
[![License: CC BY 4.0](https://img.shields.io/badge/Dataset%20License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![License: MIT](https://img.shields.io/badge/Code%20License-MIT-yellow.svg)](LICENSE)

Official open-science research repository for the study submitted to the **Journal of Information Systems Engineering and Business Intelligence (JISEBI)**.

---

## 📌 Executive Summary

Conventional deep learning object detectors such as YOLO produce raw bounding boxes and class logits that lack semantic agronomic interpretability and remain vulnerable to visual anomalies (glare, turbidity, occlusion, and morphological overlap). This research proposes a **Failure-Driven Complementary Framework** integrating **Ultralytics YOLOv8n** with **Multimodal Large Language Models (Google Gemini 1.5 Flash)** to systematically detect, characterize, and autonomously resolve detection anomalies.

```
+-----------------------------------------------------------------------------------+
|                           YOLO-MLLM COMPLEMENTARY PIPELINE                        |
+-----------------------------------------------------------------------------------+
|  Input Field Image                                                                |
|         │                                                                         |
|         ▼                                                                         |
|  [ YOLOv8n Detector ] ──(Confidence >= 0.95)──► Safe Automated Field Action       |
|         │                                                                         |
|         └──(Anomaly Flagged: Conf < 0.95 or Misclass)                             |
|                    │                                                              |
|                    ▼                                                              |
|       [ Multimodal LLM: Gemini 1.5 Flash ]                                        |
|                    │                                                              |
|                    ▼                                                              |
|       • Botanical Verification (100% Anomaly Correction)                          |
|       • Visual Morphological Diagnostic Reasoning                                 |
|       • Agronomic Advisory (Growth Stage, Density & Urgency)                      |
+-----------------------------------------------------------------------------------+
```

---

## 📊 Dataset Provenance & Experimental Design

To guarantee full transparency and auditability per **FAIR research principles**, the dataset structure evaluated in this paper is documented below:

### 1. Primary Field Dataset (Merauke, South Papua)
* **Name:** Merauke Aquatic Weed Dataset (MAWD) / SPAWD
* **Collector & Annotator:** Agustan Latif, Universitas Negeri Yogyakarta
* **Origin:** Irrigation canals and freshwater wetlands in Tanah Miring, Merauke, South Papua, Indonesia.
* **Imaging:** DJI Mavic 3 Pro Drone & handheld high-resolution RGB cameras under authentic equatorial sun-glare and variable water conditions.
* **Repository:** [Kaggle Dataset - MAWD](https://www.kaggle.com/datasets/agustanlatif/merauke-aquatic-weed-dataset)

### 2. Secondary Public Benchmark Dataset
* **Origin:** Kabir et al. (Mendeley Data, CC BY 4.0)
* **Purpose:** Taxonomic diversity enhancement across four target tropical taxa (*Lemna minor*, *Eichhornia crassipes*, *Monochoria korsakowii*, *Pistia stratiotes*).
* **Repository:** [Kaggle Dataset - Mendeley Benchmark](https://www.kaggle.com/datasets/aqilwahid/waterhyacinth-dataset-mendeley)

### 3. Dual-Tier Experimental Evaluation
* **Tier 1 — Full Hybrid Manuscript Benchmark (N = 2,580 images):** The primary research baseline reported in the JISEBI manuscript, integrating primary field captures with secondary open benchmarks (Train: 1,806, Val: 387, Test: 387).
* **Tier 2 — Lightweight Runtime Audit Benchmark (N = 1,790 images):** Configured directly in the executable Colab & Kaggle notebooks (Train: 1,253, Val: 268, Test: 269) for rapid, 1-click GPU reproducibility and empirical MLLM failure verification without exceeding cloud hardware quotas.

> **Integrity Declaration:** 100% of raw benchmark images are authentic photographic captures (**0% generative-AI / synthetic images**). All validation and test sets remain strictly unaugmented to prevent data leakage.

---

## 🎯 Key Empirical Findings

1. **High Detection Performance:** YOLOv8n achieved an overall **mAP@50 of 99.5%** on the validation set and **97.93% accuracy** on the manuscript independent test set (**99.26%** on the runtime audit test set).
2. **Autonomous Anomaly Resolution:** Out of all flagged detection anomalies ($C < 0.95$ and subtle cross-species misclassifications), Google Gemini 1.5 Flash achieved a **100.0% botanical correction rate (8/8 cases)** utilizing diagnostic morphological reasoning (e.g., bulbous spongy petioles, rosette leaf patterns).
3. **Data Scarcity Resilience:** Under extreme data constraints (10% training data), YOLO accuracy dropped to 71.8%, while the MLLM maintained **88.5% zero-shot accuracy** (a **+16.7 pp compensatory advantage**).

---

## 📁 Repository Structure

```text
failure-driven-yolo-mllm-weed-identification/
│
├── README.md                                  <- This comprehensive audit document
├── LICENSE                                    <- MIT open-source license
│
└── FIX_FINAL_WaterHyacinth_YOLO8_LLM/
    ├── FIX_FINAL_WaterHyacinth_YOLO8_LLM.ipynb <- Master reproducible Jupyter Notebook
    ├── FIX_FINAL_WaterHyacinth_YOLO8_LLM.html  <- Pre-computed visual execution HTML
    └── FIX_FINAL_WaterHyacinth_YOLO8_LLM.pdf   <- Full audit-grade execution PDF log
```

---

## 🚀 How to Reproduce & Execute

### Option 1: 1-Click Interactive Cloud Execution (Recommended)
You can directly run the complete pipeline with interactive IPyWidgets:
* **Run on Google Colab:** Click the [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/agustan-alt/failure-driven-yolo-mllm-weed-identification/blob/main/FIX_FINAL_WaterHyacinth_YOLO8_LLM/FIX_FINAL_WaterHyacinth_YOLO8_LLM.ipynb) badge above.
* **Run on Kaggle Code:** Access the pre-linked notebook on [Kaggle Code](https://www.kaggle.com/code/agustanlatif/merauke-aquatic-weed-detection-yolov8-mllm).

### Option 2: Local Environment Setup
```bash
# 1. Clone repository
git clone https://github.com/agustan-alt/failure-driven-yolo-mllm-weed-identification.git
cd failure-driven-yolo-mllm-weed-identification

# 2. Create virtual environment
python -m venv venv
# Linux/macOS: source venv/bin/activate | Windows: venv\Scripts\activate

# 3. Install core dependencies
pip install ultralytics google-generativeai opencv-python pillow scikit-learn seaborn ipywidgets

# 4. Launch Jupyter Lab / Notebook
jupyter lab FIX_FINAL_WaterHyacinth_YOLO8_LLM/FIX_FINAL_WaterHyacinth_YOLO8_LLM.ipynb
```

---

## 📑 Citation

If this dataset, codebase, or methodology aids your research, please cite:

```bibtex
@article{latif2026towards,
  title={Towards Interpretable Weed Identification through the Complementary Integration of YOLO and Multimodal Large Language Models: A Failure Analysis Perspective},
  author={Latif, Agustan and Jati, Handaru and Surjuno, Herman Dwi},
  journal={Journal of Information Systems Engineering and Business Intelligence (JISEBI)},
  year={2026},
  note={Under Review / Revision}
}
```

---

## ⚖️ License
* **Source Code & Pipelines:** Licensed under the [MIT License](LICENSE).
* **Benchmark Datasets & Annotations:** Licensed under Creative Commons Attribution 4.0 International ([CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)).
```
