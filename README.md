## Project Overview
This project uses deep learning with TensorFlow to classify facial images as **Smiling** or **Not Smiling**.  
In addition to model performance, the project evaluates **demographic bias** by analyzing prediction disparities across subgroups such as gender and age.

## Evaluation Metrics
The model is evaluated using standard classification metrics, including:
- **Accuracy** for overall performance
- **Precision, Recall, and F1-score** to assess error trade-offs
- **Confusion matrices** to analyze misclassification patterns
- **Subgroup-wise performance metrics** to identify potential demographic bias

## Evaluation Strategy
Model performance is primarily evaluated using **recall** for the smiling class, as it measures the proportion of actual smiling faces correctly identified by the model. This metric is emphasized to expose potential demographic bias, particularly false negatives that may disproportionately affect certain subgroups.

Additional metrics include precision, F1-score, and confusion matrices. Confusion matrices are computed separately for each demographic subgroup (e.g., gender and age) to analyze misclassification patterns and identify performance disparities.

## Bias Hypothesis 
**Primary hypothesis**.

Due to the potential gender imbalance in the CelebA dataset , the model is expected to avheive a higher classification accuracy in the female gender than male presenting faces.

**Exploratory Hyothesis** 

Although CelebA dataset does not explicity label skin tone , the model may demonstrate reduced performance for darker skin tone. This analysis is exploratory and subject ot dataset limitations .

## Limitations
While the work of the model is to evaluate the smiling attributes across a demopgraphuc group , there are several limitations. First the CelebA dataset does not evenly represent gender demographic categories, prior analysis has shown that female labeled images occur more than male labeled images ,which could influence model decisions and evaluations. Second, the dataset does not provide explicit annotations for skin tone or other intersectional attributes, so any exploratory interpretations regarding these features are limited by the absence of ground-truth labels. Third, the dataset consists of celebrity images collected from publicly available sources, which may not represent broader population distributions. These factors limit the generalizability of this study’s findings to other settings beyond the CelebA dataset.

