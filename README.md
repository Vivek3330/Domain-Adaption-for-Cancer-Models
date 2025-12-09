Domain Adaptation for Cell Lines to Patient Tumors

Overview
This repository implements an Adversarial Domain Adaptation Network using Gradient Reversal Layer (GRL) to transfer drug response predictions from in-vitro cell lines to patient tumors. The goal is to bridge the gap between laboratory cell line experiments and real-world patient outcomes.

Problem Statement
Drug response predictions trained on cell line data (GDSC, CCLE) often fail to generalize to patient tumors (TCGA) due to domain shift. This project uses adversarial domain adaptation to learn domain-invariant features that improve cross-domain generalization.

Key Features
Adversarial Domain Adaptation with Gradient Reversal Layer
Multi-source learning from GDSC and CCLE cell lines
Transfer to patient data (TCGA)
Comprehensive evaluation with domain invariance metrics
TensorBoard integration for training visualization
Expected Performance
Target: 20-30% improvement in patient drug response prediction vs direct transfer
Metrics: MSE, R², Pearson correlation, domain invariance score
Architecture
The system consists of three neural network components:

┌─────────────────┐
│ Gene Expression │ (17,419 features)
└────────┬────────┘
         │
         ▼
┌─────────────────────────────┐
│   Feature Extractor (Gf)    │
│  [1024 → 512 → 256]          │
│  + BatchNorm + Dropout       │
└───────────┬─────────────────┘
            │ domain-invariant features
            ├──────────────┬──────────────┐
            ▼              ▼              ▼
    ┌───────────┐  ┌──────────────┐  ┌─────────────┐
    │ Predictor │  │ Discriminator│  │  Gradient   │
    │    (Gy)   │  │     (Gd)     │  │  Reversal   │
    │   [128]   │  │   [128,64]   │  │    Layer    │
    └─────┬─────┘  └──────┬───────┘  └──────┬──────┘
          │                │                 │
          ▼                ▼                 ▼
    Drug Response    Domain Label     Adversarial
    (regression)    (0=cell, 1=tumor)   Training
Components
Feature Extractor (Gf): Learns domain-invariant gene expression representations
Drug Response Predictor (Gy): Predicts drug sensitivity from features
Domain Discriminator (Gd): Classifies source domain (adversarially trained)
Gradient Reversal Layer: Reverses gradients to fool domain discriminator
Training Objective
L_total = L_drug + λ(t) * L_domain
Where:

L_drug: MSE loss for drug response prediction
L_domain: Cross-entropy loss for domain classification
λ(t): Dynamic weight (0→1.0) following schedule: 2/(1+exp(-10*p)) - 1
