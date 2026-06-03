# CelebA Smiling Classifier — Bias Audit

A CNN trained to classify smiling expressions on the CelebA dataset, with a
full demographic bias audit across gender subgroups using Gender Shades-aligned
fairness metrics.

## What This Notebook Does

1. Loads and preprocesses the CelebA dataset
2. Trains a CNN smiling classifier (64×64 input)
3. Evaluates performance using TPR, FNR, FPR, and TNR per subgroup
4. Identifies gender-based performance disparities
5. Generates confusion matrices and performance heatmaps

## Results

### Subgroup Performance

| Subgroup | TPR | FNR | FPR | TNR |
|----------|-----|-----|-----|-----|
| Female | 0.925 | 0.075 | 0.080 | 0.920 |
| Male | 0.874 | 0.126 | 0.074 | 0.926 |

**Key finding:** The model failed to detect smiling in male subjects at nearly
double the rate it failed for female subjects — a 5.1 percentage point false
negative rate gap. This suggests the model weighted gender features more heavily
than expression features during training.

## Fairness Metrics

Metrics follow the Gender Shades evaluation framework:

- **TPR (True Positive Rate):** proportion of smiling images correctly
  classified as smiling
- **FNR (False Negative Rate):** proportion of smiling images incorrectly
  classified as not smiling
- **FPR (False Positive Rate):** proportion of not-smiling images incorrectly
  classified as smiling
- **TNR (True Negative Rate):** proportion of not-smiling images correctly
  classified as not smiling

A fair model would show consistent TPR and FNR across demographic subgroups.
The gap observed here — particularly in FNR — indicates systematic
underperformance on male subjects.

## Dataset Composition

| Group | Image Count |
|-------|-------------|
| Female | 118,165 |
| Male | 84,434 |

The 1.4:1 female-to-male ratio in training data likely contributed to the
model encoding gender as a predictive feature rather than learning expression
features independent of demographic identity.

## Setup

Download the CelebA dataset from
[Kaggle](https://www.kaggle.com/datasets/jessicali9530/celeba-dataset) and
place it at `data/`. Update the `DATA_PATH` variable in the config cell at
the top of the notebook.

## Methodology Note

Subgroup evaluation methodology adapted from Buolamwini & Gebru,
*Gender Shades* (FAccT 2018).
