# AI Coding Instructions for cv-fail-detect

## Project Overview

**Purpose:** A binary image classification system that detects surveillance camera failures (obstruction, blur, misalignment, darkness, etc.) using computer vision and machine learning.

**Key business constraint:** Recall is prioritized over precision—missing a failure (false negative) costs more operationally than false alarms.

**Failure modes to detect:** Lens obstruction, severe blur, lighting failures (washout/darkness), physical misalignment, frozen feeds, weather obstruction.

## Architecture & Data Strategy

- **Problem type:** Binary image classification (functioning vs. degraded)
- **Modeling approaches:** 
  - Interpretable baseline using hand-crafted features (blur metrics, brightness, entropy) with traditional ML
  - Deep learning approach with fine-tuned CNNs (ResNet, EfficientNet) and transfer learning
- **Data composition:** Mix of public traffic camera streams + synthetically degraded images (clearly labeled in training)
- **Directory structure** (as described in README):
  ```
  ├── data/          # Raw and processed frames
  ├── notebooks/     # EDA and experiments  
  ├── src/
  │   ├── preprocessing/  # Image quality metrics, normalization
  │   ├── features/       # Blur, brightness, entropy extraction
  │   ├── models/         # Model definitions, training loops
  ├── results/       # Model outputs, performance analysis
  ```

## Key Patterns & Conventions

**Image preprocessing:** Use consistent resizing/normalization across training/inference. Document any preprocessing steps applied during feature extraction, as they affect model generalization to unseen camera feeds.

**Model evaluation:** Use F1-score or recall-focused metrics (not accuracy) when comparing models. Maintain detailed error analysis tracking false negatives separately.

**Feature engineering:** Both traditional ML and DL paths are valid—when adding features (e.g., temporal smoothing, edge detection), benchmark against the baseline to justify added complexity.

**Synthetic data transparency:** Tag all synthetically degraded images in datasets. When reporting results, report performance separately on synthetic vs. real camera data if possible.

## Development Workflow

**Getting started:**
1. Clone the repo: `git clone https://github.com/imsibaja/cv-fail-detect.git`
2. Check README for current phase (currently: problem definition and baseline modeling)
3. Look at `notebooks/` for existing EDA and experiment patterns

**Testing & experimentation:** Use Jupyter notebooks for exploration; move validated approaches to `src/` modules for reuse.

**Next planned work** (from README): Multiclass classification (identify failure type), temporal modeling for intermittent failures, monitoring dashboard prototype.

## Collaboration Notes

- This is a portfolio/demonstration project prioritizing **interpretability and clear methodology** alongside performance
- Document the "why" behind architectural decisions, especially trade-offs between interpretable ML and black-box DL approaches
- Public accessibility matters—avoid hardcoded camera URLs; use environment variables or config files
