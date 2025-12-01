# Nowcasting Euro Area Manufacturing Confidence with LLMs & News Data

[![Python](https://img.shields.io/badge/Python-3.11-blue.svg)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.0+-red.svg)](https://pytorch.org/)
[![Transformers](https://img.shields.io/badge/%F0%9F%A4%97-HuggingFace-yellow)](https://huggingface.co/)


---

## 📖 Overview

This project proposes a novel framework for **nowcasting the Euro Area Manufacturing Confidence Index (ICI)** using global news flow. By leveraging the **GDELT** database and a **Teacher-Student LLM Distillation** pipeline, we construct a high-frequency sentiment index that significantly improves macroeconomic forecasting accuracy.

### Key Results
- **Data:** Processed over 760k+ news articles (2015-2025) related to the Eurozone economy.
- **Method:** Distilled sentiment knowledge from **Gemini-Pro** (Teacher) to lightweight models like **MPNet** (Student).
- **Performance:** Adding the LLM-based sentiment index to a baseline AR(2) model reduced the forecast RMSE from **1.508** to **1.300** (a ~14% improvement).

---

## 🚀 Methodology

The pipeline consists of three main stages:

### 1. Data Engineering (BigQuery & GDELT)
* **Source:** GDELT GKG (Global Knowledge Graph).
* **Filtering:** SQL queries via BigQuery to filter for Eurozone countries and Manufacturing/Economy themes.
* **Preprocessing:** Deduplication, Entity Resolution (Country mapping), and noise removal (sport/crime filtering).

### 2. LLM Distillation (Teacher-Student Framework)
To analyze massive amounts of text cost-effectively, we used a knowledge distillation approach:
* **Teacher:** **Gemini-2.5-Pro**. Scored a representative subset (Teacher Set) of headlines on a scale of -1 to 1.
* **Students:** Trained lightweight regressors on the Teacher's labels:
    * *Student A:* FinBERT + Random Forest
    * *Student B:* DeBERTa-Financial + Random Forest
    * *Student C:* **MPNet Embeddings + Ridge Regression** (Best Performer)
* **Inference:** Applied the best student model to the entire dataset (660k+ articles) to generate the "EA Manufacturing Sentiment Index".

### 3. Econometric Nowcasting
* **Baseline:** Autoregressive model $AR(2)$.
* **Enhanced:** $ARX(2) + Sentiment_{t-2}$.
* **Evaluation:** Out-of-sample RMSE on the last 24 months.

---

## 📂 Repository Structure

```bash
├── data/                   # Data files (often not included due to size)
├── notebooks/
│   ├── data-preproccesing.ipynb  # GDELT cleaning, dedup, and filtering
│   └── llm-fine-tuned.ipynb      # Gemini labeling, Student model training, and ARX forecasting
├── slides/
│   └── data+LLM.pdf # Detailed presentation slides
├── results/                # Saved models and forecast plots
└── README.md
