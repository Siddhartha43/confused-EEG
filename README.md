# Brainwave Measurement for Assessing Learning Engagement: A Machine Learning Approach

## Motivation
This research was driven by our curiosity about whether it's feasible to assess student engagement in learning, particularly the emotion of confusion, by measuring brainwaves. Measuring the degree of confusion is crucial both in classroom teaching and online learning environments.

## Dataset from Kaggle
[Confused student EEG brainwave data](https://www.kaggle.com/code/shreyaspj/confused-student-eeg-prediction)

## Dataset Processing
- Remove columns: `attention`, `mediation`, `raw`
- Retain data up to 112 seconds for each video
- Two normalization methods:
  - Individual normalization
  - Overall normalization
- Target variable: `y` (user-defined label)

## Discussion on Data Handling

In reviewing previous methodologies used on Kaggle, a significant flaw was identified in the data handling process. There was an issue where data from the same participant was being used in both the training and testing phases of the model development. This practice inadvertently allowed the model to 'see' part of the answers beforehand, leading to an overestimated accuracy rate in the testing evaluation.

To rectify this, a more robust approach has been adopted to ensure that each participant's data is exclusively allocated to either the training set or the testing set, but not both. This method, known as 'subject independence', is critical for validating the model's ability to generalize to new, unseen data. By enforcing this separation, we aim to achieve a more accurate and realistic assessment of the model's predictive performance.

## Model Training
- Models used: Random Forest, SVM, KNN
- Exclude data for specific test subjects (IDs: 3, 5)
- Target variable: `y` (user-defined label)

## Model Testing
- Traditional methods were limited to offline analysis.
- Subject independence validation

### SVM Parameters:
- `C`: Penalty parameter
- `Kernel`: Kernel function type
- `gamma`: Coefficient for the kernel function

### KNN Parameters:
- `n_neighbors`: Number of neighbors
- `weights`: Weight function
- `metric`: Distance metric

### Random Forest Parameters:
- `n_estimators`: Number of trees in the forest (50/100/150)
- `max_depth`: Maximum depth of the tree (8/10/none)
- `min_samples_split`: Minimum number of samples required to split a node (2/5/10)
- `min_samples_leaf`: Minimum number of samples required at a leaf node (1/2/4)

## Results

Performance comparison of models with different normalization methods:

| Normalization Method | KNN     | SVM     | Random Forest |
|----------------------|---------|---------|---------------|
| Individual           | 0.5766  | 0.5689  | 0.5578        |
| Overall              | 0.6745  | 0.6710  | 0.6898        |
| **Improvement**      | 14.51%  | 17.94%  | 23.66%        |

The results demonstrate significant improvement in model performance when using overall standardization compared to individual standardization.


