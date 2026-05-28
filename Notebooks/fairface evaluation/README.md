# FairFace Generalization Evaluation

Zero-shot evaluation of the CelebA smiling classifier on FairFace — a 
demographically diverse dataset the model has never seen — to test whether 
gender bias patterns generalize across race and population.

## What This Notebook Does

1. Loads the pretrained CelebA smiling classifier
2. Runs zero-shot inference on 97,698 FairFace images
3. Evaluates predicted smiling rate and model confidence across 
   race × gender subgroups
4. Compares findings against the CelebA bias audit

## Why FairFace Has No Accuracy Metrics

FairFace does not include smiling ground truth labels. This notebook therefore 
measures **distributional bias** rather than accuracy bias:

- **Predicted smiling rate**: what fraction of each subgroup does the model 
  predict as smiling?
- **Average confidence**: how strongly does the model commit to its smiling 
  prediction for each subgroup?

If smiling expression were distributed equally across demographic groups in a 
general population dataset, a fair model would predict approximately equal smiling 
rates across subgroups. Systematic deviation from this expectation — particularly 
patterns consistent with social stereotypes — indicates the model has encoded 
demographic bias from its training distribution.

## Results

| Subgroup | Predicted Smiling Rate | Avg Confidence |
|----------|----------------------|----------------|
| white_female | 26.3% | 28.9% |
| latino_hispanic_female | 23.4% | 26.5% |
| black_female | 19.3% | 23.9% |
| east_asian_female | 18.5% | 22.8% |
| southeast_asian_female | 17.7% | 21.6% |
| middle_eastern_female | 17.3% | 21.6% |
| indian_female | 16.6% | 20.8% |
| white_male | 15.2% | 19.7% |
| latino_hispanic_male | 12.3% | 17.3% |
| black_male | 10.3% | 16.2% |
| indian_male | 10.2% | 15.9% |
| southeast_asian_male | 10.1% | 15.1% |
| east_asian_male | 9.5% | 14.9% |
| middle_eastern_male | 8.9% | 14.8% |

## Key Findings

**Gender bias is systematic and consistent.** Female subgroups are predicted as 
smiling at approximately double the rate of male subgroups across every single 
racial group without exception. This confirms the gender bias identified in the 
CelebA evaluation is a property of the model itself, not an artifact of the 
CelebA dataset distribution.

**Racial disparities exist within gender subgroups.** Among male subgroups, 
white males show the highest predicted smiling rate (15.2%) while middle eastern 
males show the lowest (8.9%) — a 6.3% gap that was invisible in the CelebA 
evaluation, which lacked racial demographic labels entirely.

**Single-dataset evaluation underreports bias.** The CelebA audit revealed gender 
bias but could not surface racial intersectionality. FairFace revealed that bias 
operates across two demographic axes simultaneously. Neither dataset alone tells 
the full story.

## Dataset

1. Download FairFace from [github.com/joojs/fairface](https://github.com/joojs/fairface)

## Methodology Note

Race labels are used directly from FairFace rather than mapped to Fitzpatrick 
skin tone proxies. Collapsing race into a skin tone proxy conflates two distinct 
demographic attributes and risks obscuring the specific group patterns that 
fairness evaluation is designed to surface.

## References

- Buolamwini, J. & Gebru, T. (2018). Gender Shades. *FAccT 2018*.
- Karkkainen, K. & Joo, J. (2021). FairFace. *WACV 2021*.
