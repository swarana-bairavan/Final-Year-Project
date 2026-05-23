# 🌿 NAMASTE-ICD11 · HealthRosetta

> *Unlocking the translation between AYUSH traditional medicine and modern ICD-11 clinical codes*

[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat&logo=python&logoColor=white)](https://python.org)
[![Java](https://img.shields.io/badge/Java-17+-ED8B00?style=flat&logo=java&logoColor=white)](https://java.com)
[![FHIR R4](https://img.shields.io/badge/FHIR-R4-E84A20?style=flat)](https://hl7.org/fhir/)
[![ICD-11](https://img.shields.io/badge/ICD--11-WHO-005EB8?style=flat)](https://icd.who.int/en)
[![License](https://img.shields.io/badge/License-MIT-green?style=flat)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Active%20Development-14B8A6?style=flat)]()

---

## 📌 Overview

**NAMASTE-ICD11** (Neural Ayurvedic Mapping and Semantic Terminology Engine for ICD-11) is a hybrid AI framework designed to bridge the gap between **AYUSH traditional medicine terminology** and **WHO ICD-11 clinical codes**.

India's AYUSH sector serves millions of patients using classical Sanskrit-based diagnostic terms like *Agnimandya*, *Jwara*, and *Amavata* — none of which exist in modern clinical coding systems. This project provides an accurate, explainable, and FHIR-compliant mapping engine to enable **interoperability between traditional and modern healthcare systems**.

---

## 🎯 Motivation

- **~900 million** AYUSH consultations happen in India every year with no standardized clinical coding
- AYUSH Electronic Health Records (EHRs) cannot communicate with modern hospital systems due to terminology mismatch
- India's **Ayushman Bharat Digital Mission (ABDM)** mandates ICD-11 compliance for all health records, including AYUSH
- Existing tools lack explainability, FHIR compliance, and support for Sanskrit medical vocabulary

---

## ✨ Features

| Feature | Details |
|---|---|
| 🧠 **Hybrid AI Mapping** | TF-IDF baseline + BioBERT semantic fusion |
| ⚡ **XAI Explainability** | Token-level contribution heatmaps (SHAP/LIME) |
| 🏥 **FHIR R4 Compliant** | Outputs valid HL7 FHIR R4 `Condition` resources |
| 🔐 **ABHA-Aligned Security** | OAuth2 security layer aligned with ABHA standards |
| 📊 **Evaluation Suite** | Top-k Accuracy, MRR, Coverage, per-category breakdown |
| 🌿 **49 AYUSH Terms** | Spanning 19 medical categories with synonym expansion |
| 🔗 **REST API** | Java Spring Boot + HAPI FHIR backend |

---

## 🏗️ System Architecture

```
AYUSH Input Term
      │
      ▼
┌─────────────┐
│ Preprocessor│  ← Tokenization, normalization, synonym expansion
└──────┬──────┘
       │
       ▼
┌──────────────────────────────────┐
│       Hybrid Embedding Layer     │
│  TF-IDF Baseline + BioBERT       │  ← Week 1 + Week 2
│  Cosine Similarity Fusion        │
└──────────────┬───────────────────┘
               │
               ▼
┌──────────────────────────────────┐
│    NAMASTEMapper (Ranking)       │  ← Confidence scoring, Top-k results
└──────────────┬───────────────────┘
               │
       ┌───────┴───────┐
       ▼               ▼
┌────────────┐   ┌──────────────────┐
│  XAI Layer │   │  FHIR R4 Output  │  ← Week 3 + Week 4
│ SHAP / LIME│   │  Spring Boot API │
└────────────┘   └──────────────────┘
```

---

## 📁 Project Structure

```
NAMASTE-ICD11/
│
├── src/
│   ├── python/
│   │   ├── preprocessor.py          # Text normalization pipeline
│   │   ├── tfidf_embedder.py        # TF-IDF vectorizer + cosine similarity
│   │   ├── biobert_embedder.py      # BioBERT hybrid fusion (Week 2)
│   │   ├── namaste_mapper.py        # Core mapping API
│   │   ├── evaluator.py             # Top-k Accuracy, MRR, Coverage
│   │   └── xai/
│   │       └── shap_explainer.py    # SHAP/LIME explainability (Week 3)
│   │
│   └── java/
│       └── namaste-api/             # Spring Boot REST API (Week 4)
│           ├── src/main/java/
│           └── pom.xml
│
├── data/
│   └── ayush_icd11_dataset.csv      # 49-entry synthetic dataset
│
├── demo/
│   ├── NAMASTE_ICD11_Demo.html      # Standalone browser demo
│   └── namaste_demo.jsx             # React component demo
│
├── tests/
│   └── test_namaste.py              # 17 unit tests (Week 1)
│
├── docs/
│   └── project_report.pdf           # Anna University mini project report
│
├── results/
│   └── baseline_metrics.json        # Week 1 benchmark results
│
├── .gitignore
├── requirements.txt
└── README.md
```

---

## 📊 Benchmark Results (Week 1 — TF-IDF Baseline)

> ⚠️ These are **self-retrieval scores** used to verify the baseline engine, not real-world performance claims.

| Metric | Score |
|---|---|
| Top-1 Accuracy | **98.0%** |
| Top-3 Accuracy | **100%** |
| Mean Reciprocal Rank (MRR) | **0.990** |
| Coverage | **100%** (49/49 entries mapped) |
| Dataset Size | 49 entries, 19 categories |

*Full experimental results with BioBERT hybrid will be updated after Week 2.*

---

## 🗂️ Dataset

49 curated AYUSH-to-ICD-11 mappings spanning **19 medical categories**:

`Digestive` `Respiratory` `Skin` `Fever` `Metabolic` `Musculoskeletal` `Haematology` `Mental Health` `Neurology` `Ophthalmology` `Urology` `Cardiology` `Hepatology` `Gynaecology` `ENT` `Paediatrics` `Surgical`

**Sample entries:**

| AYUSH Term | ICD-11 Code | Description | Category |
|---|---|---|---|
| Agnimandya | DA96.Z | Functional dyspepsia | Digestive |
| Jwara | MG2A.0 | Fever / pyrexia | Fever |
| Amavata | FA20.0 | Rheumatoid arthritis | Musculoskeletal |
| Madhumeha | 5A10.Z | Diabetes mellitus type 2 | Metabolic |
| Shwasa | CA21.0 | Bronchial asthma | Respiratory |

---

## 🚀 Getting Started

### Prerequisites

```bash
Python 3.10+
Java 17+
Maven 3.8+
```

### Installation

```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/NAMASTE-ICD11.git
cd NAMASTE-ICD11

# Install Python dependencies
pip install -r requirements.txt
```

### Run the Mapping Engine

```python
from src.python.namaste_mapper import NAMASTEMapper

mapper = NAMASTEMapper()
results = mapper.map("Jwara", top_k=3)

for r in results:
    print(f"{r.rank}. {r.term} → {r.icd11_code} ({r.confidence:.2%})")
```

### Run Tests

```bash
python -m pytest tests/ -v
```

### Run the Browser Demo

Simply open `demo/NAMASTE_ICD11_Demo.html` in any browser — no server needed.

---

## 🔄 Development Roadmap

- [x] **Week 1** — TF-IDF Baseline Engine, Dataset (49 entries), Evaluator, 17 Unit Tests
- [ ] **Week 2** — BioBERT Hybrid Fusion Model
- [ ] **Week 3** — SHAP/LIME Explainability Layer
- [ ] **Week 4** — Java Spring Boot REST API + HAPI FHIR Integration + Security

---

## 🛠️ Tech Stack

**Machine Learning / Python**
- `scikit-learn` — TF-IDF vectorization
- `sentence-transformers` — BioBERT embeddings
- `shap`, `lime` — Explainability
- `pytest` — Unit testing

**Backend / Java**
- `Spring Boot 3` — REST API
- `HAPI FHIR` — FHIR R4 resource generation
- `Spring Security` — OAuth2

---

## 🔌 FHIR R4 Output Example

```json
{
  "resourceType": "Condition",
  "id": "ayush-mg2a-0",
  "code": {
    "coding": [
      {
        "system": "http://id.who.int/icd/release/11/mms",
        "code": "MG2A.0",
        "display": "Fever / pyrexia of unknown origin"
      },
      {
        "system": "http://ayush.gov.in/terminology",
        "code": "jwara",
        "display": "Jwara"
      }
    ]
  },
  "extension": [
    {
      "url": "http://namaste-icd11.ai/confidence",
      "valueDecimal": 0.9823
    }
  ]
}
```

---

## 👥 Authors

| Name | Role |
|---|---|
| **SB** | Lead Developer & ML Engineer |
| **Najeem Dheen Abdul Majeeth** | Co-author |
| **Senthamil Selvan S** | Co-author |

**Faculty Advisor:** Dr. K. Vijayakumar, Head of Department  
**Institution:** St. Joseph's Institute of Technology, Chennai  
**Affiliation:** Anna University, Chennai

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgements

- World Health Organization (WHO) — ICD-11 classification system
- Ministry of AYUSH, Government of India
- HL7 International — FHIR R4 standard
- Hugging Face — BioBERT model weights

---

<div align="center">
  <sub>Built with 🌿 for bridging traditional wisdom and modern medicine</sub>
</div>
