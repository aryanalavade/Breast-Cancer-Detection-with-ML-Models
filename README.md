# Proposal

## Introduction / Background
Breast cancer is a disease characterized by the abnormal, rapid growth of breast cells forming tumors. When individuals are not diagnosed at an early stage, these tumors can metastasize, becoming increasingly lethal. Globally, breast cancer is one of the most prevalent forms of cancers affecting. Within the United States alone, about 1 in 8 women are affected by breast cancer during their lifetime [1]. 

However, early intervention is extremely effective and vital in reducing the effects of this cancer. Computer-aided detection (CAD) acts as a supplemental tool for radiologists in identifying abnormalities. CAD utilizes ML and image processing to analyze scans, providing a second opinion that identifies abnormalities missed by manual review.
#### Literature Review
Traditional diagnosis often relies on fine needle aspiration (FNA) biopsies [2]. However, human interpretation can often be subject to variability based on countless factors. Quantitative nuclear features extracted from FNA scans improve the efficiency of distinguishing between benign and malignant masses [3]. With more recent advances in Deep Learning and ML algorithms like Support Vector Machines (SVM), machine learning based disease diagnosis (MLBDD) shows accuracies above 90% [4], [5].
#### Dataset Description
For our project, we will be using the Diagnostic Wisconsin Breast Cancer Database from the UCI Machine Learning Repository. There are 32 features including radius, texture, perimeter, areas, smoothness, compactness, concavity, concave points, symmetry, and fractal dimension. They describe characteristics of the cell nuclei in the digital image. The binary target variable indicates if the tumour is benign (B) or malignant (M). It is made up of 569 samples, 357 of which are benign and 212 are malignant. 
#### Dataset Source
Link: https://archive.ics.uci.edu/dataset/17/breast+cancer+wisconsin+diagnostic

## Problem Definition
### Problem
Diagnostic misclassification is critical. False negatives can delay critical treatment, while false positives cause unnecessary invasive procedures. The lack of transparency in many CAD systems makes it difficult for professionals to trust the automated outputs and black-boxed predictions.
#### Motivation
We aim to build a system that essentially maximizes recall to make sure no cancer presence is left undetected while sustaining high accuracy by applying robust ML algorithms. We also would like to look for deeper insights by incorporating unsupervised learning, potentially finding different clusters of masses that might represent information such as different stages of the progression of cancer.

## Methods
### Data Preprocessing
1. Data Cleaning  
We will drop the non-predictive ID column and programmatically verify the reported lack of missing values.
3. One Hot Encoding  
The Diagnosis column currently contains either M for a malignant tumor or B for a benign tumor. To facilitate classification, these labels will be encoded as 0 for B and 1 for M.
4. Dimensionality Reduction  
We will apply Principal Component Analysis to reduce dimensionality of 30 numerical features while preserving maximum variance. PCA will help reduce multicollinearity, improve computational efficiency, and potentially improve generalization.

### Algorithms/Models
1. K-MEANS  
K-Means is an unsupervised algorithm that applies hard clustering to separate our data into groupings based on tumor feature similarities. The intent is to roughly align data within clusters with benign and malignant labels.
2. XGBoost  
XGBoost is a supervised prediction algorithm that sequentially learns through gradient boosted decision trees.  XGBoost is not sensitive to linear dependence between features, a beneficial trait given that we begin with 30. We will use the xgboost.XGBClassifier implementation and tune learning rate, max depth, and number of estimators.
3. SVM  
SVM is a supervised algorithm that classifies by maximizing the margin between classes. Particularly powerful for binary classification, it will be applied to predict between benign and malignant tumors. We will experiment with both linear and RBF kernels using sklearn.svm.SVC.


## Potential Results and Discussion

### Quantitative Metrics
We plan to use standard metrics defined in the scikit-learn metrics documentation. Because this is a binary classification project (Benign vs. Malignant), and false negatives are clinically important, our evaluation prioritizes recall for the malignant class.

#### Supervised Learning Evaluation (SVM and XGBoost)

1. Confusion Matrix: True Positives (TP), False Positives (FP), True Negatives (TN), False Negatives (FN)

2. Recall (Malignant Class): proportion of actual malignant tumors correctly identified: Recall = TP / (TP + FN). This is our primary metric because false negatives (malignant predicted as benign) are the most critical error.

2. Precision (Malignant Class): proportion of predicted malignant tumors that are truly malignant: Precision = TP / (TP + FP).

3. F1-Score: harmonic mean of precision and recall: F1 = 2 * (Precision * Recall) / (Precision + Recall)

4. Receiver Operating Characteristic Area Under the Curve (ROC-AUC) for comparing SVM and XGBoost.

5. Balanced Accuracy: accounts for class imbalance by averaging recall across classes, preventing inflated performance estimates from majority-class dominance.

