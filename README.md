# Surveillance Camera Failure Detection

## What This Project Does

Cities spend millions maintaining surveillance camera networks—traffic monitors, parking enforcement, public safety systems. My little town of Fillmore has recently installed 4 flock cameras scattered around town. The problem? Cameras can fail constantly (dirt, weather, hardware issues), but nobody knows until someone manually checks or a critical incident reveals the gap.

I built a computer vision system that automatically detects camera failures by analyzing the video feed itself. Think of it as a health monitor for infrastructure that normally operates blind.

## The Business Problem

Failed cameras create real costs: - Traffic management loses data for optimization - Law enforcement misses evidence windows\
- Maintenance teams waste time on manual spot-checks - Cities pay for cameras that aren't actually working

My solution flags failures in real-time by classifying each frame as either functioning normally or degraded.

## Technical Approach

**Problem Type:** Binary image classification

**Failure modes I detect:** - Lens obstruction (dirt, snow, vandalism) - Severe blur or defocus - Lighting failures (washout, darkness) - Physical misalignment - Frozen feeds - Weather obstruction

**My Modeling Strategy:**

I tested two approaches to compare interpretability vs. performance:

1.  **Interpretable baseline** - Extracted image quality features (blur metrics, brightness, entropy) and trained traditional ML models. This gives stakeholders explainable results.

2.  **Deep learning** - Fine-tuned CNNs (ResNet, EfficientNet) for higher accuracy. Used transfer learning to work with limited labeled data.

I prioritized recall over precision—missing a failure (false negative) is worse than a false alarm.

## Data Strategy

I combined: - Public traffic camera streams - Synthetically degraded images (clearly labeled as training augmentation)

The synthetic approach is intentional: it let me create balanced training data for rare failure types while being transparent about data limitations.

This dataset contains minimal metadata, reflecting a realistic operational constraint in many real-world camera networks.

## Results

*\[This section will show model performance comparisons, precision/recall tradeoffs, and specific failure modes the system catches well vs. struggles with\]*

## Skills Demonstrated

-   **Computer vision**: Image preprocessing, feature engineering, CNN architectures
-   **Model evaluation**: Handling imbalanced classes, choosing metrics that match business priorities
-   **ML engineering**: Transfer learning, model comparison, error analysis
-   **Domain translation**: Taking an operational problem (infrastructure monitoring) and framing it as a solvable ML task

## Tech Stack

Python • PyTorch • OpenCV • scikit-learn • NumPy • Pandas

## Repository Structure

```         
├── data/          # Raw and processed frames
├── notebooks/     # EDA and experiments  
├── src/
│   ├── preprocessing/
│   ├── features/
│   ├── models/
├── results/       # Model outputs and analysis
```

## What's Next

-   Expand to multiclass classification (identify *which* failure type)
-   Add temporal modeling to catch intermittent failures
-   Build a monitoring dashboard prototype

## Context Note

This project focuses on system monitoring, not identifying people. I use only publicly accessible data and discuss the surveillance context critically—the technical approach transfers directly to industrial IoT monitoring, quality control systems, and remote sensing applications.

------------------------------------------------------------------------

**Ian Morris-Sibaja**\
*Portfolio demonstrating production-ready computer vision for infrastructure monitoring*