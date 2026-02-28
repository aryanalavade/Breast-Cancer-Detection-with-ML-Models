# Proposal

## Introduction / Background
Breast cancer is a disease characterized by the abnormal, rapid growth of breast cells forming tumors. When individuals are not diagnosed at an early stage, these tumors can metastasize, becoming increasingly lethal. Globally, breast cancer is one of the most prevalent forms of cancers affecting. Within the United States alone, about 1 in 8 women are affected by breast cancer during their lifetime [1]. 

However, early intervention is extremely effective and vital in reducing the effects of this cancer. Computer-aided detection (CAD) acts as a supplemental tool for radiologists in identifying abnormalities. CAD leverages technologies such as Machine Learning, Artificial Intelligence, and Image Processing to analyze ultrasounds, mammograms, and MRIs to detect early-stage cancers, either validating a professional’s diagnosis or even pointing out abnormalities that they may have overlooked.
#### Literature Review
Traditional diagnosis often relies on fine needle aspiration (FNA) biopsies [2]. However, human interpretation can often be subject to variability based on countless factors. Research has shown that computer derived nuclear features, quantitative measurements extracted from digital pathology scans like FNA, can help more efficiently distinguish between benign and malignant masses [3]. With more recent advances in Deep Learning and ML algorithms like Support Vector Machines (SVM), machine learning based disease diagnosis (MLBDD) shows accuracies above 90% [4], [5].
#### Dataset Description
For our project, we will be using the Diagnostic Wisconsin Breast Cancer Database from the UCI Machine Learning Repository. There are 32 features including radius, texture, perimeter, areas, smoothness, compactness, concavity, concave points, symmetry, and fractal dimension. They describe characteristics of the cell nuclei in the digital image. The binary target variable indicates if the tumour is benign (B) or malignant (M). It is made up of 569 samples, 357 of which are benign and 212 are malignant. 
#### Dataset Source
Link: https://archive.ics.uci.edu/dataset/17/breast+cancer+wisconsin+diagnostic

## Problem Definition
### Problem
The primary challenge in breast cancer diagnosis is the consequences of misclassification. A False Positive can result in unnecessary invasive procedures and a False Negative can delay or prevent necessary treatment. The lack of transparency in many CAD systems makes it difficult for professionals to trust the automated outputs and black-boxed predictions.
#### Motivation
We aim to build a system that essentially maximizes recall to make sure no cancer presence is left undetected while sustaining high accuracy by applying robust ML algorithms. We also would like to look for deeper insights by incorporating unsupervised learning, potentially finding different clusters of masses that might represent information such as different stages of the progression of cancer. This would provide more insight beyond the binary label of malignant or benign.

## Methods
### Data Preprocessing
1. Data Cleaning  
The ID column does not provide predictive value and will be removed. Although the dataset documentation indicates no missing values, we will programmatically verify this and handle any anomalies if detected.
3. One Hot Encoding  
The Diagnosis column currently contains either M for a malignant tumor or B for a benign tumor. To facilitate classification, these labels will be encoded as 0 for B and 1 for M.
4. Dimensionality Reduction  
The dataset contains 30 numerical features, many of which are correlated. We will apply Principal Component Analysis to reduce dimensionality while preserving maximum variance. PCA will help reduce multicollinearity, improve computational efficiency, and potentially improve generalization. We will evaluate model performance both with and without PCA to measure its impact.

### Algorithms/Models
1. K-MEANS  
K-Means is an unsupervised algorithm that applies hard clustering to separate our data into groupings based on tumor feature similarities. The intent is to roughly align data within clusters with benign and malignant labels. We will evaluate clustering quality using silhouette scores and compare cluster assignments against true labels.
2. XGBoost  
XGBoost is a supervised prediction algorithm that sequentially learns through gradient boosted decision trees.  XGBoost is not sensitive to linear dependence between features, a beneficial trait given that we begin with 30. We will use the xgboost.XGBClassifier implementation and tune learning rate, max depth, and number of estimators.
3. SVM  
SVM is a supervised algorithm that classifies by maximizing the margin between classes. Particularly powerful for binary classification, it will be applied to predict between benign and malignant tumors. We will experiment with both linear and RBF kernels using sklearn.svm.SVC. Hyperparameters such as C and gamma will be tuned using grid search with cross-validation.


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
The primary goal of this project is to develop and evaluate a machine learning model for binary classification of breast tumors using morphological features from our Breast Cancer Wisconsin Diagnostic dataset. To accomplish this, we aim to compare the predictive performance of multiple supervised learning algorithms, XGBoost and SVM. Additionally, we will investigate whether unsupervised clustering, K-means, reveals natural groupings within the tumor feature space that align with malignancy status. We will also evaluate the impact of using dimensionality reduction, specifically PCA, on the model's classification accuracy and generalization. 

Throughout this project, we will consider clinical and computational sustainability when developing the model because misclassification in cancer diagnosis has serious consequences. We will prioritize high recall in order to minimize false negatives, while still maintaining a strong overall accuracy. We aim to leverage low-cost nuclear morphology features instead of expensive genomic or imaging pipelines, so that we can explore whether accurate predictions can be achieved using scalable and resource-efficient data. Additionally, we will also evaluate dimensionality reduction (PCA) to reduce redundancy and improve computational efficiency. In terms of ethics, since it is a smaller dataset, there is a risk of overfitting. As a result, we will be using stratified cross-validation and performing  hyperparameter tuning within validation folds. Additionally, we will analyze feature importance in order to improve model transparency and ensure that the use of this is a decision-support research prototype rather than a clinical diagnostic tool.


### Expected Results
We expect that our machine learning model will have a strong classification performance in distinguishing malignant from benign tumors using the dataset. There has been prior work done on this same dataset, and it also had a very high performance, with Support Vector Classification using an RBF kernel achieving testing accuracy near 98.7% in an open-access study, along with robust precision and recall metrics across evaluation splits [6]. Therefore, based on past results, it suggests that a well-tuned SVM and similar classifiers are capable of reliably separating benign and malignant cases. By using cross-validation, we expect our models to have high accuracy, robust ROC-AUC values, and balanced sensitivity and specificity, especially when thresholds are set to prioritize recall in a clinical setting. Based on prior research, we also expect feature importance analyses to identify morphology-related variables, such as texture and area, as important predictors. This will support the models' responsible, clinically meaningful use and offer interpretable insights.


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
