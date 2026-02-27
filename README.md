## Proposal

### Introduction / Background
Breast cancer is a disease characterized by the abnormal, rapid growth of breast cells forming tumors. When individuals are not diagnosed at an early stage, these tumors can metastasize, becoming increasingly lethal. Globally, breast cancer is one of the most prevalent forms of cancers affecting. Within the United States alone, about 1 in 8 women are affected by breast cancer during their lifetime [1]. 

However, early intervention is extremely effective and vital in reducing the effects of this cancer. Computer-aided detection (CAD) acts as a supplemental tool for radiologists in identifying abnormalities. CAD leverages technologies such as Machine Learning, Artificial Intelligence, and Image Processing to analyze ultrasounds, mammograms, and MRIs to detect early-stage cancers, either validating a professional’s diagnosis or even pointing out abnormalities that they may have overlooked.
#### Literature Review
Traditional diagnosis often relies on fine needle aspiration (FNA) biopsies [2]. However, human interpretation can often be subject to variability based on countless factors. Research has shown that computer derived nuclear features, quantitative measurements extracted from digital pathology scans like FNA, can help more efficiently distinguish between benign and malignant masses [3]. With more recent advances in Deep Learning and ML algorithms like Support Vector Machines (SVM), machine learning based disease diagnosis (MLBDD) shows accuracies above 90% [4], [5].
#### Dataset Description
For our project, we will be using the Diagnostic Wisconsin Breast Cancer Database from the UCI Machine Learning Repository. There are 32 features including radius, texture, perimeter, areas, smoothness, compactness, concavity, concave points, symmetry, and fractal dimension. They describe characteristics of the cell nuclei in the digital image. The binary target variable indicates if the tumour is benign (B) or malignant (M). It is made up of 569 samples, 357 of which are benign and 212 are malignant. 
#### Dataset Source
Link: https://archive.ics.uci.edu/dataset/17/breast+cancer+wisconsin+diagnostic

### Problem Definition
#### Problem
The primary challenge in breast cancer diagnosis is the consequences of misclassification. A False Positive can result in unnecessary invasive procedures and a False Negative can delay or prevent necessary treatment. The lack of transparency in many CAD systems makes it difficult for professionals to trust the automated outputs and black-boxed predictions.
#### Motivation
We aim to build a system that essentially maximizes recall to make sure no cancer presence is left undetected while sustaining high accuracy by applying robust ML algorithms. We also would like to look for deeper insights by incorporating unsupervised learning, potentially finding different clusters of masses that might represent information such as different stages of the progression of cancer. This would provide more insight beyond the binary label of malignant or benign.

### Methods
#### Data Preprocessing
1. [blank]
2. [blank]
3. [blank]

#### Algorithms/Models
1. [blank]
2. [blank]
3. [blank]

#### Supervised Learning Methods

#### Unsupervised Learning Methods

### Results and Discussion

#### Quantitative Metrics
We plan to use standard metrics defined in the scikit-learn metrics documentation. Because this is a binary classification project (Benign vs. Malignant), and false negatives are clinically important, our evaluation prioritizes recall for the malignant class.

Supervised Learning Evaluation (SVM and XGBoost)

1. Recall (Malignant Class)

&emsp; Recall measures the proportion of actual malignant tumors correctly identified: Recall = TP / (TP + FN). This is our primary metric because false negatives (malignant predicted as benign) are the most critical error.

2. Precision (Malignant Class)

&emsp; Precision measures the proportion of predicted malignant tumors that are truly malignant: Precision = TP / (TP + FP).

3. F1-Score

&emsp; The F1-score is the harmonic mean of precision and recall: F1 = 2 * (Precision * Recall) / (Precision + Recall)

4. ROC-AUC

&emsp; The Receiver Operating Characteristic Area Under the Curve (ROC-AUC) for comparing SVM and XGBoost.

5. Balanced Accuracy

&emsp; Balanced accuracy accounts for class imbalance by averaging recall across classes. This prevents inflated performance estimates from majority-class dominance.

6. Confusion Matrix
&emsp; - True Positives (TP)
&emsp; - False Positives (FP)
&emsp; - True Negatives (TN)
&emsp; - False Negatives (FN)

&emsp; Specifically for minimizing false negatives.


Unsupervised Learning Evaluation (K-Means)

1. Adjusted Rand Index (ARI)

&emsp; Measures similarity between clustering assignments and ground truth labels, adjusted for chance.

2. Normalized Mutual Information (NMI)

&emsp; Measures shared information between cluster assignments and true labels.

4. Silhouette Score

&emsp; Measures internal cluster cohesion and separation without using ground truth labels.

5. Model Generalization
&emsp; - Cross-validation mean score
&emsp; - Cross-validation standard deviation
&emsp; - Training vs. validation performance gap

#### Project Goals

#### Expected Results

### References
[1] L. Shockney, “Breast Cancer Facts & Statistics,” National Breast Cancer Foundation, Jun. 15, 2023. https://www.nationalbreastcancer.org/breast-cancer-facts/

[2] Cleveland Clinic, “Fine-Needle Aspiration,” Cleveland Clinic, May 16, 2023. https://my.clevelandclinic.org/health/diagnostics/17872-fine-needle-aspiration-fna

[3] W. H. Wolberg, W. Nick. Street, D. M. Heisey, and O. L. Mangasarian, “Computer-derived nuclear features distinguish malignant from benign breast cytology,” Human Pathology, vol. 26, no. 7, pp. 792–796, Jul. 1995, doi: https://doi.org/10.1016/0046-8177(95)90229-5.

‌[4] M. M. Ahsan, S. A. Luna, and Z. Siddique, “Machine-Learning-Based Disease Diagnosis: A Comprehensive Review,” Healthcare, vol. 10, no. 3, p. 541, Mar. 2022, doi: https://doi.org/10.3390/healthcare10030541.

[5] M. Golts, “Support Vector Machines,” AI in Asset Management: Tools, Applications, and Frontiers, pp. 40–51, Nov. 2025, doi: https://doi.org/10.56227/25.1.38.

## Gantt Chart
https://docs.google.com/spreadsheets/d/1q1Ha7X4cs_rv75ANg4HArgvxn4CUn1_MCZZd7z7sMLw/edit?usp=sharing

## Contribution Table
| Name  | Proposal Contributions |
| --- | --- |
| Aesha Shah  | Content Cell  |
| Shreema Vijayakumar  | Content Cell  |
| Suhaani Gupta  | Content Cell  |
| Galadriel Cho  | Content Cell  |
| Arya Nalavade  | Content Cell  |

## GitHub Repository
https://github.gatech.edu/ashah726/ashah726.github.io

## Slidedeck
https://docs.google.com/presentation/d/1FLcbaeM0SAPhENrqE2YTM4Voni2K-sQHjwmWEPyKncg/edit?usp=sharing

## Proposal Draft Document
https://docs.google.com/document/d/1hO6IhdO9scGuWqY_3P0qxXo7ijVnvJT0wbaslSVciW4/edit?usp=sharing
