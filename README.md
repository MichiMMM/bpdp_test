# Usage of this repository
This repository is supposed to help to reproduce the work proposed in the paper "Business Process Deviation Prediction: Predicting Non-Conforming Process Behavior"

The file "BPDP_Code.ipynb" contains all code used to implement and evaluate the proposed approach. The function "BPDP_classification_CIBE" executes the approach using the complex index-based encoding (BPDP<sub>CIBE</sub>) while the function "BPDP_classification_MPPN" uses the pre-trained feature vectors from MPPN (BPDP<sub>MPPN</sub>). 

To train BPDP using the feature vectors created by MPPN:
- Train the MPPN using the code from https://github.com/joLahann/mppn
- Store the feature vectors per prefix in a pandas dataframe. Each row represents one prefix where "idx" is the unique id of the prefix and "FV" the learned feature vector of it

To execute the classification using the Genga et. al. approach (Genga et. al. [9]), use the function "genga_benchmark". For the CatBoost classification (CatBoost), execute "classify_cat" and to use suffix prediction (Suffix Prediction) for deviation prediction (Suffix Prediction), execute "suffix_prediction_deviations".

To execute BPDP using a single classifier (BPDP<sub>SC,CIBE</sub>), execute "BPDP_single_classifier". For BPDP without undersampling and weighted loss (BPDP<sub>MC,No Imbalance</sub>), use "BPDP_no_imbalance".

The folder "Evaluation" contains all evaluation results displayed in the paper. This folder contains all event logs, to-be models, and frozen alignments. Please load the respective data from the folder "Datasets" before. 


# Precision, Recall, and F1-Score for a Single Classifier for all Deviations (BPDP<sub>SC,CIBE</sub>) and for Multiple Classifier without Undersampling and Weighted Loss (BPDP<sub>MC,No Imbalance</sub>)
As mentioned in the dicsussion section, the following table illustrates that BPDP<sub>SC,CIBE</sub> and BPDP<sub>MC,No Imbalance</sub> perform worse than the proposed approaches BPDP<sub>CIBE</sub> and BPDP<sub>MPPN</sub>.
![plot](./Evaluation/figures/sc_noimb_bpdp.png)


# Hyperparameteroptimization
We performed a HPO for the following discrete values for hyperparameters of BPDP (**boldness** indicates the best performing value):

WCEL weighted loss: [4, 8, **16**, 24, 32]

Dropout: [0.0, **0.1**, 0.2]

Network Size: [32x32, 64x64, **256x256**, 512x256x256]

For more information, we refer to the Excel file "HyperParameterOptimization.xlsx" in the folder "Evaluation", which portrays the performance of the different changed hyperparameters in comparison to the proposed BPDP approach for the CIBE encoding.


# Further Shapley value plots
The following graphs show Shapley value plots for all deviations of the BPIC 12A event log. 

## ('>>', 'A_APPROVED')
![plot](./Evaluation/Shapley_Values/ShapValues_12A_Model_A_APPROVED.png)

## ('A_APPROVED', '>>')
![plot](./Evaluation/Shapley_Values/ShapValues_12A_Log_A_APPROVED.png)

## ('>>', 'A_DECLINED')
![plot](./Evaluation/Shapley_Values/ShapValues_12A_Model_A_DECLINED.png)

# Evaluation metrics per deviation type for BPIC 12A

To illustrate the varying performance over deviations, we show the evaluation metrics for the three deviation types in BPIC 12A individually.

|           | Dev                                                           |||| No Dev                                                        ||||
|-----------|------------------|------------------|------------------|---------|------------------|------------------|------------------|---------|
|Metric     | (>>, A_APPROVED) | (A_APPROVED, >>) | (>>, A_DECLINED) | Average | (>>, A_APPROVED) | (A_APPROVED, >>) | (>>, A_DECLINED) | Average |
| Precision | 0.1587           | 0.2166           | 0.1108           | 0.1620  | 0.9576           | 0.9468           | 0.9964           | 0.9669  |
| Recall    | 0.7770           | 0.7557           | 0.8926           | 0.8084  | 0.5503           | 0.6143           | 0.8043           | 0.6563  |
| ROC_AUC   | 0.6637           | 0.6850           | 0.8485           | 0.7324  | 0.6637           | 0.6850           | 0.8485           | 0.7324  |
 
