# CelebA Smiling Classifier — Bias Audit

A CNN trained to classify smiling expressions on the CelebA dataset, with a 
full demographic bias audit across gender subgroups.

## What This Notebook Does

1. Loads and preprocesses the CelebA dataset
2. Trains a CNN smiling classifier (64×64 input, ~92% overall accuracy)
3. Evaluates performance using precision, recall, and F1-score
4. Breaks down performance by gender subgroups to identify bias patterns
5. Generates confusion matrices and performance heatmaps

## Results

| Metric | Value |
|--------|-------|
| Overall Accuracy | 91.6% |
| Overall Precision | 0.914 |
| Overall Recall | 0.919 |
| Overall F1 | 0.917 |

### Subgroup Performance

| Subgroup | Precision | Recall | F1 |
|----------|-----------|--------|----|
| female_not_smiling | 0.931 | 0.935 | 0.933 |
| female_smiling | 0.931 | 0.935 | 0.933 |
| male_not_smiling | 0.877 | 0.885 | 0.881 |
| male_smiling | 0.877 | 0.885 | 0.881 |

**Gender F1 gap: 5.2%** — Female subgroups consistently outperform male subgroups 
across all metrics. The identical scores within each gender group (smiling vs. 
not smiling) suggest the model weights gender features more heavily than expression 
features.

## Key Finding

The model achieves strong overall accuracy while showing systematic underperformance 
on male subjects. This pattern — correct answers through potentially incorrect 
reasoning — motivated the FairFace generalization evaluation in the companion notebook.


## Methodology Note

Subgroup evaluation methodology adapted from Buolamwini & Gebru, 
*Gender Shades* (FAccT 2018).
