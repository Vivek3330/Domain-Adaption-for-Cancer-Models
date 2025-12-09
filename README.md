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
