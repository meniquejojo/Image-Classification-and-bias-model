# Image Classification and Bias Analysis

This repository contains research into intersectional bias in facial expression
classification. The project trains a CNN smiling classifier on the CelebA dataset,
evaluates its performance across demographic subgroups, and tests whether bias
patterns generalize to an out-of-distribution dataset (FairFace).

## Research Question

Does a smiling classifier trained on CelebA encode demographic stereotypes rather
than learning expression features independent of identity — and does that bias
pattern persist when the model encounters a demographically diverse dataset it has
never seen?

## Key Findings

- The CelebA evaluation revealed a consistent gender performance gap. Female
  subgroups achieved a **true positive rate of 92.5%** and a **false negative
  rate of 7.5%**, while male subgroups achieved a **true positive rate of 87.4%**
  and a **false negative rate of 12.6%**. The model failed to detect smiling in
  male subjects at nearly double the rate it failed for female subjects — a
  **5.1 percentage point FNR gap**.
- On FairFace (zero-shot, 97,698 images), female subgroups were predicted as
  smiling at **roughly double the rate** of male subgroups across every racial
  group without exception — consistent with the hypothesis that the model encoded
  a social stereotype associating femininity with smiling.
- Racial disparities emerged within gender subgroups on FairFace: among females,
  white females showed the highest predicted smiling rate (26.3%) and Indian
  females the lowest (16.6%), a **9.7 percentage point gap**. Among males, white
  males showed the highest rate (15.2%) and middle eastern males the lowest
  (8.9%), a **6.3 percentage point gap** — both invisible in the CelebA
  evaluation due to the absence of racial demographic labels.
- Training data imbalance — CelebA contained 118,165 female images compared to
  84,434 male images — likely contributed to the model encoding demographic
  stereotypes as learned features.

## Methodology

This project reproduces and extends the evaluation framework from Buolamwini and
Gebru's *Gender Shades* (FAccT 2018), applying intersectional demographic
evaluation to expression classification rather than gender classification.

Fairness metrics follow the Gender Shades framework: true positive rate (TPR),
false negative rate (FNR), false positive rate (FPR), and true negative rate
(TNR) per demographic subgroup.

The two-dataset approach was intentional:
- **CelebA** provides ground truth smiling labels, enabling accuracy-based
  fairness metrics (TPR, FNR, FPR, TNR per subgroup)
- **FairFace** provides racial demographic labels and a demographically diverse
  general population, enabling distributional bias analysis across race × gender
  subgroups

## Repository Structure