#### Unsupervised Learning Evaluation (K-Means)

1. Adjusted Rand Index (ARI): measures how well clusters align with true benign and malignant labels, adjusted for chance.

2. Normalized Mutual Information (NMI): measures how much diagnostic information (benign vs. malignant) is captured by the clusters.

3. Silhouette Score: evaluates cluster separation and cohesion to determine whether tumors form distinct groups in feature space without using labels.

4. Model Generalization: cross-validation mean, standard deviation, and training–validation gap are reported to ensure clustering stability and avoid overfitting.

These measures ensure that clustering structure is stable across data splits and not driven by random variation.

### Project Goals
The goal of this project is to develop and evaluate a binary classification model for breast tumor diagnosis using morphological features from the Breast Cancer Wisconsin Diagnostic dataset. We will compare supervised learning algorithms, including XGBoost and SVM, and explore whether unsupervised clustering (K-means) reveals natural groupings aligned with malignancy. We will also assess the effect of dimensionality reduction using PCA on classification accuracy and generalization.

Given the high stakes of cancer diagnosis, we will prioritize minimizing false negatives while maintaining strong overall accuracy. By using low-cost nuclear morphology features instead of expensive genomic or imaging data, we aim to evaluate whether scalable, resource-efficient inputs can still achieve strong predictive performance. To address overfitting risks in this relatively small dataset, we will use stratified cross-validation with hyperparameter tuning inside validation folds. We will also analyze feature importance to improve transparency and emphasize that this model is a decision-support research prototype, not a clinical diagnostic tool.


### Expected Results
We expect strong classification performance in distinguishing malignant from benign tumors. Prior work on this dataset has achieved testing accuracy near 98.7% using SVM with an RBF kernel, along with high precision and recall across evaluation splits [6]. Based on these results, we anticipate that well-tuned SVM and XGBoost models will achieve high accuracy, strong ROC-AUC, and balanced sensitivity and specificity, particularly when thresholds are adjusted to prioritize recall in clinical contexts.

We also expect feature importance analyses to highlight morphology-related variables, such as texture and area, as key predictors, supporting both model interpretability and clinically meaningful insights.

## References
[1] L. Shockney, “Breast Cancer Facts & Statistics,” National Breast Cancer Foundation, Jun. 15, 2023. https://www.nationalbreastcancer.org/breast-cancer-facts/

[2] Cleveland Clinic, “Fine-Needle Aspiration,” Cleveland Clinic, May 16, 2023. https://my.clevelandclinic.org/health/diagnostics/17872-fine-needle-aspiration-fna

[3] W. H. Wolberg, W. Nick. Street, D. M. Heisey, and O. L. Mangasarian, “Computer-derived nuclear features distinguish malignant from benign breast cytology,” Human Pathology, vol. 26, no. 7, pp. 792–796, Jul. 1995, doi: https://doi.org/10.1016/0046-8177(95)90229-5.

‌[4] M. M. Ahsan, S. A. Luna, and Z. Siddique, “Machine-Learning-Based Disease Diagnosis: A Comprehensive Review,” Healthcare, vol. 10, no. 3, p. 541, Mar. 2022, doi: https://doi.org/10.3390/healthcare10030541.

[5] M. Golts, “Support Vector Machines,” AI in Asset Management: Tools, Applications, and Frontiers, pp. 40–51, Nov. 2025, doi: https://doi.org/10.56227/25.1.38.

# Gantt Chart
https://docs.google.com/spreadsheets/d/1q1Ha7X4cs_rv75ANg4HArgvxn4CUn1_MCZZd7z7sMLw/edit?usp=sharing

# Contribution Table
| Name  | Proposal Contributions |
| --- | --- |
| Aesha Shah  | GitHub repo creation & updates, Proposal (Metrics), Slides (Metrics), Video, Gantt Chart |
| Shreema Vijayakumar  | GitHub repo updates, Proposal (Intro, Problem), Slides & Video (Intro, Problem) |
| Suhaani Gupta  | GitHub repo updates, Proposal (Supervised & Unsupervised Methods), Slides & Video (Supervised & Unsupervised Methods)  |
| Galadriel Cho  | Proposal (Data Preprocessing & Algorithms/Models), Slides & Video (Data Preprocessing & Algorithms/Models) |
| Arya Nalavade  | Proposal (Goals & Expected Results), Slides & Video (Goals & Expected Results) |

# GitHub Repository
https://github.gatech.edu/ashah726/ashah726.github.io

# Slidedeck
https://docs.google.com/presentation/d/1FLcbaeM0SAPhENrqE2YTM4Voni2K-sQHjwmWEPyKncg/edit?usp=sharing

# Proposal Draft Document
https://docs.google.com/document/d/1hO6IhdO9scGuWqY_3P0qxXo7ijVnvJT0wbaslSVciW4/edit?usp=sharing
