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

- The model achieved 91.6% overall accuracy on CelebA, but showed a consistent 
  **5.2% F1 gap** between female subgroups (F1: 0.933) and male subgroups 
  (F1: 0.881), suggesting the model encodes gender as a feature rather than 
  expression alone.
- On FairFace (zero-shot, 97,698 images), female subgroups were predicted as 
  smiling at **roughly double the rate** of male subgroups across every racial 
  group without exception — confirming the gender bias is a property of the model, 
  not an artifact of the CelebA distribution.
- Racial disparities emerged within male subgroups on FairFace: white males showed 
  the highest predicted smiling rate (15.2%) while middle eastern males showed the 
  lowest (8.9%), a gap invisible in the CelebA evaluation which lacked racial labels.

## Methodology

This project reproduces and extends the evaluation framework from Buolamwini and 
Gebru's *Gender Shades* (FAccT 2018), applying intersectional demographic evaluation 
to expression classification rather than gender classification.

The two-dataset approach was intentional:
- **CelebA** provides ground truth labels, enabling accuracy-based fairness metrics 
  (precision, recall, F1 per subgroup)
- **FairFace** provides racial demographic labels and a demographically diverse 
  population, enabling distributional bias analysis across race × gender subgroups

## References

- Buolamwini, J. & Gebru, T. (2018). Gender Shades: Intersectional Accuracy 
  Disparities in Commercial Gender Classification. *FAccT 2018*.
- Karkkainen, K. & Joo, J. (2021). FairFace: Face Attribute Dataset for Balanced 
  Race, Gender, and Age. *WACV 2021*.
