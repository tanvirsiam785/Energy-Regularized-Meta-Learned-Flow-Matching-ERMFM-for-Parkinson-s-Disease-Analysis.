# ERMFM: Parkinson's Disease Analysis

## Project Title
Few-Shot Adaptive Data Generation through Energy-Regularized Meta-Learned Flow Matching for Parkinson's Disease Analysis

## Overview
This project proposes an Energy-Regularized Meta-Learned Flow Matching (ERMFM) framework to support Parkinson's disease (PD) analysis when labeled medical data is limited and patient characteristics vary widely.

The framework combines:
- **Gaussian Mixture Model (GMM):** Identifies probabilistic patient subgroups.
- **Flow Matching (FM):** Generates synthetic clinical or MRI-related samples by learning a continuous transformation from noise to the target data distribution.
- **Energy-Based Model (EBM):** Scores generated samples and filters out samples considered implausible by the learned data distribution.
- **Implicit Model-Agnostic Meta-Learning (iMAML):** Helps a model adapt to new patient subgroups using only a few labeled examples.

## Problem Statement
Parkinson's disease datasets can be small, imbalanced, sensitive, and heterogeneous. Models trained on one patient group may not generalize well to another. ERMFM is proposed to generate useful synthetic data, represent patient subgroups, assess sample plausibility, and support few-shot adaptation.

## Main Workflow
1. **Preprocess data**
   - Clean clinical data and handle missing values.
   - Normalize/standardize features.
   - Prepare MRI images in a consistent input format.
2. **Discover patient subgroups with GMM**
   - Fit a Gaussian Mixture Model to the processed features.
   - Use probabilistic subgroup membership to represent overlapping patient profiles.
   - The paper describes using BIC to select the number of Gaussian components.
3. **Generate synthetic data with Flow Matching**
   - Learn a continuous velocity field that transports samples from a simple noise distribution toward the target data distribution.
   - Condition generation on the identified subgroups where applicable.
4. **Validate samples with EBM**
   - Assign energy scores to synthetic samples.
   - Retain low-energy samples and filter unusually high-energy samples, according to the proposed method.
5. **Adapt with iMAML**
   - Use real and validated synthetic samples to support few-shot learning on new patient groups.
   - Evaluate adaptation with small labeled support sets.
6. **Evaluate performance**
   - Assess classification and few-shot performance using metrics such as accuracy, precision, recall, F1-score, and ROC-AUC.
   - Use cross-validation and component ablation analysis as described in the paper.

## Datasets Reported in the Paper
| Dataset | Samples | Data type |
|---|---:|---|
| Parkinson's clinical dataset | 2,105 | Structured clinical data |
| Parkinson's MRI dataset | 442 | Preprocessed T1-weighted MRI scans |

The paper describes clinical features such as demographics, lifestyle, medical history, cardiovascular measurements, cognitive assessments, and motor/non-motor symptoms.

## Reported Results
Overall classification results reported in the paper:
- Accuracy: **0.9140**
- Precision: **0.9060**
- Recall: **0.9180**
- F1-score: **0.9120**
- ROC-AUC: **0.9490**

Few-shot results reported in the paper:

| Setting | Accuracy | ROC-AUC |
|---|---:|---:|
| 5-shot | 0.8870 | 0.9160 |
| 10-shot | 0.9060 | 0.9440 |
| 20-shot | 0.9100 | 0.9470 |

These are results reported by the paper and should not be interpreted as independently reproduced results.

## Suggested Repository Structure
```text
ERMFM/
├── README.txt
├── data/
│   ├── clinical/
│   └── mri/
├── src/
│   ├── preprocessing.py
│   ├── gmm_subgroups.py
│   ├── flow_matching.py
│   ├── energy_validation.py
│   ├── imaml.py
│   └── evaluation.py
├── experiments/
├── results/
└── requirements.txt
```

This is a suggested structure for implementation, not a repository structure specified in the paper.

## Implementation Status
The supplied paper describes a proposed framework and reports experimental results. This README summarizes the paper; it does not claim that the full implementation, datasets, trained models, or experiment scripts are included in this repository.

Before running experiments, add the actual dataset sources, implementation code, environment details, and setup instructions. Follow applicable data-use, privacy, and ethics requirements when handling clinical or MRI data.

## Potential Future Work
The paper suggests:
- Incorporating multimodal health data, including genetic data, wearable-sensor data, and patient trajectories.
- Exploring subgroup-discovery methods beyond GMM.
- Incorporating clinical expert knowledge into energy-based validation.
- Extending the framework to other neurological or chronic diseases.
- Evaluating robustness and utility through further clinical studies.

## Reference
Tasin Zawad Al Jame, Ramisha Mahzabin Hridika, Tanvir Mohammad Siam, Maria Zaman Oyshi, and Zayed Humayun, "Few-Shot Adaptive Data Generation through Energy-Regularized Meta-Learned Flow Matching for Parkinson's Disease Analysis."

---
Note: This README is based on the supplied paper. It documents the proposed methodology and paper-reported results, not verified software functionality.
