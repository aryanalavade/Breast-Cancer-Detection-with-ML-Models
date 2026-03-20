# Midterm

## Introduction / Background
Breast cancer, affecting 1 in 8 women in the United States, is lethal if diagnosed late due to metastasis [1]. Early intervention is vital. Computer-aided detection (CAD) utilizes ML and image processing to provide a second opinion, identifying abnormalities missed by manual review.
#### Literature Review
Traditional diagnosis via fine needle aspiration (FNA) biopsies [2] can often be subject to human variability. Quantitative nuclear features extracted from digital FNA scans enable more efficient differentiation between benign and malignant masses [3]. With more recent advances in Deep Learning and ML algorithms like Support Vector Machines (SVM), machine learning based disease diagnosis (MLBDD) shows accuracies above 90% [4], [5]. 
#### Dataset Description
This project uses the Diagnostic Wisconsin Breast Cancer dataset from the UCI Machine Learning Repository. The dataset contains 569 samples (357 benign and 212 malignant) with 30 numerical features describing cell nucleus characteristics such as radius, texture, concavity, and fractal dimension. The binary target variable indicates whether a tumor is benign or malignant.  
#### Dataset Source
Link: https://archive.ics.uci.edu/dataset/17/breast+cancer+wisconsin+diagnostic

## Problem Definition
### Problem
Diagnostic misclassification is critical. False negatives can delay critical treatment, while false positives cause unnecessary invasive procedures. The lack of transparency in many CAD systems makes it difficult for professionals to trust the automated outputs and black-boxed predictions.
#### Motivation
We aim to maximize recall to ensure no malignancy goes undetected while maintaining high accuracy. Additionally, unsupervised learning will be used to identify latent clusters that may represent different stages of cancer progression.

## Methods
### Data Preprocessing
1. Data Cleaning  
We will drop the non-predictive ID column and programmatically verify the reported lack of missing values.
3. One Hot Encoding  
The Diagnosis column labels (M/B) will be binary encoded as 0 for Benign and 1 for Malignant to facilitate classification.
4. Dimensionality Reduction (IMPLEMENTED IN MIDTERM for K-MEANS)   
We will apply Principal Component Analysis to reduce dimensionality of 30 numerical features while preserving maximum variance. PCA will help reduce multicollinearity, improve computational efficiency, and potentially improve generalization.

### Algorithms/Models
1. K-MEANS (IMPLEMENTED IN MIDTERM)   
K-Means is an unsupervised algorithm that applies hard clustering to separate our data into groupings based on tumor feature similarities. The intent is to roughly align data within clusters with benign and malignant labels.
2. XGBoost  
XGBoost is a supervised prediction algorithm that sequentially learns through gradient boosted decision trees.  XGBoost is not sensitive to linear dependence between features, a beneficial trait given that we begin with 30. We will use the xgboost.XGBClassifier implementation and tune learning rate, max depth, and number of estimators.
3. SVM  (IMPLEMENTED IN MIDTERM)  
SVM is a supervised algorithm that classifies by maximizing the margin between classes. Particularly powerful for binary classification, it will be applied to predict between benign and malignant tumors. We will experiment with both linear and RBF kernels using sklearn.svm.SVC.


## Potential Results and Discussion

### Quantitative Metrics
We plan to use standard metrics defined in the scikit-learn metrics documentation. Because this is a binary classification project (Benign vs. Malignant), and false negatives are clinically important, our evaluation prioritizes recall for the malignant class.

#### Supervised Learning Evaluation (SVM and XGBoost)

1. Confusion Matrix: True Positives (TP), False Positives (FP), True Negatives (TN), False Negatives (FN)

2. Recall (Malignant Class): proportion of actual malignant tumors correctly identified: Recall = TP / (TP + FN)

3. Precision (Malignant Class): proportion of predicted malignant tumors that are truly malignant: Precision = TP / (TP + FP).

4. F1-Score: harmonic mean of precision and recall: F1 = 2 * (Precision * Recall) / (Precision + Recall)

5. Receiver Operating Characteristic Area Under the Curve (ROC-AUC) for comparing SVM and XGBoost.

6. Balanced Accuracy: accounts for class imbalance by averaging recall across classes, preventing inflated performance estimates from majority-class dominance.

#### Unsupervised Learning Evaluation (K-Means)

1. Adjusted Rand Index (ARI): measures how well clusters align with true benign and malignant labels, adjusted for chance.

2. Normalized Mutual Information (NMI): measures how much diagnostic information (benign vs. malignant) is captured by the clusters.

3. Silhouette Score: evaluates cluster separation and cohesion to determine whether tumors form distinct groups in feature space without labels.

4. Model Generalization: cross-validation mean, standard deviation, and training–validation gap are reported to ensure clustering stability and avoid overfitting.

### Project Goals
Our goal is to compare XGBoost and SVM performance while using K-Means to identify latent feature patterns. We prioritize clinical sustainability through high recall and model transparency. We anticipate accuracies near 98.7%, identifying key morphological predictors like texture and area for clinical decision support.

### Expected Results
We anticipate strong classification performance, as prior studies using SVM with RBF kernels on this dataset have reached accuracies near 98.7% [6]. We expect well-tuned models to yield high ROC-AUC and balanced sensitivity. Furthermore, we expect feature importance analysis to identify morphology variables such as texture and areas as the most significant predictors of malignant, providing interpretable insights for clinical support.

## Results & Discussion

### Visualizations

### Quantitative Metrics

### Analysis of Algorithms / Models
1. K-means --
   
3. SVM -- 

### Next Steps
We plan to refine our current model developments (K-means & SVM) and work on XGBoost implementation. [need to add more i think?]

## References
[1] L. Shockney, “Breast Cancer Facts & Statistics,” National Breast Cancer Foundation, Jun. 15, 2023. https://www.nationalbreastcancer.org/breast-cancer-facts/

[2] Cleveland Clinic, “Fine-Needle Aspiration,” Cleveland Clinic, May 16, 2023. https://my.clevelandclinic.org/health/diagnostics/17872-fine-needle-aspiration-fna

[3] W. H. Wolberg, W. Nick. Street, D. M. Heisey, and O. L. Mangasarian, “Computer-derived nuclear features distinguish malignant from benign breast cytology,” Human Pathology, vol. 26, no. 7, pp. 792–796, Jul. 1995, doi: https://doi.org/10.1016/0046-8177(95)90229-5.

‌[4] M. M. Ahsan, S. A. Luna, and Z. Siddique, “Machine-Learning-Based Disease Diagnosis: A Comprehensive Review,” Healthcare, vol. 10, no. 3, p. 541, Mar. 2022, doi: https://doi.org/10.3390/healthcare10030541.

[5] M. Golts, “Support Vector Machines,” AI in Asset Management: Tools, Applications, and Frontiers, pp. 40–51, Nov. 2025, doi: https://doi.org/10.56227/25.1.38.

[6] K. T. Chui, M. D. Lytras, and R. W. Liu, “A Generic Design of Driver Drowsiness and Stress Recognition Using MOGA Optimized Deep MKL-SVM,” Sensors, vol. 20, no. 5, p. 1474, Mar. 2020, doi: https://doi.org/10.3390/s20051474.
‌
# Gantt Chart
https://docs.google.com/spreadsheets/d/1q1Ha7X4cs_rv75ANg4HArgvxn4CUn1_MCZZd7z7sMLw/edit?usp=sharing

# Contribution Table
| Name  | Proposal Contributions |
| --- | --- |
| Aesha Shah  | GitHub repo creation & updates, Proposal (Metrics), Slides (Metrics), Video, Gantt Chart, SVM code (code modifications & visualizations), Midterm (Next Steps) |
| Shreema Vijayakumar  | GitHub repo updates, Proposal (Intro, Dataset Analysis, Problem), Slides & Video (Intro, Dataset Analysis, Problem), SVM model code (base code & initial visualizations)|
| Suhaani Gupta  | GitHub repo updates, Proposal (Supervised & Unsupervised Methods), Slides & Video (Supervised & Unsupervised Methods), K-means code (data preprocessing, base code, visualizations) |
| Galadriel Cho  | Proposal (Data Preprocessing & Algorithms/Models), Slides & Video (Data Preprocessing & Algorithms/Models, K-means code (data preprocessing, base code, visualizations) |
| Arya Nalavade  | Proposal (Goals & Expected Results), Slides & Video (Goals & Expected Results), Midterm (Results & Discussion) |

# GitHub Repository
https://github.gatech.edu/ashah726/ashah726.github.io

## Directory
```
.
├── kmeans
│   └── breast_cancer_kmeans.ipynb
├── svm
│   ├── breast_cancer_svm.ipynb
│   ├── gitignore.txt
│   └── requirements.txt
├── README.md
└── _config.yaml
```

```
/kmeans/: Contains files related to the K-Means clustering algorithm.
/kmeans/breast_cancer_kmeans.ipynb: Jupyter Notebook implementing K-Means on the breast cancer dataset.

/svm/: Contains files r related to the Support Vector Machine (SVM) model.
/svm/breast_cancer_svm.ipynb: Jupyter Notebook implementing an SVM model on the breast cancer dataset.
/svm/gitignore.txt: Specifies files and directories to be ignored by version control.
/svm/requirements.txt: Lists Python dependencies required to run the notebook code.

/README.md: Project documentation (proposal & midterm).
/_config.yaml: Configuration file used for project settings, environment configuration, and static site generation (GitHub Pages).
```

# Proposal Slidedeck & Video 
- https://docs.google.com/presentation/d/1FLcbaeM0SAPhENrqE2YTM4Voni2K-sQHjwmWEPyKncg/edit?usp=sharing
- https://youtu.be/732VsacyU7g

